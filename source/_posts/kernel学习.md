---
title: kernel学习
reward: true
date: 2018-12-12 12:19:14
description:
categories:
tags:
- linux
---



## 简介
[git仓库](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/)

[github仓库](https://github.com/torvalds/linux)

[文档](https://www.kernel.org/doc/html/latest/)

[wikis](https://www.wiki.kernel.org/)

## 编译

通过git获取源代码

查看当前系统的内核配置文件

```shell
/boot/config-$(uname -r)
```

|     名称     |            解释            |
| :----------: | :------------------------: |
|  defconfig   |          默认配置          |
| allnoconfig  |    尽可能多的选项都关闭    |
| allyesconfig |    尽可能多的选项都开启    |
| allmodconfig | 尽可能多的选项作为模块启动 |

```shell
$make ARCH=arm64 defconfig
$make -j8
```

编译出错

```shell
kernel/built-in.o：在函数‘update_wall_time’中：
(.text+0x293ee)：对‘____ilog2_NaN’未定义的引用
Makefile:949: recipe for target 'vmlinux' failed
make: *** [vmlinux] Error 1
```

处理方法:

[补丁包处理](https://blog.csdn.net/wlj1012/article/details/81626669)

## 构建虚拟内存盘(initrd)

### busybox

[官网](https://busybox.net/)



### 目录部署

## 前期准备

#### 汇编整理

```
$gcc –S –o main.s main.c -m32
```

### 最简易根文件系统镜像

[github](https://github.com/mengning/menu)

find . | cpio -o -Hnewc |gzip -9 > ../rootfs.img

## 内核运行

使用gdb调试

```shell
$gdb -q
$> file linux_*/vmlinux
$> target remote:1234
$> break start_kernel
```



## 相关资料

[linux-insides](https://0xax.gitbooks.io/linux-insides/content/index.html)

[中文翻译](https://xinqiu.gitbooks.io/linux-insides-cn/content/CONTRIBUTORS.html)

