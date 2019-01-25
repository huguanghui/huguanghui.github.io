---
title: Java环境搭建
categories:
  - Java
tags:
  - Java环境
reward: true
originContent: "## JDK下载\n[Java的JDK安装包](http://www.oracle.com/technetwork/java/javase/downloads/index.html)\n\n## 配置环境变量\n右键\"计算机\"--属性--高级系统设置-高级\n* JAVA_HOME\n\t* value: java的安装目录\\jdk1.8.0_91\n* CLASSPATH\n\t* value: %JAVA_HOME%\\lib\\dt.jar;%JAVA_HOME%\\lib\\tools.jar;\n* Path\n\t* vaule: %JAVA_HOME%\\bin;%JAVA_HOME%\\jre\\bin;\n\n注意: Win10中由于系统的限制,Path中的路径只能用绝对路径.\n\n<!--more-->\n\n### 检测安装成功\n\n```cmd\njava -version\njava\njavac\n```\n\n### 安装eclipse\n\n[下载](http://www.eclipse.org/downloads/)"
toc: false
date: 2018-04-18 00:07:35
description:
---

## JDK下载
[Java的JDK安装包](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

## 配置环境变量
右键"计算机"--属性--高级系统设置-高级
* JAVA_HOME
	* value: java的安装目录\jdk1.8.0_91
* CLASSPATH
	* value: %JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
* Path
	* vaule: %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

注意: Win10中由于系统的限制,Path中的路径只能用绝对路径.

<!--more-->

### 检测安装成功

```cmd
java -version
java
javac
```

### 安装eclipse

[下载](http://www.eclipse.org/downloads/)