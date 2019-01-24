[TOC]

---

## samba安装
apt-get install samba

## samba配置修改(/etc/samba/)
[linux]
path=/home/linux
valid users=linux
public=yes
writable=yes

## 重启samba服务
    service smbd restart

## 创建samba用户
    smbpasswd -a root