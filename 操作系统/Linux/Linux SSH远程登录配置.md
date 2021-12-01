### SSH远程登录配置

~~~shell
vim /etc/ssh/sshd_config
~~~

> 修改ssh 端口
>
> Port 2200
>
> 限制Root用户远程登录
>
> PermitRootLogin no

~~~shell
# 重启SSHD
systemctl restart sshd
~~~

