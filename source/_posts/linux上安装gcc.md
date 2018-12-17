---
title: linux上安装gcc
reward: true
date: 2018-12-01 10:05:27
description:
categories:
tags:
- linux
---

# linux上 安装gcc

## 简介

### [官网](https://gcc.gnu.org/)

### 部署环境

win10微软商店中的ubuntu18.04

### gcc的历史版本

|  版本   | 简介 |
| :-----: | :--: |
| GCC 5.5 |      |
| GCC 6.4 |      |
| GCC 6.5 |      |
| GCC 7.2 |      |
| GCC 7.3 |      |
| GCC 8.1 |      |
| GCC 8.2 |      |
| GCC 9.0 |      |

## 编译安装GCC 7.3

### 下载

```shell
$wget ftp://ftp.gwdg.de/pub/misc/gcc/releases/gcc-7.3.0/gcc-7.3.0.tar.xz
```

### 解压

```shell
$xz -d gcc-7.3.0.tar.xz
$tar -xvf gcc-7.3.0.tar
```

下载,配置,安装需要的依赖库

```shell
$./contrib/download_prerequisites
$mkdir gcc-build-7.3.0 // 建立编译输出目录
$../configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
$make
$卸载 旧版本gcc和g++
$sudo make install
```

