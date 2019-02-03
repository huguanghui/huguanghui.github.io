---
title: Hexo中的常用命令
categories:
  - 前端
tags:
  - 项目管理
reward: true
originContent: |+
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


  ## 利用TravisCI实现文档提交的自动部署

  ```yml
  # 指定语言为node_js, nodejs版本stable
  language: node_js
  node_js: stable

  # 指定构建的分支
  branches:
    only:
      - code

  # 制定node_modules缓存
  cache:
    directories:
      - node_modules

  # 构建之前安装hexo-cli
  before_install:
    - npm install -g hexo-cli

  # 安装依赖
  install:
   - npm install

  # 执行脚本
  script:
    - hexo clean
    - hexo generate

  # 上面的脚本执行成功之后执行deploy
  after_success:
    - git init
    - git config --global user.name "huguanghui"
    - git config --global user.email "522146829@qq.com"
    # 替换同目录下_config.yml文件中的GH_TOKEN字符串为travis后台配置的GH_TOKEN
    - sed -i "s/GH_TOKEN/${GH_TOKEN}/g" ./_config.yml
    - hexo deploy
  ```

  ## hexo插件安装

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


## 利用TravisCI实现文档提交的自动部署

```yml
# 指定语言为node_js, nodejs版本stable
language: node_js
node_js: stable

# 指定构建的分支
branches:
  only:
    - code

# 制定node_modules缓存
cache:
  directories:
    - node_modules

# 构建之前安装hexo-cli
before_install:
  - npm install -g hexo-cli

# 安装依赖
install:
 - npm install

# 执行脚本
script:
  - hexo clean
  - hexo generate

# 上面的脚本执行成功之后执行deploy
after_success:
  - git init
  - git config --global user.name "huguanghui"
  - git config --global user.email "522146829@qq.com"
  # 替换同目录下_config.yml文件中的GH_TOKEN字符串为travis后台配置的GH_TOKEN
  - sed -i "s/GH_TOKEN/${GH_TOKEN}/g" ./_config.yml
  - hexo deploy
```

## hexo插件安装

