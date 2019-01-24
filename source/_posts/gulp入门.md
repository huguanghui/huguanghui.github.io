---
title: gulp入门
reward: true
date: 2019-01-14 20:17:54
description:
categories:
tags:
- gulp
---

# gulp入门

## 简介

自动化构建工具

## 使用

1. 全局安装

   ```shell
   $ npm install --global gulp
   ```

   

2. 项目依赖安装

   ```shell
   $ npm install --save-dev gulp
   ```

   

3. 在根目录下创建一个名为gulpfile.js的文件

   ```js
   var gulp = require('gulp');
   
   gulp.task('default', function() {
       // 将默认的任务代码放到这里
   });
   ```

   

4. 运行gulp

```shell
$ gulp
```

