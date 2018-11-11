---
title: CMake的使用
reward: true
date: 2018-11-08 23:53:32
description:
categories:
tags:
- CMake
---

# CMake

## 链接

[官网](https://cmake.org/)
[CMake入门实践](http://www.hahack.com/codes/cmake/)
[实践](https://www.kancloud.cn/itfanr/cmake-practice/82988)
[选项](https://zh.wikibooks.org/zh-hans/CMake_%E5%85%A5%E9%96%80/%E5%8A%A0%E5%85%A5%E7%B7%A8%E8%AD%AF%E9%81%B8%E9%A0%85)

## 使用

### 动态库编译

add_library(hgh_base SHARED ${base_SRCS})
target_link_libraries(hgh_base pthread rt)

### 静态库编译

add_library(hgh_base ${base_SRCS})
target_link_libraries(hgh_base pthread rt)

### 动态库和静态库同时编译

set_target_properties(hgh_base_static PROPERTIES OUTPUT_NAME "hgh_base")

### 可执行编译