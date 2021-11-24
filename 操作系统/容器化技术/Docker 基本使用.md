# Docker 

DockerHub：https://registry.hub.docker.com/

Docker 官网：https://www.docker.com/

## Docker 安装&卸载

系统环境：Centos 7

参考：https://docs.docker.com/engine/install/centos/

### 安装

1、设置yum源

~~~shell
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
~~~

2、查询docker版本

~~~shell
yum list docker-ce --showduplicates | sort -r
~~~

3、安装指定版本

~~~shell
sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
~~~

4、启动Docker

~~~shell
sudo systemctl start docker
# 查看Docker状态
sudo systemctl status docker
~~~

5、设置开机启动

~~~shell
sudo systemctl enable docker
~~~

#### 坑点

1、安装失败，强制安装最新版的containerd

~~~shell
yum install https://download.docker.com/linux/fedora/30/x86_64/stable/Packages/containerd.io-1.2.6-3.3.fc30.x86_64.rpm
~~~

### 卸载

~~~shell
# 卸载
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
# 删除docker 文件
rm -rf /var/lib/docker
~~~

## Docker 常用命令

### Docker 镜像

~~~shell
# 查询镜像
docker images
# 删除镜像
docker rmi <image-name>
# 基于Dockerfile 创建镜像
docker build -t <image-name:version> .
~~~

### Docker 容器

~~~shell
# 启动容器
docker run --name <continer-name> <image-name>
# 启动容器并后台运行
docker run -d --name <continer-name> <image-name:version>
# 查看容器
docker container ls -al
# 删除容器
docker rm <continer-name>
# 停止容器
docker container stop <container-name>
# 查询容器运行情况
docker container ps -al
# 进入容器
docker exec -it <container-name> /bin/bash
~~~

#### docker run

> -d ：后台运行
>
> -p ：配置端口映射
>
> -e ：配置环境变量



## Dokcerfile

~~~
# 
FROM openjdk:8
# 
MAINTAINER liubing@zrcctv.com
# 
ADD zerui-media.jar /opt/media/zerui-media.jar
# 
ENV HOST_IP=192.168.33.13
# 
WORKDIR /opt/media/
#
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Xbootclasspath/a:/opt/media/config","-jar","/opt/media/app.jar"]

~~~



# Docker Compose

GitHub：https://github.com/docker/compose/releases

### 安装

~~~shell
# 下载
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 添加可执行权限
sudo chmod +x /usr/local/bin/docker-compose
# 创建软连接
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
# 测试是否安装成功
docker-compose --version
~~~

### 常用命令

~~~shell
# 启动
docker-compose up 
# 停止容器
docker-compose stop
# 
~~~

#### docker-compose up

> -d 后台运行
>
> --build 重新创建容器
