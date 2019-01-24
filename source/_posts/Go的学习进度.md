---
title: Go的学习进度
reward: true
date: 2018-12-19 22:30:09
description:
categories:
tags:
- Go
---

# Go的学习进度

## Go的整体计划

项目目标: 实现一个简易的RTSP服务器
每日计划: 对一个开源代码的一段进行分析

## 2018/12/19

RTSP服务器:
实现了一个最简单的服务监听功能,能监听554端口,发送消息和响应消息

代码分析:(net中的tcpsock.go)

```go
func ListenTCP(network string, laddr *TCPAddr) (*TCPListener, error) {
	switch network {
	case "tcp", "tcp4", "tcp6":
	default:
		return nil, &OpError{Op: "listen", Net: network, Source: nil, Addr: laddr.opAddr(), Err: UnknownNetworkError(network)}
	}
	if laddr == nil {
		laddr = &TCPAddr{}
	}
	sl := &sysListener{network: network, address: laddr.String()}
	ln, err := sl.listenTCP(context.Background(), laddr)
	if err != nil {
		return nil, &OpError{Op: "listen", Net: network, Source: nil, Addr: laddr.opAddr(), Err: err}
	}
	return ln, nil
}
```

解析:

这是net中TCP监听的一段代码.

1.参数检测,network必须为"tcp","tcp4","tcp6"中的一种; laddr转换

2.进行监听,失败返回对于的错误信息.

问题点: &OpError, &TCPAddr{}和 &sysListener的使用

​	     return 多个参数, 直接在函数定义的地方**指定返回类型**就可以了

增加：

2018-12-21：

&sysListener是Go语言中获取地址变量的一个技巧(问题: 实现了深拷贝,浅拷贝还是其他的方式)

&OpError按自己定义错误的一种使用方式(定义一个错误对象,实现错误的Error()方法)

对于错误的处理,尽量就立即返回

## 2018/12/20

RTSP服务器:

更改结构将rtsp服务功能包化

代码分析:(net/http/header.go)

主要用于http的header头解析和时间格式的解析

```go
func hasToken(v, token string) bool {
	if len(token) > len(v) || token == "" {
		return false
	}
	if v == token {
		return true
	}
	for sp := 0; sp <= len(v)-len(token); sp++ {
		// Check that first character is good.
		// The token is ASCII, so checking only a single byte
		// is sufficient. We skip this potential starting
		// position if both the first byte and its potential
		// ASCII uppercase equivalent (b|0x20) don't match.
		// False positives ('^' => '~') are caught by EqualFold.
		if b := v[sp]; b != token[0] && b|0x20 != token[0] {
			continue
		}
		// Check that start pos is on a valid token boundary.
		if sp > 0 && !isTokenBoundary(v[sp-1]) {
			continue
		}
		// Check that end pos is on a valid token boundary.
		if endPos := sp + len(token); endPos != len(v) && !isTokenBoundary(v[endPos]) {
			continue
		}
		if strings.EqualFold(v[sp:sp+len(token)], token) {
			return true
		}
	}
	return false
}
```

功能描述: 查看v字符串中是不是包含token.

## 2018/12/21

RTSP服务器:

参照http模块处理http请求的流程处理RTSP的处理

代码分析:

```go
type onceCloseListener struct {
	net.Listener   //隐式声明
	once     sync.Once
	closeErr error
}
```

梳理http的框架结构

## 2018/12/23

net/http中的ServeMux结构是一个http服务端对请求的URI做处理的一个多路复用器.

