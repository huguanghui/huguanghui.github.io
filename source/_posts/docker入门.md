---
title: docker入门
categories:
  - 操作系统
tags:
  - 软件
reward: true
originContent: >-
  ## 简介


  Docker 是世界领先的软件容器平台。开发人员利用 Docker 可以消除协作编码时“在我的机器上可正常工作”的问题。运维人员利用 Docker
  可以在隔离容器中并行运行和管理应用，获得更好的计算密度。企业利用 Docker 可以构建敏捷的软件交付管道，以更快的速度、更高的安全性和可靠的信誉为
  Linux 和 Windows Server 应用发布新功能。


  [中文官网](http://www.docker-cn.com/)


  [DockerHub](https://hub.docker.com/)


  ## 安装


  ### Ubuntu上的安装

  ```shell

  // 卸载旧版本

  $apt-get remove docker docker-engine docker.io

  // 使用存储库进行安装

  $ apt-get install \
      apt-transport-https \
      ca-certificates \
      curl \
      software-properties-common
  // 添加Docker的官方GPG密钥

  $ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo
  apt-key add -

  // 添加Docker软件源

  $ sudo add-apt-repository \
      "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
      $(lsb_release -cs) \
      stable"
  $sudo apt-get install docker-ce

  // 运行hello-world

  $docker run hello-world

  // 以非root用户身份运行docker

  $sudo groupadd docker

  $sudo usermod -aG docker $USER

  ```


  ## 使用


  [部署](https://juejin.im/post/5a4858235188257d6a7ee393)


  ### 使用中国的官方镜像加速


  ```shell

  // 守护进程传参

  $ docker --registry-mirror=https://registry.docker-cn.com daemon

  // 通过配置项来修改 /etc/docker/daemon.json

  {
    "registry-mirrors": ["https://registry.docker-cn.com"]
  }

  ```


  ### docker远程仓库的使用


  ```shell

  $docker tag local-image:tagname new-repo:tagname

  $docker push new-repo:ragname

  ```


  ### 构建应用


  创建Dockerfile, app.py, requirements.txt


  ```shell

  $docker build -t friendlyhello .

  ```


  ### 运行应用


  -d 后台运行


  -p 内外端口映射


  ```shell

  $docker run -d -p 4000:80 friendlyhello

  ```


  停止服务


  ```shell

  $docker ps

  $docker stop ${CONTAINER ID}

  ```


  ### 服务


  ```yaml

  # docker-compose.yml

  version: "3"

  services:
    web:
      # 将 username/repo:tag 替换为您的名称和镜像详细信息
      image: username/repository:tag
      deploy:
        replicas: 5
        resources:
          limits:
            cpus: "0.1"
            memory:50M
        restart_policy:
          condition: on-failure
      ports:
        - "80:80"
      networks:
        - webnet
  networks:
    webnet:
  ```


  运行新的应用


  ```shell

  $docker swarm init

  // 部署应用

  $docker stack deploy -c docker-compose.yml getstartedlab

  // 查看服务容器列表

  $docker stack ps getstartedlab

  // 修改docker-compose.yml参数再部署应用就是更新

  ```


  清除应用


  ```shell

  // 删除应用

  $docker stack rm getstartedlab

  // 清除swarm

  $docker swarm leave --force

  ```


  ### swarm集群


  利用Virtualbox来创建


  [VirtualBox安装](https://www.virtualbox.org/wiki/Downloads)


  ```shell

  $wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo
  apt-key add -

  ```


  [docker-machine安装](https://www.cnblogs.com/sparkdev/p/7044950.html)


  ```shell

  https://github.com/docker/machine/releases/

  ```


  ```shell

  // 创建一对VM

  docker-machine create --driver virtualbox myvm1

  docker-machine create --driver virtualbox myvm2

  ```


  myvm1发送命令


  ```shell

  $docker-machine ssh myvm1 "docker swarm init"

  // --advertise-addr错误的解决

  $docker-machine ssh myvm1 "docker swarm init --advertise-addr
  192.168.99.100:2377"

  ```


  ### 技术栈


  ```yaml

  version: "3"

  services:
    web:
      # 将 username/repo:tag 替换为您的名称和镜像详细信息
      image: huguanghui/helltest:latest
      deploy:
        replicas: 5
        resources:
          limits:
            cpus: "0.1"
            memory: 50M
        restart_policy:
          condition: on-failure
      ports:
        - "80:80"
      networks:
        - webnet
    visualizer:
      image: dockersamples/visualizer:stable
      ports:
        - "8080:8080"
      volumes:
        - "/var/run/docker.sock:/var/run/docker.sock"
      deploy:
        placement:
          constraints: [node.role == manager]
      networks:
        - webnet
  networks:
    webnet:
  ```


  ### 技巧总结


  #### 查看本地Docker镜像库

  ```shell

  $docker images

  ```


  #### 常用命令

  ```shell

  docker build -t friendlyname .# 使用此目录的 Dockerfile 创建镜像

  docker run -p 4000:80 friendlyname  # 运行端口 4000 到 90 的“友好名称”映射

  docker run -d -p 4000:80 friendlyname         # 内容相同，但在分离模式下

  docker ps                                 # 查看所有正在运行的容器的列表

  docker stop <hash>                     # 平稳地停止指定的容器

  docker ps -a           # 查看所有容器的列表，甚至包含未运行的容器

  docker kill <hash>                   # 强制关闭指定的容器

  docker rm <hash>              # 从此机器中删除指定的容器

  docker rm $(docker ps -a -q)           # 从此机器中删除所有容器

  docker images -a                               # 显示此机器上的所有镜像

  docker rmi <imagename>            # 从此机器中删除指定的镜像

  docker rmi $(docker images -q)             # 从此机器中删除所有镜像

  docker login             # 使用您的 Docker 凭证登录此 CLI 会话

  docker tag <image> username/repository:tag  # 标记 <image> 以上传到镜像库

  docker push username/repository:tag            # 将已标记的镜像上传到镜像库

  docker run username/repository:tag                   # 运行镜像库中的镜像

  docker search <key>                     # 搜索docker镜像

  ```
toc: false
date: 2018-12-24 20:06:03
description:
---

## 简介

Docker 是世界领先的软件容器平台。开发人员利用 Docker 可以消除协作编码时“在我的机器上可正常工作”的问题。运维人员利用 Docker 可以在隔离容器中并行运行和管理应用，获得更好的计算密度。企业利用 Docker 可以构建敏捷的软件交付管道，以更快的速度、更高的安全性和可靠的信誉为 Linux 和 Windows Server 应用发布新功能。

[中文官网](http://www.docker-cn.com/)

[DockerHub](https://hub.docker.com/)

## 安装

### Ubuntu上的安装
```shell
// 卸载旧版本
$apt-get remove docker docker-engine docker.io
// 使用存储库进行安装
$ apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
// 添加Docker的官方GPG密钥
$ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
// 添加Docker软件源
$ sudo add-apt-repository \
    "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
$sudo apt-get install docker-ce
// 运行hello-world
$docker run hello-world
// 以非root用户身份运行docker
$sudo groupadd docker
$sudo usermod -aG docker $USER
```

## 使用

[部署](https://juejin.im/post/5a4858235188257d6a7ee393)

### 使用中国的官方镜像加速

```shell
// 守护进程传参
$ docker --registry-mirror=https://registry.docker-cn.com daemon
// 通过配置项来修改 /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

### docker远程仓库的使用

```shell
$docker tag local-image:tagname new-repo:tagname
$docker push new-repo:ragname
```

### 构建应用

创建Dockerfile, app.py, requirements.txt

```shell
$docker build -t friendlyhello .
```

### 运行应用

-d 后台运行

-p 内外端口映射

```shell
$docker run -d -p 4000:80 friendlyhello
```

停止服务

```shell
$docker ps
$docker stop ${CONTAINER ID}
```

### 服务

```yaml
# docker-compose.yml
version: "3"
services:
  web:
    # 将 username/repo:tag 替换为您的名称和镜像详细信息
    image: username/repository:tag
    deploy:
      replicas: 5
      resources:
        limits:
          cpus: "0.1"
          memory:50M
      restart_policy:
        condition: on-failure
    ports:
      - "80:80"
    networks:
      - webnet
networks:
  webnet:
```

运行新的应用

```shell
$docker swarm init
// 部署应用
$docker stack deploy -c docker-compose.yml getstartedlab
// 查看服务容器列表
$docker stack ps getstartedlab
// 修改docker-compose.yml参数再部署应用就是更新
```

清除应用

```shell
// 删除应用
$docker stack rm getstartedlab
// 清除swarm
$docker swarm leave --force
```

### swarm集群

利用Virtualbox来创建

[VirtualBox安装](https://www.virtualbox.org/wiki/Downloads)

```shell
$wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
```

[docker-machine安装](https://www.cnblogs.com/sparkdev/p/7044950.html)

```shell
https://github.com/docker/machine/releases/
```

```shell
// 创建一对VM
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm2
```

myvm1发送命令

```shell
$docker-machine ssh myvm1 "docker swarm init"
// --advertise-addr错误的解决
$docker-machine ssh myvm1 "docker swarm init --advertise-addr 192.168.99.100:2377"
```

### 技术栈

```yaml
version: "3"
services:
  web:
    # 将 username/repo:tag 替换为您的名称和镜像详细信息
    image: huguanghui/helltest:latest
    deploy:
      replicas: 5
      resources:
        limits:
          cpus: "0.1"
          memory: 50M
      restart_policy:
        condition: on-failure
    ports:
      - "80:80"
    networks:
      - webnet
  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints: [node.role == manager]
    networks:
      - webnet
networks:
  webnet:
```

### 技巧总结

#### 查看本地Docker镜像库
```shell
$docker images
```

#### 常用命令
```shell
docker build -t friendlyname .# 使用此目录的 Dockerfile 创建镜像
docker run -p 4000:80 friendlyname  # 运行端口 4000 到 90 的“友好名称”映射
docker run -d -p 4000:80 friendlyname         # 内容相同，但在分离模式下
docker ps                                 # 查看所有正在运行的容器的列表
docker stop <hash>                     # 平稳地停止指定的容器
docker ps -a           # 查看所有容器的列表，甚至包含未运行的容器
docker kill <hash>                   # 强制关闭指定的容器
docker rm <hash>              # 从此机器中删除指定的容器
docker rm $(docker ps -a -q)           # 从此机器中删除所有容器
docker images -a                               # 显示此机器上的所有镜像
docker rmi <imagename>            # 从此机器中删除指定的镜像
docker rmi $(docker images -q)             # 从此机器中删除所有镜像
docker login             # 使用您的 Docker 凭证登录此 CLI 会话
docker tag <image> username/repository:tag  # 标记 <image> 以上传到镜像库
docker push username/repository:tag            # 将已标记的镜像上传到镜像库
docker run username/repository:tag                   # 运行镜像库中的镜像
docker search <key>                     # 搜索docker镜像
```