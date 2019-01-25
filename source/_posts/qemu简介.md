---
title: qemu简介
categories:
  - 调试
tags:
  - 工具
reward: true
originContent: |-
  ## 简介

  qemu是一个通用和开源的机器仿真器和虚拟器.

  三种使用:

  Full-system emulation 可以在所有支持的架构的机器上运行操作系统

  User-mode emulation 在所有支持的架构上运行Linux/BSD程序

  Virtualization 运行接近本机性能的KVM和Xen虚拟机

  [git仓库](https://git.qemu.org/git/qemu.git/)

  [wiki](https://wiki.qemu.org/Main_Page)

  ## 源码安装

  ```shell
  $git clone https://git.qemu.org/git/qemu.git
  $cd qemu
  $git submodule init
  $git submodule update --recursive
  $./configure
  $make
  $sudo make install
  ```



  安装过程中遇到的问题:

  1.glib缺少

  sudo apt-get install libglib2.0-dev

  2.ERROR: pixman >= 0.21.8 not present.
  ​       Please install the pixman devel package.

  解决办法:

  apt-cache search pixman

  sudo apt install libpixman-1-dev

  ## 系统仿真

  只出现VNC server running on 127.0.0.1:5901

  原因是缺少libsdl开发库

  ```shell
  $sudo apt-get install libsdl2-dev
  ```
toc: false
date: 2018-12-23 09:34:02
description:
---

## 简介

qemu是一个通用和开源的机器仿真器和虚拟器.

三种使用:

Full-system emulation 可以在所有支持的架构的机器上运行操作系统

User-mode emulation 在所有支持的架构上运行Linux/BSD程序

Virtualization 运行接近本机性能的KVM和Xen虚拟机

[git仓库](https://git.qemu.org/git/qemu.git/)

[wiki](https://wiki.qemu.org/Main_Page)

## 源码安装

```shell
$git clone https://git.qemu.org/git/qemu.git
$cd qemu
$git submodule init
$git submodule update --recursive
$./configure
$make
$sudo make install
```



安装过程中遇到的问题:

1.glib缺少

sudo apt-get install libglib2.0-dev

2.ERROR: pixman >= 0.21.8 not present.
​       Please install the pixman devel package.

解决办法:

apt-cache search pixman

sudo apt install libpixman-1-dev

## 系统仿真

只出现VNC server running on 127.0.0.1:5901

原因是缺少libsdl开发库

```shell
$sudo apt-get install libsdl2-dev
```