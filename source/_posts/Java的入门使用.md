---
title: Java的入门使用
categories:
  - Java
tags:
  - Java
reward: true
originContent: "## Java中的命令\n\n### javac\n&emsp;将*.java文件编译成*.class文件.\n\n\n### java\n&emsp;运行*.class文件\n\n### javap\n&emsp;帮助开发者了解java的编译机制\n\n## 第一个工程\n\n### Hello World!\n```java\n/*hello.java*/\npublic class hello {\n\tpublic static void main(String []args) {\n\t\tSystem.out.println(\"Hello World\");\n\t}\n}\n```\n```cmd\n$javac -d . .\\hello.java\n$java hello\n```"
toc: false
date: 2018-04-18 00:43:42
description:
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