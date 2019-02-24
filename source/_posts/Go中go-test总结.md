---
title: Go中go test总结
categories:
  - Go
tags:
  - Go语言
reward: true
originContent: ''
toc: false
date: 2019-02-04 15:39:08
description:
---

# Go测试

## 依赖Go的规则

在Go工程中,以_或者.符号作为文件名的首字母时,会被构建工具忽略.
go工具会忽略testdata目录,使其可以保存所需的辅助数据.
使用testing包

## 分类

分为三类:
- 测试函数
    测试程序的一些接口是否正确
- 基准测试函数
    衡量接口的性能
- 例子函数
    函数使用

## go test参数