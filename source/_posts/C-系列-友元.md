---
title: C++系列_友元
categories:
  - CPlusPlus
tags:
  - c++
reward: true
originContent: "# C++系列_友元\n\n## 简介\n\n友元声明是在类的结构中.确保函数或者其他类有访问声明有元类中的私有和保护类的\n\n## 语法\n\nfriend function-deciaration\n\nfriend function-definition\n\nfriend elaborated-class-specifier\n\nfriend simple-type-specifier\n\nfriend typename-specifier\n\n## 描述\n\n### 1.指定一个或几个函数作为类的友元\n\n```c++\nclass Y {\n\tint data;\n    friend std::ostream& operator<<(std::ostream& out, const Y& o);\n    friend char* X::foo(int);\n    friend X::X(char), X::~X();\n};\nstd::ostream& operator<<(std::ostream& out, const Y& y)\n{\n    return out << y.data;\n}\n```\n\n2.(在非本地类定义)定义一个非成员函数,同时也让它成为这个类的友元.像这样的非成员函数也是inline方式.\n\n```c++\nclass X {\n    int a;\n    friend void friend_set(X& p, int i) {\n        p.a = i;\n    }\npublic:\n    void member_set(int i) {\n        a = i;\n    }\n};\n```"
toc: false
date: 2018-11-30 22:25:37
description:
---

# C++系列_友元

## 简介

友元声明是在类的结构中.确保函数或者其他类有访问声明有元类中的私有和保护类的

## 语法

friend function-deciaration

friend function-definition

friend elaborated-class-specifier

friend simple-type-specifier

friend typename-specifier

## 描述

### 1.指定一个或几个函数作为类的友元

```c++
class Y {
	int data;
    friend std::ostream& operator<<(std::ostream& out, const Y& o);
    friend char* X::foo(int);
    friend X::X(char), X::~X();
};
std::ostream& operator<<(std::ostream& out, const Y& y)
{
    return out << y.data;
}
```

2.(在非本地类定义)定义一个非成员函数,同时也让它成为这个类的友元.像这样的非成员函数也是inline方式.

```c++
class X {
    int a;
    friend void friend_set(X& p, int i) {
        p.a = i;
    }
public:
    void member_set(int i) {
        a = i;
    }
};
```