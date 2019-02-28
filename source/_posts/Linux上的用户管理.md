---
title: Linux上的用户管理
categories:
  - 操作系统
tags:
  - 项目管理
reward: true
originContent: |-
  # Linux上的用户管理
  > 在开发过程中经常会出现人员的流动.为了保证数据安全性和环境的稳定性,需要为新加入成员添加账号,在人员离开时也要进行账号的销毁.

  ## 相关概念

  用户组:

  用户:

  ## 查看用户和用户组

  ```shell
  # 查看系统所有用户组
  $cat /etc/group
  # 查看系统所有用户
  $cat /etc/shadow
  ```

  ## 新建用户

  ```shell
  $useradd username -d /home/username -g usergroup
  $passwd username //密码
  $gpasswd -a username usergroup
  ```

  ## 删除用户

  ```shell
  $userdel username
  ```

  ## useradd和adduser的区别
  > CentOS下两个命令没有区别,在Ubuntu系统下useradd添加用户不会自动设置用户目录和shell版本,userdel和deluser类似.
toc: false
date: 2019-02-28 01:00:25
description:
---

# Linux上的用户管理
> 在开发过程中经常会出现人员的流动.为了保证数据安全性和环境的稳定性,需要为新加入成员添加账号,在人员离开时也要进行账号的销毁.

## 相关概念

用户组:

用户:

## 查看用户和用户组

```shell
# 查看系统所有用户组
$cat /etc/group
# 查看系统所有用户
$cat /etc/shadow
```

## 新建用户

```shell
$useradd username -d /home/username -g usergroup
$passwd username //密码
$gpasswd -a username usergroup
```

## 删除用户

```shell
$userdel username
```

## useradd和adduser的区别
> CentOS下两个命令没有区别,在Ubuntu系统下useradd添加用户不会自动设置用户目录和shell版本,userdel和deluser类似.