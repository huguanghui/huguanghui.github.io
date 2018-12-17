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

### 基础的开始设置

```cmake
cmake_minimum_required(VERSION 2.6)
project(cplusplus_common)
```

### 设置编译器和编译参数

```cmake
set(CXX_FLAGS
-g
-Wall
-rdynamic
)
set(CMAKE_CXX_COMPILER "g++")
# 显示编译过程参数
set(CMAKE_VERBOSE_MAKEFILE OFF)
```

### 动态库编译

add_library(hgh_base SHARED ${base_SRCS})
target_link_libraries(hgh_base pthread rt)

### 静态库编译

add_library(hgh_base ${base_SRCS})
target_link_libraries(hgh_base pthread rt)

### 动态库和静态库同时编译

set_target_properties(hgh_base_static PROPERTIES OUTPUT_NAME "hgh_base")

### 可执行编译

```cmake
add_executable(test SRC_LIST)
```

### 指定可执行程序的输出目录

```cmake
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
```

## 扩展

### 使用build.sh脚本独立编译环境

```shell
#!/bin/sh

set -x

SOURCE_DIR=`pwd`
BUILD_DIR=${BUILD_DIR:-../build}
BUILD_TYPE=${BUILD_TYPE:-debug}
INSTALL_DIR=${INSTALL_DIR:-../${BUILD_TYPE}-install}

mkdir -p $BUILD_DIR/$BUILD_TYPE \
    && cd $BUILD_DIR/$BUILD_TYPE \
    && cmake \
        -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
        -DCMAKE_INSTALL_PREFIX=$INSTALL_DIR \
        $SOURCE_DIR \
    && make $*

```

