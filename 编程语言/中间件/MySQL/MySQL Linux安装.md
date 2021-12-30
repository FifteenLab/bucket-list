## 安装&配置

### 安装

~~~shell
# 下载安装包

# 解压安装包
tar -zxvf mysql-5.7.36-linux-glibc2.12-x86_64.tar.gz
# 将安装包移动至/usr/local目录下
mv -f mysql-5.7.36-linux-glibc2.12-x86_64 /usr/local/mysql
# 创建mysql 数据存储目录
mkdir -p /data/mysql
# 创建mysql 用户组和用户，并修改数据存储目录权限
groupadd mysql
useradd -r -g mysql mysql
chown -R mysql:mysql /data/mysql

~~~

### 配置

~~~shell
# 修改mysql 配置文件
vim /etc/my.cnf
~~~

#### my.cnf

> [mysqld]
>
> datadir=/data/mysql
>
> port=3306
>
> max_connections=400
>
> innodb_file_per_table=1
>
> lower_case_table_names=1
>
> character_set_server=utf8
>
> socket=/data/mysql/mysql.sock
>
> symbolic-links=0
>
> 
>
> [mysqld_safe]
>
> log-error=/data/mysql/mariadb.log
>
> pid-file=/var/run/mariadb/mariadb.pid

### 初始化

~~~shell
cd /usr/local/mysql/bin/
# 执行初始化操作并记录root用户默认密码
./mysqld --defaults-file=/etc/my.cnf --basedir=/usr/local/mysql/ --datadir=/data/mysql/ --user=mysql --initialize

# 启动测试
/usr/local/mysql/support-files/mysql.server start
~~~

> x9GgoFzEn+N(

~~~shell
# 创建软连接
ln -s /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql.server
ln -s /usr/local/mysql/bin/mysql /usr/bin/mysql
# 配置开机启动
chkconfig --add mysql.server
# 使用service 启动mysql
service mysql restart
~~~

### 修改Root密码

~~~shell
# 登录mysql
mysql -u root -h 127.0.0.1 -p'x9GgoFzEn+N('
~~~

~~~shell
# 修改密码
SET PASSWORD = PASSWORD('1q2w3e4r');
ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
FLUSH PRIVILEGES;
~~~

退出重新登陆MySQL，配置root用户允许任何host访问。

~~~shell
use mysql;
update user set host='%' where user='root';
flush privileges;
~~~

## FAQ

Q：MySQL初始化报缺少`libaio.so.1`。

>[root@localhost bin]# ./mysqld --initialize --user=mysql --datadir=/data/mysql --basedir=/usr/local/mysql
>./mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory

A：安装`libaio.so.1`包。

~~~shell
yum install libaio-devel.x86_64
~~~

