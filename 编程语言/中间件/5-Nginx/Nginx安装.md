## 环境说明

系统版本：Centos 7.9.2009  3.10.0-1127.el7.x86_64

Nginx版本：

## 安装配置

~~~shell
sudo yum install yum-utils
~~~

创建`/etc/yum.repos.d/nginx.repo`。

~~~text
[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

[nginx-mainline]
name=nginx mainline repo
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/
gpgcheck=1
enabled=0
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true
~~~

执行安装命令

~~~shell
yum install nginx
~~~

启动服务

~~~shell
# 启动
systemctl start nginx
# 查看状态
systemctl status nginx
# 设置开机启动
systemctl enable nginx
# 查看开机启动状态
systemctl is-enabled nginx
~~~

