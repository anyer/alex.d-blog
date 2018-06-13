---
title: Win8.1的Matlab7卸载问题
copyright: true
categories:
  - 问题处理
tags:
  - Windows 8.1
  - Matlab
  - Error
description: 本文记录Win8.1的Matlab7卸载时报错问题。
date: 2015-07-03- 11:30:26
updated: 2015-07-03- 11:30:26
---


### **问题描述**

使用matlab7自带的uninstaller.exe及控制面板卸载时都提示`exeption calling main`的错误提示信息。

### **问题处理**

- 网上有很多都是介绍说是因为主题不符导致的这个问题，处理方法很简单，就是在个性化中，将主题改为windows经典主题样式，然后执行卸载程序就可以解决了。
- 但有一点很尴尬，我使用的win8.1，在个性化中没有windows经典主题样式 ，这时可以试试下面的方法：
1、在matlab的安装目录（或开始菜单中）找到uninstaller.exe；
2、右键属性，修改其兼容性中兼容模式为Windows vista;
3、确定后，重新运行uninstaller.exe，即可实现卸载。
- 还有很多推荐使用完美卸载，但是很不理想，也会出现相同的错误提示。
