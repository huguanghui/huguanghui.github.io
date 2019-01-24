---
title: zabbix的使用
date: 2018-04-20 06:20:49
categories:
- 环境监控
tags:
- Zabbix
---

[官网][1]
[文档][2]
[中文社区][3]

## 安装
- 分发包安装
- 源码编译
- 容器安装
- 虚拟应用

### 服务端安装

### 部署安装

#### 1.Windows环境
[下载地址](https://www.zabbix.com/downloads/3.4.6/zabbix_agents_3.4.6.win.zip)

- 配置
修改conf/zabbix_agentd.win.conf配置文件
```log
LogFile=c:\zabbix_agentd.log
Server=192.168.0.210
Hostname=f523540
ServerActive=192.168.0.210
```

- 安装agent
```cmd
zabbix_agentd.exe -c E:\zabbix\conf\zabbix_agentd.win.conf -i
```

- 启动agent客户端
```cmd
zabbix_agentd.exe -c E:\zabbix\conf\zabbix_agentd.win.conf -s
```

- 启动agnet客户端

[1]:https://www.zabbix.com/
[2]:https://www.zabbix.com/documentation/3.4/zh/manual
[3]:http://www.zabbix.org.cn/