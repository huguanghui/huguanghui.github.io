---
title: ubuntu_18.04LST上的使用问题
categories:
  - 操作系统
tags:
  - ubuntu
reward: true
originContent: ''
toc: false
date: 2019-01-25 08:32:38
description:
---

18.04LST上安装google浏览器
     下载google的deb包
      root用户无法使用,可以在运行后添加--non-sandbox选项.

18.04LST上运行sslocal失败

	* 
安装shadowsocks
$ sudo pip install shadowsocks
	* 
配置shadowsocks
{


             "server": "",
             "server_port":,
             "password": "",
             "local_address":"127.0.0.1",
              "timeout":600,
              "method": "aes-256-cfb"  
        }

	* 
 启动shadowsocks
$sudo sslocal -c /etc/shadowsocks.json -d -start

由于在openssl1.1.0版本中,废弃了EVP_CIPHER_CTX_cleanup函数
/usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py文件中将libcrypto.EVP_CIPHER_CTX_cleanup替换成libcrypto.EVP_CIPHER_CTX_reset


     