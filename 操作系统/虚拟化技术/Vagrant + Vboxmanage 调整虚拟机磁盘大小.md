# Vagrant + Vboxmanage 调整虚拟机磁盘大小

## 调整虚拟机磁盘大小

找到VirtualBox 存储位置，vmdk 格式不能直接调整磁盘大小，需要克隆磁盘为vdi格式再修改大小。具体操作步骤如下：

1、使用vagrant 关闭虚拟机。

~~~shell
$ vagrant halt <machine_id>
# machine id 可使用 vagrant global-status 查看。
~~~

2、进入vmdk所在文件目录。

~~~shell
$ cd /c/Users/user/VirtualBox\ VMs/
~~~

3、查看磁盘uuid，并记录。

~~~shell
$ vboxmanage showhdinfo centos-7-1-1.x86_64.vmdk
UUID:           aafec154-54e2-49aa-b3fe-fc34a7f0d262
# 记录UUID，在第8步中需要用到
Parent UUID:    base
State:          created
Type:           normal (base)
Location:       C:\Users\user\VirtualBox VMs\centos7_default_1636533266998_50081\centos-7-1-1.x86_64.vmdk
Storage format: VMDK
Format variant: dynamic default
Capacity:       40960 MBytes
Size on disk:   1178 MBytes
Encryption:     disabled
In use by VMs:  centos7_default_1636533266998_50081 (UUID: f3351386-6b84-452f-b818-1563db33c16b)
~~~

4、克隆磁盘，改用vdi格式。

~~~shell
$ vboxmanage clonehd centos-7-1-1.x86_64.vmdk new-virtualdisk.vdi --format vdi
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Clone medium created in format 'vdi'. UUID: 86cfbf44-4a81-4b33-82ca-acbf2c143484
# 这里生成了一个新UUID
~~~

5、调整克隆磁盘的大小。单位M

~~~shell
$ vboxmanage modifyhd new-virtualdisk.vdi --resize 81920
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
~~~

6、覆盖原磁盘。

~~~shell
$ vboxmanage clonehd new-virtualdisk.vdi resized.vmdk --format vmdk
0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Clone medium created in format 'vmdk'. UUID: 0666a0cb-e0a8-41de-b284-906dd73d7cba
# 又产生了一个新的UUID

$ mv resized.vmdk centos-7-1-1.x86_64.vmdk
~~~

7、删除vdi 格式磁盘。

~~~shell
$ rm new-virtualdisk.vdi

# 不修改磁盘UUID的情况下尝试启动
$ vagrant up b2cbab7
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["startvm", "f3351386-6b84-452f-b818-1563db33c16b", "--type", "headless"]
# 此处报错也给出了启动失败的原因
Stderr: VBoxManage.EXE: error: UUID {0666a0cb-e0a8-41de-b284-906dd73d7cba} of the medium 'C:\Users\user\VirtualBox VMs\centos7_default_1636533266998_50081\centos-7-1-1.x86_64.vmdk' does not match the value {aafec154-54e2-49aa-b3fe-fc34a7f0d262} stored in the media registry ('C:\Users\user\.VirtualBox\VirtualBox.xml')
VBoxManage.EXE: error: Details: code E_FAIL (0x80004005), component MediumWrap, interface IMedium
~~~

8、修改磁盘UUID。

~~~shell
$ vboxmanage internalcommands sethduuid centos-7-1-1.x86_64.vmdk aafec154-54e2-49aa-b3fe-fc34a7f0d262
UUID changed to: aafec154-54e2-49aa-b3fe-fc34a7f0d262
~~~

9、使用vagrant 启动虚拟机。

~~~shell
vagrant up b2cbab7
~~~

## 创建盘分区

ssh 登录虚拟机，查看磁盘大小，现在磁盘已经由原来的40G扩容到80G。使用fdisk 创建盘分区。