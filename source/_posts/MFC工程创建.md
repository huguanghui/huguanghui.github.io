---
title: MFC工程创建
date: 2018-04-20 20:47:33
categories:
- Windows应用
tags:
- VS2017
- MFC
---

## SDK应用程序和MFC应用程序的对比
### SDK应用程序的运行流程
	WinMain => 初始化WNDCLASSEX => 调用RegisterClassEx函数注册窗口类 =>调用ShowWindow和UpdateWindow函数显示并更新窗口 => 进入消息循环<br>

	Windows应用程序是消息驱动的系统或用户让应用程序进行某项操作或完成某个
	任务时会发送消息，进入程序的消息队列，然后消息循环会将消息队列中的消息
	取出，交予相应的窗口过程处理，此程序的窗口过程函数就是myWndProc函数，
	窗口过程函数处理完消息就完成了某项操作或任务。

### MFC应用程序
	MFC应用程序根据工程的名称定义了一个全局对象theApp: CMFCApplication1App 
	theApp,调用CWinApp和CMFCApplication1App的构造函数后，进入WinMain函数()

## 文件
- Accelerator 快捷键



## 相关链接
[WPF使用](https://docs.microsoft.com/zh-cn/dotnet/framework/wpf/getting-started/introduction-to-wpf-in-vs)
[MFC基础创建](https://jingyan.baidu.com/article/915fc414fe1ffa51394b2007.html)
[VS2017+GIT](https://blog.csdn.net/boonya/article/details/78750230)
[MFC系列编程](http://www.jizhuomi.com/catalog.asp?tags=MFC)
