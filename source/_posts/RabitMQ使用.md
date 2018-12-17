---
title: RabitMQ使用
reward: true
date: 2018-11-18 20:16:45
description:
categories:
tags:
- RabbitMQ
---

# RabbitMQ

## 链接

[官网](http://www.rabbitmq.com/)

## ubuntu上安装RabbitMQ

1. 将RabbitMQ signing key添加到apt-key中

```shell
$apt-key adv --keyserver "hkps.pool.sks-keyservers.net" --recv-keys "0x6B73A36E6026DFCA"
$wget -O - "https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc" | sudo apt-key add -
```

2. 添加到sources.list.d中

```shell
$echo "deb https://dl.bintray.com/rabbitmq/debian bionic main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
```
---

## 插件

### rabbitmq-management

该插件提供基于HTTP的API,用于管理和监控RabbitMQ的节点和集群,以及基于浏览器的UI和命令行工具rabbitmqadmin.
它定期收集和汇总有关系统许多方面的数据.这些指标在UI和监控系统中向所有操作员公开,用于长期存储,警报,可视化和图表分析.

#### 入门

该插件已经包含在RabbitMQ的发行版本中.

```shell
$rabbitmq-plugins enable rabbitmq_management
```

---

## 配置

RabbitMQ带有默认的内置配置.在一些环境下已经完全够用.在一些部署调整的环境下,还有一种代理和插件配置的方法.

### 用户管理

#### 创建用户

```shell
$rabbitmqctl add_user root 123789
```

#### 设置权限

```shell
$rabbitmqctl set_user_tags root administrator
```

#### 查看用户列表

```shell
$rabbitmqctl list_users
```

#### 删除用户

```shell
$rabbitmqctl delete_user root
```

#### 修改用户密码

```shell
$rabbitmqctl change_password admin 123789hgh
```

### 为用户赋权

```shell
$rabbitmqctl list_user_permissions root
$rabbitmqctl list_permissions -p vhost1
$rabbitmqctl clear_permissions -p vhost1 root
$rabbtimqctl set_permissions -p vhost1 root '.*' '.*' '.*'
```

---

## 编程语言支持

### C/C++

[RabbitMQ C client](https://github.com/alanxz/rabbitmq-c)
[SimpleAmqpClient](https://github.com/alanxz/SimpleAmqpClient)
[amqpcpp](https://github.com/akalend/amqpcpp)
[AMPQ-CPP](https://github.com/CopernicaMarketingSoftware/AMQP-CPP)