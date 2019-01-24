---
title: Java环境搭建
date: 2018-04-18 00:07:35
categories:
- Java
tags:
- Java环境
---

## JDK下载
[Java的JDK安装包](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

### 设置三项系统变量
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
