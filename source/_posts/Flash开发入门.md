---
title: Flash开发入门
date: 2018-05-18 18:02:18
categories: 插件
tags: flash
---

## 链接
- [资源汇总](https://www.cnblogs.com/wanghe/archive/2013/01/26/2877748.html)
- [将Flash嵌入到WPF程序中](http://www.cnblogs.com/gnielee/archive/2010/07/27/wpf-flash-activex.html)
- [Flash AS3.0 socket编程](http://www.cnblogs.com/Longbin/articles/1929771.html)
- [AS3类库资源集合](http://www.cnblogs.com/top5/archive/2009/08/01/1536625.html)

## 环境搭建

### 实现多实例
- Echo > .multi

## 多工程的使用
### 命令编译
"$(CompilerPath)\bin\compc.exe" -include-sources "$(ProjectDir)\src" -output "$(OutputDir)\$(OutputName)"

### 链接库
-include-libraries

LibA库 中ClaA
LibB库 中ClaB