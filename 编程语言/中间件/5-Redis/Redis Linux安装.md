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
~~~

### 配置

~~~shell
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

### 开机启动

#### 复制启动脚本

~~~shell
cd redis-6.2.6/utils
cp redis_init_script /etc/init.d/redis
~~~

#### 修改启动脚本

1、脚本第一行后面添加如下内容

~~~shell
# Bomments to support chkconfig on RedHat Linux
# chkconfig: 2345 80 90
~~~

2、修改安装路径

> REDISPORT=6379
> EXEC=/usr/local/bin/redis-server
> CLIEXEC=/usr/local/bin/redis-cli
>
> PIDFILE=/var/run/redis_${REDISPORT}.pid
> CONF="/etc/redis/${REDISPORT}.conf"

~~~shell
# 添加执行权限
chmod +x /etc/init.d/redis
# 配置开机启动
chkconfig --add redis
chkconfig redis on
# 查看注册的脚本
chkconfig --list 
~~~

> 添加如下内容
>
> /usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf

### 手动启动

~~~shell
# 启动redis
/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
# 停止redis
pkill redis
~~~

