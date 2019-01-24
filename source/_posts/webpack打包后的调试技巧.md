---
title: webpack打包后的调试技巧
date: 2018-05-17 06:33:00
categories: Node
tags: 调试
---

### 简介
使用webpack后很多代码被打包在一起,不方便调试.webpack提供了source map来解决这个问题.
本文就分析webpack使用source map来调试代码的流程.

---
### 配置
- devtool
 - source-map
 - cheap-module-source-map
 - eval-source-map
 - cheap-module-eval-source-map
 从上到下打包速度越来越快,负面作用越来越多
