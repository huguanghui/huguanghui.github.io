---
title: Strace使用
categories:
  - Linux
  - 调试
tags:
  - 系统调用跟踪
reward: true
originContent: >-
  @[TOC]


  ---


  # Strace的使用

  [Strace诊断](https://huoding.com/2015/10/16/474)


  命令

  strace -p <PID>

  strace -cp <PID>


  strace用于追踪系统调用和信号量.在调试时，strace是一个可以采集上下文的实用工具.

  1.strace PTRACE_TRACEME EPERM (Operation not permitted)

  你应该以root权限运行strace，如果你收到这条消息，这意味着在你当前系统上不允许绑定进程.

  解决办法:

  1.sudo bash -c 'echo 0 > /proc/sys/kernel/yama/ptrace_scope'

  2.检查文件/etc/sysctl.d/10-ptrace.conf,将其权限改为可读

  3.kernel.yama.ptrace_scope = 0

  如果没有那个文件

  打开/etc/sysctl/conf，查找设置kernrl.yama.ptrace_scope
  存在将其值设为0，如果不支持添加一行kernel.yama.ptrace_scope = 0


  ---

  ### 追踪线程PID

  - 追踪进程

  $ strace -p [pid]

  - 追踪进程和线程

  $ strace -fp [pid]

  - 追踪进程和限定字符

  $ strace -s 80 -fp [pid]


  ### 追踪程序

  $ strace ./program

  $ strace -f ./program

  $ strace -s 80 -f ./program


  ### 过滤futex调用

  1.只是过滤futex

  $ strace -Tf ./program 2>&1 | grep -v futex

  2.过滤多个系统调用

  $ strace -Tfe strace=open,read,write ./program


  ### 其他实用选项

  -f 线程号

  -T 添加打印时间

  -t 打印时间

  -s [size] 指定显示长度

  -e strace=open,close 只追踪open和close系统调用.


  ### linux平台编译strace源码.

  1.下载strace-4.19.tar.xz

  2.解压，对于ARM平台，需要打补丁,暂时没有遇见过

  3.配置 ./configure --host=arm-linux CC=arm_v5t_le-gcc LD=arm_v5t_le-ld

  4.编译 make CFLAGS+="-static"

  5.strip arm_v5t_le-strip 
toc: false
date: 2019-01-25 07:58:52
description:
---

@[TOC]

---

# Strace的使用
[Strace诊断](https://huoding.com/2015/10/16/474)

命令
strace -p <PID>
strace -cp <PID>

strace用于追踪系统调用和信号量.在调试时，strace是一个可以采集上下文的实用工具.
1.strace PTRACE_TRACEME EPERM (Operation not permitted)
你应该以root权限运行strace，如果你收到这条消息，这意味着在你当前系统上不允许绑定进程.
解决办法:
1.sudo bash -c 'echo 0 > /proc/sys/kernel/yama/ptrace_scope'
2.检查文件/etc/sysctl.d/10-ptrace.conf,将其权限改为可读
3.kernel.yama.ptrace_scope = 0
如果没有那个文件
打开/etc/sysctl/conf，查找设置kernrl.yama.ptrace_scope 存在将其值设为0，如果不支持添加一行kernel.yama.ptrace_scope = 0

---
### 追踪线程PID
- 追踪进程
$ strace -p [pid]
- 追踪进程和线程
$ strace -fp [pid]
- 追踪进程和限定字符
$ strace -s 80 -fp [pid]

### 追踪程序
$ strace ./program
$ strace -f ./program
$ strace -s 80 -f ./program

### 过滤futex调用
1.只是过滤futex
$ strace -Tf ./program 2>&1 | grep -v futex
2.过滤多个系统调用
$ strace -Tfe strace=open,read,write ./program

### 其他实用选项
-f 线程号
-T 添加打印时间
-t 打印时间
-s [size] 指定显示长度
-e strace=open,close 只追踪open和close系统调用.

### linux平台编译strace源码.
1.下载strace-4.19.tar.xz
2.解压，对于ARM平台，需要打补丁,暂时没有遇见过
3.配置 ./configure --host=arm-linux CC=arm_v5t_le-gcc LD=arm_v5t_le-ld
4.编译 make CFLAGS+="-static"
5.strip arm_v5t_le-strip 