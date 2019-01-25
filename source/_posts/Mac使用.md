---
title: Mac使用
categories:
  - 操作系统
tags:
  - 软件
reward: true
originContent: >-
  @[TOC]


  ---


  ## Dash


  [官网]()


  ## Mounty


  ## iTerm2


  ## sock5代理


  ```shell

  $brew install shadowsocks-libev

  ```


  配置代理服务器配置

  /usr/local/etc/shadowsocks-libev.json


  设置开机启动

  ln -s /usr/local/opt/shadowsocks-libev/homebrew.mxcl.shadowsocks-libev.plist
  ~/Library/LaunchAgents/homebrew.mxcl.shadowsocks-libev.plist


  加载配置文件

  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.shadowsocks-libev.plist


  使用privoxy来实现shadowsocks向http代理

  brew install privoxy
toc: false
date: 2019-01-25 08:28:16
description:
---

@[TOC]

---

## Dash

[官网]()

## Mounty

## iTerm2

## sock5代理

```shell
$brew install shadowsocks-libev
```

配置代理服务器配置
/usr/local/etc/shadowsocks-libev.json

设置开机启动
ln -s /usr/local/opt/shadowsocks-libev/homebrew.mxcl.shadowsocks-libev.plist ~/Library/LaunchAgents/homebrew.mxcl.shadowsocks-libev.plist

加载配置文件
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.shadowsocks-libev.plist

使用privoxy来实现shadowsocks向http代理
brew install privoxy