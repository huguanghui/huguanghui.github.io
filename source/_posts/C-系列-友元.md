---
title: C++系列_友元
reward: true
date: 2018-11-30 22:25:37
description:
categories:
tags:
- friend declaration1.
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

