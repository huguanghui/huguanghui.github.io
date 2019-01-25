---
title: LNMP环境
categories:
  - 操作系统
tags:
  - 项目管理
reward: true
originContent: >-
  ## 简介

  - LNMP(Linux Nginx Mysql PHP)

  ```shell

  sudo apt-get update

  sudo apt-get install nginx php5-fpm php5-cli php5-curl php5-gd php5-mcrypt
  php5-mysql php5-cgi mysql-server

  ```


  *树莓派中搭建的问题*

  在安装php5-fpm出现无法定位到安装包的问题

  修改apt的镜像源 (浙江大学镜像源地址)

  deb http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib non-free
  rpi

  deb-src http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib
  non-free rpi


  关于下载mysql-server依赖项的问题解决使用清华的镜像

  deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main
  contrib non-free



  ## Mysql

  --- 

  ### 简介

  Mysql是一个关系型数据库,由瑞典MySQL AB公司开发,目前属于Oracle旗下公司.

  MySQL最流行的关系数据库管理系统.


  ### 安装

  ```shell

  $sudo apt-get install mysql-server

  $sudo apt-get install mysql-client

  $sudo apt-get install libmysqlclient-dev

  ```


  ## PHP

  ---

  PHP5.6.36

  ```shell

  $./configure  --prefix=/usr/local/php-5.5.7 \

  --with-config-file-path=/usr/local/php-5.5.7/etc --with-bz2 --with-curl \

  --enable-ftp --enable-sockets --disable-ipv6 --with-gd \

  --with-jpeg-dir=/usr/local --with-png-dir=/usr/local \

  --with-freetype-dir=/usr/local --enable-gd-native-ttf \

  --with-iconv-dir=/usr/local --enable-mbstring --enable-calendar \

  --with-gettext --with-libxml-dir=/usr/local --with-zlib \

  --with-pdo-mysql=mysqlnd --with-mysqli=mysqlnd --with-mysql=mysqlnd \

  --enable-dom --enable-xml --enable-fpm --with-libdir=lib64 --enable-bcmath


  $apt-get install libxml2

  $apt-get install libxml2-dev

  $apt-get install libbz2-dev

  $apt-get install curl

  $apt-get install libcurl4-gnutls-dev

  ```


  ## 链接

  [nginx+php5.0安装][1]

  [zabbix环境](http://www.ttlsa.com/zabbix/install-zabbix-on-linux-5-ttlsa/)

  [ubuntu源码安装php的常见错误解决办法](https://blog.csdn.net/white__cat/article/details/28907535)


  [1]:https://www.cnblogs.com/kevingrace/p/6212005.html
toc: false
date: 2018-04-24 21:39:29
description:
---

## 简介
- LNMP(Linux Nginx Mysql PHP)
```shell
sudo apt-get update
sudo apt-get install nginx php5-fpm php5-cli php5-curl php5-gd php5-mcrypt php5-mysql php5-cgi mysql-server
```

*树莓派中搭建的问题*
在安装php5-fpm出现无法定位到安装包的问题
修改apt的镜像源 (浙江大学镜像源地址)
deb http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi
deb-src http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi

关于下载mysql-server依赖项的问题解决使用清华的镜像
deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ stretch main contrib non-free


## Mysql
--- 
### 简介
Mysql是一个关系型数据库,由瑞典MySQL AB公司开发,目前属于Oracle旗下公司.
MySQL最流行的关系数据库管理系统.

### 安装
```shell
$sudo apt-get install mysql-server
$sudo apt-get install mysql-client
$sudo apt-get install libmysqlclient-dev
```

## PHP
---
PHP5.6.36
```shell
$./configure  --prefix=/usr/local/php-5.5.7 \
--with-config-file-path=/usr/local/php-5.5.7/etc --with-bz2 --with-curl \
--enable-ftp --enable-sockets --disable-ipv6 --with-gd \
--with-jpeg-dir=/usr/local --with-png-dir=/usr/local \
--with-freetype-dir=/usr/local --enable-gd-native-ttf \
--with-iconv-dir=/usr/local --enable-mbstring --enable-calendar \
--with-gettext --with-libxml-dir=/usr/local --with-zlib \
--with-pdo-mysql=mysqlnd --with-mysqli=mysqlnd --with-mysql=mysqlnd \
--enable-dom --enable-xml --enable-fpm --with-libdir=lib64 --enable-bcmath

$apt-get install libxml2
$apt-get install libxml2-dev
$apt-get install libbz2-dev
$apt-get install curl
$apt-get install libcurl4-gnutls-dev
```

## 链接
[nginx+php5.0安装][1]
[zabbix环境](http://www.ttlsa.com/zabbix/install-zabbix-on-linux-5-ttlsa/)
[ubuntu源码安装php的常见错误解决办法](https://blog.csdn.net/white__cat/article/details/28907535)

[1]:https://www.cnblogs.com/kevingrace/p/6212005.html