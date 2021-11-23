# Virtualbox

## 下载安装
[Virtualbox 下载地址](https://www.virtualbox.org/wiki/Downloads)

# Vagrant
[Vagrant官网](www.vagrantup.com)

## 下载安装
[Vagrant 下载地址](https://www.vagrantup.com/downloads)

## 基本使用
### 下载镜像
Vagrant 镜像仓库请访问 [Vagrant Boxs](https://app.vagrantup.com/boxes/search)，我个人使用的是 Centos/7。

* 官方下载地址: [Vagrant box centos/7](https://app.vagrantup.com/centos/boxes/7)
* 百度云下载地址：链接：https://pan.baidu.com/s/1IsBqFx8XUUUFpfmtYxmKYg  提取码：7v1f
* 中科大镜像地址：[Centos/7 Images](https://mirrors.ustc.edu.cn/centos-cloud/centos/7/vagrant/x86_64/images/)

### 添加本地镜像文件
~~~shell
vagrant box add centos/7 CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box
~~~
#### 查看本地镜像列表
完成镜像添加后使用`list` 指令查看本地镜像列表。
```shell
 vagrant box list
```
#### 删除镜像
针对添加错误的镜像如果要删除，则使用`remove`指令，删除镜像。
~~~shell
vagrant box remove centos/7
~~~

### 初始化虚拟机
创建虚拟机目录，在目录下执行`init`命令完成虚拟机的初始化。
```shell
 vagrant init centos/7
```
完成虚拟机初始化后，系统会自动在当前目录下生成`Vagrantfile`文件。
### 启动虚拟机
完成虚拟机初始化后，执行`up`命令启动虚拟机。
~~~shell
vagrant up
~~~
### 登录虚拟机

~~~shell
vagrant ssh
~~~



## Vagrant问题

### Q1: window 文件同步失败

需要安装 `vagrant-vbguest`插件

~~~ shell
vagrant plugin install vagrant-vbguest
~~~

Github: https://github.com/dotless-de/vagrant-vbguest



## Vagrantfile 文件详解

*待补充。。。。*