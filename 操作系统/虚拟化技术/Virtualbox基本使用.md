## 简介

官方文档：

https://www.virtualbox.org/manual/UserManual.html

## 安装

### 安装扩展包

1、下载扩展包

~~~shell
wget https://download.virtualbox.org/virtualbox/6.1.30/Oracle_VM_VirtualBox_Extension_Pack-6.1.30.vbox-extpack
~~~

> 需要根据实际安装的virtualbox版本，下载对应的扩展包，版本号必须保持一直
>
> 查看VirtualBox 版本号：
>
> VBoxManage --version

2、安装扩展包

~~~shell
VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.30.vbox-extpack
~~~

3、查看安装的扩展包

~~~shell
VBoxManage list extpacks
~~~

### 卸载插件

~~~shell
VBoxManage extpack uninstall "Oracle VM VirtualBox Extension Pack"
~~~

### 

## 基本使用

### 设置远程桌面

1、查看虚拟机列表，找到uuid 或者 vm-name

~~~shell
VBoxManage list vms
~~~

2、配置VRDE

~~~shell
# 配置监听端口--开机情况下
VBoxManage controlvm <uuid|vmname> vrdeport 3390
# 关机情况下
VBoxManage modifyvm <uuid|vmname> --vrdeport 3390
# 设置认证类型
VBoxManage modifyvm <uuid|vmname> --vrdeauthtype null
~~~

3、启动VRDE

~~~shell
# 开机情况下
VBoxManage controlvm <uuid|vmname> vrde on

# 关机情况下
VBoxManage modifyvm <uuid|vmname> --vrde on
~~~

4、修改防火墙，放开对应端口

~~~shell
firewall-cmd --zone=public --add-port=3390/tcp
~~~

5、使用Window 远程桌面，连接宿主机IP+端口

### 查看虚拟机

~~~shell
# 查看虚拟机列表
VBoxManage list vms
# 查看运行列表
VBoxManage list runningvms
# 查看虚拟机详情
VBoxManage showvminfo <uuid|vmname>
~~~

### 启停虚拟机

~~~shell
# 关机
VBoxManage controlvm <uuid|vmname> poweroff
# 开机
VBoxManage startvm <uuid|vmname> --type headless
~~~

### 挂载媒介

~~~shell
# 添加控制器（IED、STAT等）
VBoxManage storagectl <uuid|vmname> --name IDE --add ide --controller PIIX4 --bootable on

# 挂载ISO镜像
VBoxManage storageattach <uuid|vmname> --storagectl "IDE" --port 0 --device 0 --type dvddrive --medium <ISO filename>
# 移除ISO镜像
VBoxManage storageattach <uuid|vmname> --storagectl "IDE" --port 0 --device 0 --type dvddrive --medium none

# 挂载磁盘
VBoxManage storageattach <uuid|vmname> --storagectl "SATA" --port 0 --device 0 --type hdd --medium <hd filename>
# 移除磁盘
VBoxManage storageattach <uuid|vmname> --storagectl "SATA" --port 0 --device 0 --type hdd --medium none
~~~







