## 环境说明

系统版本：Centos 7.9.2009  3.10.0-1127.el7.x86_64

Redis版本：6.2.6

## 简介

Redis 官方网站：https://redis.io/

## 安装配置

~~~shell
wget https://download.redis.io/releases/redis-6.2.6.tar.gz
tar -zxvf redis-6.2.6.tar.gz

cd redis-6.2.6/
cd src/
make install PREFIX=/usr/local/redis

cd ../
mkdir /usr/local/redis/etc
cp redis.conf /usr/local/redis/etc/

vim /usr/local/redis/etc/redis.conf
~~~

> requirepass 1q2w3e4r
>
> bind * -::1
>
> daemonize yes

~~~shell
# 配置开启启动
vim /etc/rc.local
~~~

> 添加如下内容
>
> /usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf



~~~shell
# 启动redis
/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
# 停止redis
pkill redis
~~~

