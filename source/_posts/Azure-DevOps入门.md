---
title: Azure_DevOps入门
categories:
  - 版本管理
tags:
  - 项目管理
reward: true
originContent: >-
  # Azure DevOps


  Azure DevOps服务提供了开发协作工具,包括高性能管道,免费的私有Git存储库,可配置的看板,以及广泛的自动化和基于云的负载测试.


  ## 简介


  Azure DevOps的开始使用:

  1.使用Azure Pipelines去编辑GitHub工程

  2.开始使用Azure DevOps


  ## 使用入门


  ### Azure Pipelines编译一个Github仓库


  #### 准备工作


  - 一个Azure
  DevOps组织,如果没有可以[免费创建一个](https://go.microsoft.com/fwlink/?LinkId=307137),

  - GitHub账号


  #### 获取源码


  #### 开始第一次的编译


  - 登陆Azure DevOps组织, 选中你的项目

  - 选中Piplines页,选择新建pipeline

  - 通过选择GitHub作为源代码的位置来完成向导的步骤

  - 认证GitHub账号权限

  - 当重回到Azure Pipelines页面,选择程序对应的存储库

  - Azure Pipelines在你的仓库中分析代码.如果仓库已经包含了一个azure-pipelines.yml文件,这一步将会被跳过.否则,Azure
  Pipelines会基于
    你的代码上会有一个模板
  - 最后,你需要展示出将要使用的YAML文件

  - 如果你看到Run按钮,选择它,跳到下一步.如果你看到Save and Run按钮,先选择Commit directly to the master
  branch,接着再选择Save and run.

  - 等待编译完成
    
  #### 将CI状态徽章到你的仓库中


  - 在Azure Pipelines页面中,进入到Build页面显示pipelines的列表.

  - 选择你创建的pipelines

  - 在pipelines的上下文菜单中,选择Status badge项

  - 拷贝到Markdown中


  ## 使用技巧


  ## 特性分析


  ## 相关链接
toc: false
date: 2019-01-13 14:38:36
description:
---

# Azure DevOps

Azure DevOps服务提供了开发协作工具,包括高性能管道,免费的私有Git存储库,可配置的看板,以及广泛的自动化和基于云的负载测试.

## 简介

Azure DevOps的开始使用:
1.使用Azure Pipelines去编辑GitHub工程
2.开始使用Azure DevOps

## 使用入门

### Azure Pipelines编译一个Github仓库

#### 准备工作

- 一个Azure DevOps组织,如果没有可以[免费创建一个](https://go.microsoft.com/fwlink/?LinkId=307137),
- GitHub账号

#### 获取源码

#### 开始第一次的编译

- 登陆Azure DevOps组织, 选中你的项目
- 选中Piplines页,选择新建pipeline
- 通过选择GitHub作为源代码的位置来完成向导的步骤
- 认证GitHub账号权限
- 当重回到Azure Pipelines页面,选择程序对应的存储库
- Azure Pipelines在你的仓库中分析代码.如果仓库已经包含了一个azure-pipelines.yml文件,这一步将会被跳过.否则,Azure Pipelines会基于
  你的代码上会有一个模板
- 最后,你需要展示出将要使用的YAML文件
- 如果你看到Run按钮,选择它,跳到下一步.如果你看到Save and Run按钮,先选择Commit directly to the master branch,接着再选择Save and run.
- 等待编译完成
  
#### 将CI状态徽章到你的仓库中

- 在Azure Pipelines页面中,进入到Build页面显示pipelines的列表.
- 选择你创建的pipelines
- 在pipelines的上下文菜单中,选择Status badge项
- 拷贝到Markdown中

## 使用技巧

## 特性分析

## 相关链接