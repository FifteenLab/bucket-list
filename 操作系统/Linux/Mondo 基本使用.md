### Mondo 简介

官方网址：http://www.mondorescue.org/

官方文档：http://www.mondorescue.org/docs/mondorescue-howto.html

### Mondo 安装

1、添加yum 镜像地址

~~~shell
cd /etc/yum.repos.d
wget http://ftp.mondorescue.org/rhel/7/x86_64/mondorescue.repo
vim mondorescue.repo
~~~

~~~tex
[mondorescue]
name=rhel 7 x86_64 - mondorescue Vanilla Packages
baseurl=ftp://ftp.mondorescue.org//rhel/7/x86_64
enabled=1
gpgcheck=0
gpgkey=ftp://ftp.mondorescue.org//rhel/7/x86_64/mondorescue.pubkey
~~~

> 官方资源地址：http://ftp.mondorescue.org/

2、使用yum安装 

~~~shell
yum -y install mondo
~~~

### Mondo 基本使用

使用Root用户执行`mondoarchive`命令。

~~~shell
mondoarchive
~~~

