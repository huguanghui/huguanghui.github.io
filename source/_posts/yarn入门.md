---
title: yarn入门
reward: true
date: 2019-01-14 20:17:54
description:
categories:
tags:
- yarn
---

# Yarn

## 简介

[Yarn](https://yarn.org.cn/) 是一个快速,可靠,安全的依赖管理.

- 极速   缓存它下载的每个包,不重复下载.还可以并行化操作以最大化资源利用率
- 超级安全  在每个安装包执行前使用校验码验证包的完整性
- 超级可靠    使用一个格式详尽但简洁的lockfile和一个精确的算法来安装,能够保证在一个系统上的运行的安装过程也会以同样的方式运行在其他系统上

## 与npm的区别

Yarn 是由Facebook, Google, Exponent和Tilde联合推出了一个新的JS包管理工具,据官方描述, Yarn是为了弥补npm的一些缺陷而出现的.

npm缺点: npm install安装慢,无法保证一致性

## Yarn和npm命令对比

|              npm              |         yarn         |
| :---------------------------: | :------------------: |
|          npm install          |         yarn         |
|   npm install react --save    |    yarn add react    |
|  npm uninstall react --save   |  yarn remove react   |
| npm install react  --save-dev | yarn add react --dev |
|       npm update --save       |     yarn upgrade     |

## npm未来: npm5.0

npm后续的改进

- 添加了类似yarn.lock的package-lock.json
- git依赖支持优化
- 文件依赖优化