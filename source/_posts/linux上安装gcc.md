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

## *.cpp->exe

![](.\_linux上安装gcc\buildexe.png)

## 汇编片段

通用寄存器:AX、BX、CX、DX
AX:累加寄存器，BX:基地址寄存器，CX:计数寄存器，DX:数据寄存器

变址寄存器:SI、DI

堆叠、基底暂存器:SP、BP
SP:堆叠指标暂存器，BP:基底指标暂存器  

E前缀表示32位系统

esp: 寄存器存放当前线程的栈顶指针

ebp:寄存器存放当前线程的栈底指针

eip:下一个CPU指令的存放位置

ebx: $?的返回

![](.\_linux上安装gcc\寻址方式.png)

### mov

寄存器赋值

b,w,l,q代表8位,16位,32位,64位

### push

入栈指令

push %eax

subl $4,%esp

movl %eax	,(%esp)

### pop

出栈指令

popl %eax

movl (%esp), %eax

addl $4,%esp

### leave

相当于mov+pop

### call

call 0x12345

push %eip*

movl 0x12345,%eip* 

### ret

popl %eip*

### enter

pushl %ebp

movl %esp,%ebp

### leave

movl %ebp,%esp

popl %ebp

## objdump二进制文件分析

### 查看当前系统是大端模式或小端模式

```shell
$objdump -i
```

### 反汇编

```shell
$objdump -S main
# 或
$objdump -d main
```

### 显示符号表入口

```shell
$objdump -t main
```

## readelf elf文件格式分析

```shell
$readelf -S a.out
```

0x0000 5555 5555 4610