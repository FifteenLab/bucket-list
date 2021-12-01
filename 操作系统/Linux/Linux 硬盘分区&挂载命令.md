## 创建磁盘分区

1、查看磁盘分区

~~~shell
$ fdisk -l

Disk /dev/sda: 85.9 GB, 85899345920 bytes, 167772160 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x0009ef1a

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    83886079    41942016   83  Linux
~~~

2、开始分区

~~~shell
$ fdisk /dev/sda
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): p # 打印磁盘分区
Command (m for help): n # 创建新分区
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): p # p - 主分区；e - 扩展分区
Partition number (2-4, default 2): 2 # 分区编号
First sector (83886080-167772159, default 83886080): # 开始柱面
Using default value 83886080
Last sector, +sectors or +size{K,M,G} (83886080-167772159, default 167772159): +20G # 结束柱面或分组大小
Partition 2 of type Linux and of size 20 GiB is set

Command (m for help): w # 保存提出
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
Syncing disks.
~~~

### fdisk 指令

~~~shell
Command (m for help): m # 帮助文档
Command action
   a   toggle a bootable flag
   b   edit bsd disklabel
   c   toggle the dos compatibility flag
   d   delete a partition
   g   create a new empty GPT partition table
   G   create an IRIX (SGI) partition table
   l   list known partition types
   m   print this menu
   n   add a new partition
   o   create a new empty DOS partition table
   p   print the partition table
   q   quit without saving changes # 退出不保存
   s   create a new empty Sun disklabel
   t   change a partition's system id
   u   change display/entry units
   v   verify the partition table
   w   write table to disk and exit # 保存退出
   x   extra functionality (experts only)

~~~



## 磁盘挂载

编辑好分区表之后，就需要创建新的文件系统了。使用mkfs 命令格式化分区。格式化分区之前需要重启。

### 格式化分区

~~~shell
$ sudo mkfs -t ext4 /dev/sda2 
~~~

~~~shell
# 未重启的情况下尝试格式化
mke2fs 1.42.9 (28-Dec-2013)
Could not stat /dev/sda2 --- No such file or directory

The device apparently does not exist; did you specify it correctly?
~~~

### 挂载

1、创建挂载目录

~~~shell
$ mkdir /data
~~~

2、挂载

~~~shell
$ sudo mount /dev/sda2 /data
~~~

3、设置开机自动挂载

~~~shell
echo "/dev/sda2 /data ext4 default 0 0" >> /etc/fstab
~~~

### 卸载

~~~shell
sudo umount /dev/sda2
~~~

### FAQ

1、目录卸载失败

~~~shell
umount: /tmp/mondo.tmp.pI8wfh/mountpoint.8372: target is busy.
~~~

使用`lsof`命令查询占用情况

~~~shell
lsof | grep '/tmp/'
~~~



## 磁盘常用命令

~~~shell
lsblk
fdisk -l
df -h
~~~

