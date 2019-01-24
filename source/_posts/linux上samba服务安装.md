---
title: linux上samba服务安装
reward: true
date: 2018-11-11 09:47:55
description:
categories:
- samba
tags:
- 软件
---
[TOC]

---

## samba安装
apt-get install samba

## samba配置修改(/etc/samba/)
[linux]
path=/home/linux
valid users=linux
public=yes
writable=yes

## 重启samba服务
    service smbd restart

## 创建samba用户
    smbpasswd -a root