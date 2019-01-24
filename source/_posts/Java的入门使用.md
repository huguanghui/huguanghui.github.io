---
title: Java的入门使用
date: 2018-04-18 00:43:42
categories:
- Java
tags:
- Java入门
---

## Java中的命令

### javac
&emsp;将*.java文件编译成*.class文件.


### java
&emsp;运行*.class文件

### javap
&emsp;帮助开发者了解java的编译机制

## 第一个工程

### Hello World!
```java
/*hello.java*/
public class hello {
	public static void main(String []args) {
		System.out.println("Hello World");
	}
}
```
```cmd
$javac -d . .\hello.java
$java hello
```


