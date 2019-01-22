title: docker从0开始
author: MiracleQi-温柔魔君
tags:
  - Docker
categories:
  - 虚拟化
cover: /img/post-cover/12.jpg
date: 2016-08-16 09:33:00
---
docker 的安装及常用命名

## 1. 安装 Docker  

当前环境为 Debian8  
在 Ubuntu 14.04 及以上版本安装 Docker

### 1.1 方法一：简化版安装 docker
```
wget -qO- https://get.docker.com/ | sh
```

### 1.2 方法二：从 Docker 官方源安装最新版本
```
  $ sudo apt-get install apt-transport-https
  $ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
  $ sudo bash -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
  $ sudo apt-get update
  $ sudo apt-get install -y lxc-docker
  $ sudo apt-get update -y lxc-docker​​
```

### 1.3 方法三：docker.io

```
  $ sudo apt-get update
  $ sudo apt-get install -y docker.io
  $ sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
  $ sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io
```
使用 Ubuntu14.04 系统默认自带 docker.io 安装包安装 Docker，这样安装的Docker 版本相对较旧，并不推荐使用。

## 2. 镜像

### 2.1 获取镜像

```
  $ sudo docker pull NAME[:TAG]
  
  如 '$ sudo docker pull ubuntu'，该命令实际下载的是 ubuntu:lastest 镜像
  此命令相当于 '$ sudo docker pull registry.hub.docker.com/ubuntu:latest' 命令
  即从默认的注册服务器 registry.hub.docker.com 中的 ubuntu 仓库来下载标记为 latest 的镜像
```
    

### 2.2 查看镜像信息
```
  $ sudo docker images          可以列出本地主机上已有的镜像
  $ sudo docker inspect IMAGEID 可以获取镜像的详细信息
```
### 2.3 搜寻镜像
```
  $ sudo docker search OpenWAF
  
  默认搜索 Docker Hub官方仓库中的镜像
  支持的参数：
    --autometad=false 仅显示自动创建的镜像
    --no-trunc=false    ​输出信息不截断显示
```

### 3. docker-enter
docker run -d 跑起一个容器后，使用 docker-enter 方便进入管理，代码如下：
```
#!/bin/sh
if [ -e $(dirname "$0")/nsenter ]; then
    # with boot2docker, nsenter is not in the PATH but it is in the same folder
    NSENTER=$(dirname "$0")/nsenter
else
    NSENTER=nsenter
fi
if [ -z "$1" ]; then
    echo "Usage: `basename "$0"` CONTAINER [COMMAND [ARG]...]"
    echo ""
    echo "Enters the Docker CONTAINER and executes the specified COMMAND."
    echo "If COMMAND is not specified, runs an interactive shell in CONTAINER."
else
    PID=$(docker inspect --format "{{.State.Pid}}" "$1")
    if [ -z "$PID" ]; then
         exit 1
    fi
    shift
    OPTS="--target $PID --mount --uts --ipc --net --pid --"
    if [ -z "$1" ]; then
         # No command given.
         # Use su to clear all host environment variables except for TERM,
         # initialize the environment variables HOME, SHELL, USER, LOGNAME, PATH,
         # and start a login shell.
         "$NSENTER" $OPTS su - root
    else
         # Use env to clear all host environment variables.
         "$NSENTER" $OPTS env --ignore-environment -- "$@"
    fi
fi 
```
```
  将 docker-enter 放入 /bin/ 目录下
  chmod +x docker-enter
  cp -P docker-enter /bin/
 ```
## 4. docker 常用命令

### 4.1 docker build
自己经常写 Dockerfile ，常用到 docker build 命令
```
创建 openwaf 仓库下的 debian8 镜像    
docker build -t openwaf:debian8 .
有时Dockerfile内容无变化，想要重新生成镜像，却不想用 docker 的cache 
docker build --no-cache -t openwaf:debian8 .
```
### 4.2 docker rm
```
删除未运行的容器
docker rm container_id1 container_id2
强制删除容器
docker rm -f container_id1 container_id2
删除所有未运行容器
docker rm $(docker container ls -a -q)

强制删除所有容器
docker rm -f $(docker container ls -a -q)
删除镜像
docker rmi image_id1 image_id2
```
### 4.3 docker images

用于查看 docker 镜像仓库

### 4.4 docker ps
```
查看运行中容器
docker ps
查看所有容器
docker ps -a
```