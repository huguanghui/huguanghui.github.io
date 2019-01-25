---
title: webpack打包后的调试技巧
categories:
  - 前端
tags:
  - 工具
reward: true
originContent: |-
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
toc: false
date: 2018-05-17 06:33:00
description:
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