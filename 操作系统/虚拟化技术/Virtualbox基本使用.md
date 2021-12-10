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

### 开启远程桌面

1、查看虚拟机列表，找到uuid 或者 vm-name

~~~shell
VBoxManage list vms
~~~

2、配置VRDE监听端口

~~~shell
# 开机情况下
VBoxManage controlvm bf904f4d-6d4d-4729-a8e2-e6815c9c3bb3 vrdeport 3390
# 关机情况下
VBoxManage modifyvm c3ae2198-6004-4b4a-8181-487774bcd170 --vrdeport 3390
~~~

3、启动VRDE

~~~shell
# 开机情况下
VBoxManage controlvm edff54c5-46e9-4539-bbee-0f1974bc05d5 vrde on

# 关机情况下
VBoxManage.exe modifyvm c3ae2198-6004-4b4a-8181-487774bcd170 --vrde on
~~~

4、修改防火墙，放开对应端口

~~~shell
firewall-cmd --zone=public --add-port=3390/tcp
~~~

5、使用Window 远程桌面，连接宿主机IP+端口





