---
title: Hexo中的常用命令
categories:
  - 前端
tags:
  - 项目管理
reward: true
originContent: |-
  ## Hexo常用命令
  ```shell
  hexo new "postName" #新建文章
  hexo new page "pageName" #新建页面
  hexo generate #生成静态页面至public目录
  hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
  hexo deploy #将.deploy目录部署到GitHub
  hexo help  # 查看帮助
  hexo version  #查看Hexo的版本
  ```

  ## 本地图片插件使用
  主配置文件中将post_asset_folder:true

  npm install https://github.com/CodeFalling/hexo-asset-image --save

  引用 "![logo](src/log.jpg)"
toc: false
date: 2018-04-15 16:48:33
description:
---

## Hexo常用命令
```shell
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #将.deploy目录部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

## 本地图片插件使用
主配置文件中将post_asset_folder:true

npm install https://github.com/CodeFalling/hexo-asset-image --save

引用 "![logo](src/log.jpg)"