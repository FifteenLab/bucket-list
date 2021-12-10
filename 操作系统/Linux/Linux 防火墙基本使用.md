### Firewalld 常用命令

**启动配置命令**

~~~shell
# 查看防火墙状态
systemctl status firewalld
# 启动防火墙
systemctl start firewalld
# 停用防火墙
systemctl stop firewalld
# 重启防火墙
systemctl restart firewalld
# 设置开机启动
systemctl enable firewalld
# 查看是否开机启动
systemctl is-enabled firewalld
~~~

**操作命令**

~~~shell
# 查看开放的端口
firewall-cmd --list-ports
# 开启端口
firewall-cmd --zone=public --add-port=22/tcp --permanent
# 删除端口
firewall-cmd --zone= public --remove-port=22/tcp --permanent
# 加载规则
firewall-cmd --reload
~~~

#### 开启端口

~~~shell
firewall-cmd --zone=public --add-port=22/tcp --permanent
~~~

> -zone：作用域
>
> -add-port：添加端口，格式：端口/通讯协议
>
> -permanent：永久生效，没有此参数重启后失效

