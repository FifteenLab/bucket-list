

### Vagrant 常用命令

~~~shell
# 添加镜像文件
vagrant box add <box-name> <box-file.box>
# 查看本地镜像列表
vagrant box list
# 删除镜像
vagrant box remove centos/7
# 初始化虚拟机
vagrant init centos/7
# 启动虚拟机
vagrant up
# 关闭虚拟机
vagrant halt 
# 登录虚拟机
vagrant ssh
# 销毁虚拟机
vagrant destroy
# 全局查看虚拟机状态
vagrant global-status
# 修改配置文件后，重新加载虚拟机
vagrant reload
~~~

#### vagrant box

> add：添加镜像
>
> list：查看本地镜像列表
>
> remove：删除本地镜像



### Vagrantfile 配置文件

