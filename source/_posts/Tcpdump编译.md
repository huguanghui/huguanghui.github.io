---
title: Tcpdump编译
categories:
  - linux
tags:
  - 工具
reward: true
originContent: "@[toc]\n---\n\n# Tcpdump交叉编译\n\nlibpcap包和tcpdump包\n\n## 编译libpcap包\n\n1.解压\n\n```shell\n    tar -zxvf libpcap-1.4.0.tar.gz\n```\n\n2.配置生产makefile\n\n\t$./configure --host=arm-linux CC=arm-none-linux-gnueabi-gcc --with-pcap=linux\n\n3.编译\n    make\n\n## 编译tcpdump包\n\n1.解压\n    tar -zxvf tcpdump-4.4.0.tar.gz\n2.配置生成makefile\n\n\t$./configure --host=arm-linux CC=arm-none-linux-gnueabi-gcc --prefix=/root/tcpdump_tool\n\n3.编译\n    make\n\n./configure时会自动查找到libpcap.a库\n\n参数使用技巧后续再使用"
toc: false
date: 2019-01-25 07:34:40
description:
---

@[toc]
---

# Tcpdump交叉编译

libpcap包和tcpdump包

## 编译libpcap包

1.解压

```shell
    tar -zxvf libpcap-1.4.0.tar.gz
```

2.配置生产makefile

```shell
$./configure --host=arm-linux CC=arm-none-linux-gnueabi-gcc --with-pcap=linux
```

3.编译

```shell
$make
```

## 编译tcpdump包

1.解压

```shell
tar -zxvf tcpdump-4.4.0.tar.gz
```

2.配置生成makefile

```shell
$./configure --host=arm-linux CC=arm-none-linux-gnueabi-gcc --prefix=/root/tcpdump_tool
```

3.编译

```shell
make
```

./configure时会自动查找到libpcap.a库

参数使用技巧后续再使用