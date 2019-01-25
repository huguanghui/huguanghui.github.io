---
title: acl开源库的使用
categories:
  - 开源代码
tags:
  - c++
reward: true
originContent: |-
  # 来历

  # 使用

  ## queue_file

  队列文件

  属性:
  m_fp                文件流对象
  m_filePath          相对于根目录的全部路径
  m_home              根目录路径
  m_queueName         队列名称
  m_queueSub          队列下的子目录
  m_partName          队列文件名
  m_extName           扩展名
  m_locker            锁
  m_bLocked           锁否
  m_bLockerOpened     文件锁开否
  nwriten_            写入文件尺寸


  # 优缺点分析
toc: false
date: 2018-10-14 22:07:15
description:
---

# 来历

# 使用

## queue_file

队列文件

属性:
m_fp                文件流对象
m_filePath          相对于根目录的全部路径
m_home              根目录路径
m_queueName         队列名称
m_queueSub          队列下的子目录
m_partName          队列文件名
m_extName           扩展名
m_locker            锁
m_bLocked           锁否
m_bLockerOpened     文件锁开否
nwriten_            写入文件尺寸


# 优缺点分析