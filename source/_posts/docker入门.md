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