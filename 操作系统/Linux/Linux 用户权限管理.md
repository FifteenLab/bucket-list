## 用户操作

~~~shell
# 添加用户
useradd -m <username>
# 修改用户密码
passwd <username>
# 修改用户组
usermod -G <用户组> <用户名>
~~~

### 修改Root密码

~~~ shell
sudo passwd root
~~~



### Wheel用户组

wheel组类似于管理员组。将用户添加到wheel 组可以使用`sudo` 获取到管理员权限。

~~~shell
#添加用户到wheel组
usemod -G wheel <用户名>
~~~





## 权限操作







