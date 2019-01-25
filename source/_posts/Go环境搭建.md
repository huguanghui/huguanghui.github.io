---
title: Go环境搭建
categories:
  - Go
tags:
  - Go语言
reward: true
originContent: |-
  [TOC]



  ## 安装

  ## 学习

  2018-12-13号开始学习.

  区块链

  云服务和云存储

  大数据开发

  ### 源码安装Go

  在树莓派上编译Go源码，查看编译完成后占用的大小

  1. 获取源码

  2. 编译源码

     由两个Go的编译工具链,一个是gc,另一个是gccgo.

     Go编译器支持8种指令集.

  3. 运行Demo

  ### linux和Mac环境部署

  go的root包存放目录 /usr/local

  在/etc/profile种添加PATH,GOROOT,GOPATH路径指定

  ```go

  export PATH=$PATH:/usr/loca/go/bin

  export GOROOT=$(go env GOROOT)

  export GOPATH=$(go env GOPATH)

  export PATH=$PATH:$GOPATH/bin

  ```



  ### go之旅

  go官网上的一个Go编程指引功能

  ### 如何去写Go代码

  #### 编译类型

  取消调试信息

  go build -ldflags "-w" prog.go

  go编译器生成的代码包含内联函数调用和注册变量

  在调试的时候需要关掉它们

  go build -gcflags "-N -l"

  ### 编辑器和IDE工具

  LiteIDE

  VSCode

  ### 高效Go

  ### 诊断

  使用gdb调试Go

  ### FAQ

  Go相关的一个共性的问题

  ### 其他资源

  ## 参考文档

  ### 包文档

  以包的形式划分模块.

  ### 命令文档

  #### godoc

  将代码和文档保持一致.

  ### 语法文档

  #### Go的特性

  ##### 切片

  入门:

  切片是对数组的一个升级,每个切片的元素都是不定长的,同时可以插入.

  ##### Map

  Map是一个类型变量的无序集合.

  ##### Interface

  把所有共性的方法定义在一起,任何其他类型只要实现这些方法就是实现这个接口.

  ##### Channel

  用于goroutine上的通信.

  ##### 并发

  goroutine轻量级线程,与内核中的线程不是一个东西.

  goroutine的实现机制值得研究一下.

  ### Go的内存模型

  ### 稳定版本的历史记录

  ## 文章

  ### Go的Blog

  ## 话题
toc: false
date: 2018-12-13 21:53:35
description:
---

[TOC]



## 安装

## 学习

2018-12-13号开始学习.

区块链

云服务和云存储

大数据开发

### 源码安装Go

在树莓派上编译Go源码，查看编译完成后占用的大小

1. 获取源码

2. 编译源码

   由两个Go的编译工具链,一个是gc,另一个是gccgo.

   Go编译器支持8种指令集.

3. 运行Demo

### linux和Mac环境部署

go的root包存放目录 /usr/local

在/etc/profile种添加PATH,GOROOT,GOPATH路径指定

```go

export PATH=$PATH:/usr/loca/go/bin

export GOROOT=$(go env GOROOT)

export GOPATH=$(go env GOPATH)

export PATH=$PATH:$GOPATH/bin

```



### go之旅

go官网上的一个Go编程指引功能

### 如何去写Go代码

#### 编译类型

取消调试信息

go build -ldflags "-w" prog.go

go编译器生成的代码包含内联函数调用和注册变量

在调试的时候需要关掉它们

go build -gcflags "-N -l"

### 编辑器和IDE工具

LiteIDE

VSCode

### 高效Go

### 诊断

使用gdb调试Go

### FAQ

Go相关的一个共性的问题

### 其他资源

## 参考文档

### 包文档

以包的形式划分模块.

### 命令文档

#### godoc

将代码和文档保持一致.

### 语法文档

#### Go的特性

##### 切片

入门:

切片是对数组的一个升级,每个切片的元素都是不定长的,同时可以插入.

##### Map

Map是一个类型变量的无序集合.

##### Interface

把所有共性的方法定义在一起,任何其他类型只要实现这些方法就是实现这个接口.

##### Channel

用于goroutine上的通信.

##### 并发

goroutine轻量级线程,与内核中的线程不是一个东西.

goroutine的实现机制值得研究一下.

### Go的内存模型

### 稳定版本的历史记录

## 文章

### Go的Blog

## 话题