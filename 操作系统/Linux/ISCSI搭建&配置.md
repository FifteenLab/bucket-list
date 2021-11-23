## ISCSI 简介

iSCSI全称Internet Small Computer System Interface，是一种由IBM公司研究开发的IPSAN技术。该技术是将现有SCSI接口与以太网络(Ethernet)技术结合，基于 TCP/IP的协议连接**iSCSI服务端（Target）**和**客户端(Initiator)**，使得封装后的SCSI数据包可以在通用互联网传输，最终实现iSCSI服务端映射为一个存储空间（磁盘）提供给已连接认证后的客户端。



## ISCSI Target & Initiator 搭建

### 1）ISCSI Target 搭建

1、安装 iscsi targetd 。

~~~shell
yum install -y targetd
~~~

2、安装 targetcli。

~~~shell
# 安装targetcli
yum install -y targetcli
~~~

3、使用 targetcli 配置ISCSI Target 服务。

~~~shell
# 进入targetcli
targetcli

> cd backstores/fileio
# 创建几个节点，此处使用的磁盘镜像文件，可以直接指定磁盘分区
> create disk01 /opt/ftp/disk.img 5G
# 创建target
> create /iscsi
> create iqn.2021-11.com.zrcctv:server
# 配置lun
> cd iqn.2021-11.com.zrcctv:server/tpg1/luns
> create /backstores/fileio/disk01 # 节点名称
# 配置ACL
> cd /iscsi/iqn.2021-11.com.zrcctv:server/tpg1/acls
# 客户端的InitiatorName需要和此处保持一直
> create iqn.2021-11.com.zrcctv:client
# 创建认证的userid、password
> cd iqn.2021-11.com.zrcctv:client
> set auth userid=admin
> set auth password=zerui123
# 退出并保存
> exit
~~~

4、启动 iscsi target 并配置开机启动。

~~~shell
# 启动Target服务
systemctl start target
# 查看Target状态
systemctl status target
# 配置开机启动
systemctl enable target
~~~

### 2）ISCSI Initiator 使用

1、安装iscsi-initiator-utils。

~~~shell
 yum install -y iscsi-initiator-utils
~~~

2、配置initiatorname

~~~shell
vim /etc/iscsi/initiatorname.iscsi
# InitiatorName 需要和ISCSI Target 的ACL配置保持一直。
# InitiatorName=iqn.2021-11.com.zrcctv:server
~~~

3、配置认证

~~~shell
vi /etc/iscsi/iscsid.conf
# 按照如下内容修改
# node.session.auth.authmethod = CHAP
# node.session.auth.username = admin
# node.session.auth.password = zerui123
~~~

4、发现Target服务

~~~shell
iscsiadm -m discovery -t sendtargets -p 192.168.1.227
# 验证
iscsiadm -m node -o show | grep node.
~~~

5、登录

~~~shell
iscsiadm -m node --login
# 验证
iscsiadm -m session -o show
~~~

6、查看磁盘分区

~~~shell
lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
sda      8:0    0  40G  0 disk
└─sda1   8:1    0  40G  0 part /
sdb      8:16   0   5G  0 disk # iscsi 已经连上了
~~~

