---
title: Linux手册
categories: []
tags:
  - linux
reward: true
originContent: |-
  # Linux手册

  ## 常用链接

  [Linux手册文档](https://linuxtools-rst.readthedocs.io/zh_CN/latest/)

  ## 应用

  ### 查看linux中程序依赖的库

  使用ldd命令查看运行所依赖的库
  ldd + 程序

  ### netstat

  ### xz和tar压缩

  压缩xz格式比7z还要小

  ## 修改Mac地址

  临时
  sudo ifconfig eth0 down
  sudo ifconfig eth0 hw ehter  地址
  sudo ifconfig eth0 up
  永久
  将命令加入 /etc/init.d/rc.local文件中
toc: false
date: 2018-11-02 23:11:33
description:
---

# Linux手册

## 常用链接

[Linux手册文档](https://linuxtools-rst.readthedocs.io/zh_CN/latest/)

## 应用

### 查看linux中程序依赖的库

使用ldd命令查看运行所依赖的库
ldd + 程序

### netstat

### xz和tar压缩

压缩xz格式比7z还要小

## 修改Mac地址

临时
sudo ifconfig eth0 down
sudo ifconfig eth0 hw ehter  地址
sudo ifconfig eth0 up
永久
将命令加入 /etc/init.d/rc.local文件中