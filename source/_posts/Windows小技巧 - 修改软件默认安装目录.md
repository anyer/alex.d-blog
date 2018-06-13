---
title: Windows小技巧 - 修改软件默认安装目录
copyright: true
categories:
  - Windows小技巧
tags:
  - Windows
description: 本文记录Windows软件默认安装路径的修改。
abbrlink: 5e3c350
date: 2016-09-14 12:20:24
updated: 2016-09-14 12:20:24
---


### **问题描述**
Windows系统下安装软件时，会提示一个默认的安装路径，如：

- 64位系统默认安装路径：
> C:\Program Files\ [软件名称]    

- 32位系统默认安装路径
> C:\Program Files (x86)\ [软件名称]   

无论`64`还是`32`位系统，均会默认提示安装到C盘，而C盘是我们默认的系统盘，如果C盘文件过多那么就会导致我们系统卡顿缓慢，严重者是需要重新安装电脑系统的。所以我们安装软件时，通常会修改软件的安装目录，不过每次都要手动修改，比较麻烦，下面介绍一劳永逸的方式解决这个问题。

---

### **技巧使用**
以 `Git-2.10.0-64-bit.exe` 安装为例。双击git安装文件后，提示如下界面：
![git install](http://img.blog.csdn.net/20160914121328712)
  
 本机系统为 `Windows 8.1 64位`，这里显示64位程序安装的默认路径。
 由于此技巧需要修改注册表，所以不放心的朋友，可以提前备份注册表。修改步骤如下：
 
 ---
 
#### **打开注册表**

快捷键 `Win + R` 打开运行窗口，输入 `regedit` ：
![win+R](http://img.blog.csdn.net/20160914121459323)

回车，打开注册表窗口：
![regedit](http://img.blog.csdn.net/20160914121538091)

---

#### **找到指定注册表项**
找到 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion` 项，点击`CurrentVersion`，如下：
![CurrentVersion](http://img.blog.csdn.net/20160914121605060)

---

#### **修改默认路径参数值**
点击 `CurrentVersion` 右侧选项中的 `ProgramFilesDir` 及 `ProgramFilesDir (x86)` 项，并修改值为自定义默认目录，下图为 `ProgramFilesDir`（64位默认安装路径）修改图示：
![ProgramFilesDir](http://img.blog.csdn.net/20160914121632215)
修改路径后（此处可按个人需要修改）如下：
![Successfully modified](http://img.blog.csdn.net/20160914121653372)

---

#### **安装软件测试**
重新打开 `Git-2.10.0-64-bit.exe` 安装程序，此时安装的默认路径如下：
![Path changed successfully](http://img.blog.csdn.net/20160914121722013)
  
至此，Windows程序默认安装路径修改成功~
  
  
 











































































 























































































































































