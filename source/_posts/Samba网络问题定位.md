---
title: Samba网络问题定位
reward: true
date: 2018-12-25 20:34:43
description:
categories:
tags:
  - bug
---

## 现象描述

ubuntu18.04在使用docker和docker-machine后出现了多个网卡,win10上的samba客户端连接不上.

## 问题定位

### 通讯流程跟踪

#### win10客户端上的抓包

![](C:\Users\29366\Documents\GIT\huguanghui.github.io\source\_posts\_Samba网络问题定位\smbd01.png)

分析:

服务器返回Destination unreachable

#### ubuntu服务器抓包

tcpdump实时抓包分析,接收有打印.

### 协议对比

根据抓包分析,应该还没有到smb交互协议部分.

### 结论

通过对之前的操作进行分析,是安装了firewalld软件导致.卸载firewalld之后通讯流程就正常了.