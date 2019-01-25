---
title: ubuntu重装系统环境搭建
categories:
  - Linux
tags:
  - 软件
reward: true
originContent: |-
  ## 重装Ubuntu后的环境搭建
  ---

  ### 必要的
  ---
  #### samba服务
  ```shell
  $sudo apt-get install samba

  // 修改配置文件
  [hgh]
  path=/home/hgh
  valid users=hgh
  public=yes
  writable=yes
  ```

  #### git
  ```shell
  $sudo apt-get install git
  ```

  #### vim
  ```shell
  $sudo apt-get install vim-gtk
  ```

  ### ssh
  ```shell
  $sudo apt-get install openssh-server
  ```

  ---
  ### 可选的
toc: false
date: 2018-05-13 08:46:47
description:
---

## 重装Ubuntu后的环境搭建
---

### 必要的
---
#### samba服务
```shell
$sudo apt-get install samba

// 修改配置文件
[hgh]
path=/home/hgh
valid users=hgh
public=yes
writable=yes
```

#### git
```shell
$sudo apt-get install git
```

#### vim
```shell
$sudo apt-get install vim-gtk
```

### ssh
```shell
$sudo apt-get install openssh-server
```

---
### 可选的