---
title: VSCode更新记录
reward: true
date: 2018-11-19 21:33:40
description:
categories:
tags:
- VSCode
---

# VSCode

## VSCode使用

### cmd中文乱码

暂时解决的办法:

chcp 65001

通过配置解决

打开“文件”--“首选项”--“用户设置”，然后在setting.json中设置：

terminal.integrated.shellArgs.windows

```json
{
    "editor.fontSize": 18,
    "terminal.integrated.shellArgs.windows": ["/K chcp 65001 >nul"],
    "terminal.integrated.fontFamily": "Lucida Console",
}
```



## VSCode更新日志

### 10月版本

1.29.1

关键的亮点:
1.多行搜索
2.IntelliSense中的文件图标
3.可折叠堆栈框架
4.改进已加载脚本视图
5.更新了扩展示例
6.CI配方扩展
7.预览列出所有扩展