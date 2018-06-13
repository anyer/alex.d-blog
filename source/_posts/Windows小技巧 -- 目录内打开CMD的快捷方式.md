---
title: Windows小技巧 -- 目录内打开CMD的快捷方式
copyright: true
categories:
  - Windows小技巧
tags:
  - Windows
  - cmd
  - 快捷方式
description: 本文记录Windows下目录内打开cmd命令行窗口的快捷方式。
date: 2016-11-10 19:27:33
updated: 2017-08-08 22:32:03
---

在工作中常常会有需要在某个文件夹内使用cmd的情况，例如运行某脚本，下面演示几种方法。

以进入以下目录操作为例：

![目录路径](http://img.blog.csdn.net/20161110191026849)


----------


### **方式一 ： 常用的cd命令**
cd命令是我们平常使用比较多的方式：
 1. `Win+R`打开cmd窗口，默认显示如下（非管理员模式）；
 
 ![非管理员模式的cmd窗口](http://img.blog.csdn.net/20161110191111156)

 2. 此时需要依次键入命令`e:` `cd github` `cd anyer` `cd Wechat-Weapp`

![cd命令进入目录](http://img.blog.csdn.net/20161110191224922)

 或`e:` `cd github\anyer\WeChat-WeApp\` 

![cd命令进入目录1](http://img.blog.csdn.net/20161110191728593)
	
 或 `cd E:\github\anyer\WeChat-WeApp\`（没有进入指定目录时，再键入一个）

![cd命令进入目录2](http://img.blog.csdn.net/20161110191831221)

 3.进行操作。


----------


### **方式二 ： 鼠标右键的快捷方式**
显然经历了上面的多个命令，是不是感觉很忧桑，下面来个快捷点的方式：
 1.`Win+E`资源管理器快速进入指定目录；
 
 ![目录路径](http://img.blog.csdn.net/20161110191026849)
 
 2.`Shift+鼠标右键`出现选项菜单
 
 ![Shift+鼠标右键进入目录](http://img.blog.csdn.net/20161110192226568)
 
 选择`在此处打开命令窗口(W)`项；
 
 ![Shift+鼠标右键进入目录1](http://img.blog.csdn.net/20161110192355288)
 
 3.进行操作。

上述方式仅支持当前用户（非管理员）权限的cmd，当需要管理员权限时，可以尝试下面方式。

给右键添加管理员方式运行命令行窗口，使用下面代码，复制代码，保存为`任意名称.reg`，即保存为注册表文件。

``` cmd
Windows Registry Editor Version 5.00

; Created by: Shawn Brink

; http://www.sevenforums.com

; Tutorial: http://www.sevenforums.com/tutorials/47415-open-command-window-here-administrator.html

[-HKEY_CLASSES_ROOT\Directory\shell\runas]

[HKEY_CLASSES_ROOT\Directory\shell\runas]

@="Open cmd here as Admin"

"HasLUAShield"=""

[HKEY_CLASSES_ROOT\Directory\shell\runas\command]

@="cmd.exe /s /k pushd \"%V\""

[-HKEY_CLASSES_ROOT\Directory\Background\shell\runas]

[HKEY_CLASSES_ROOT\Directory\Background\shell\runas]

@="Open cmd here as Admin"

"HasLUAShield"=""

[HKEY_CLASSES_ROOT\Directory\Background\shell\runas\command]

@="cmd.exe /s /k pushd \"%V\""

[-HKEY_CLASSES_ROOT\Drive\shell\runas]

[HKEY_CLASSES_ROOT\Drive\shell\runas]

@="Open cmd here as Admin"

"HasLUAShield"=""

[HKEY_CLASSES_ROOT\Drive\shell\runas\command]

@="cmd.exe /s /k pushd \"%V\""

```

保存后，双击此文件，即在右键添加了选项：

![右键菜单添加管理员运行cmd](http://img.blog.csdn.net/20161110192440320)


当想删除右键菜单选项时，可以使用下面命令，复制保存为`任意名称.reg`，双击运行即可。
``` cmd
  Windows Registry Editor Version 5.00

  ; Created by: Shawn Brink

  ; http://www.sevenforums.com

  ; Tutorial: http://www.sevenforums.com/tutorials/47415-open-command-window-here-administrator.html

  [-HKEY_CLASSES_ROOT\Directory\shell\runas]

  [-HKEY_CLASSES_ROOT\Directory\Background\shell\runas]

  [-HKEY_CLASSES_ROOT\Drive\shell\runas]

```



----------

### **方式三：资源管理器（2017-08-08 增）**
在资源管理器的地址栏内输入`cmd` 或 `powershell` 回车后，依旧可以实现在当前目录快速打开命令行窗口:
 - 进入指定目录
 
 ![进入指定目录](http://img.blog.csdn.net/20170808123218214?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
 
 - 地址栏输入`cmd` 或 `powershell`

![输入cmd命令](http://img.blog.csdn.net/20170808123327984?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 - 回车确认
 
 ![指定目录打开cmd](http://img.blog.csdn.net/20170808123342342?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


----------

### **方式四 : git命令行**
此方式使用git的用户，安装git时确定安装git bash命令行，以确保可以在命令行里完成git操作~。windows下安装git教程自行百度了。安装好后，在需要使用cmd的目录中，使用git bash来替代使用。
1.资源管理器进入指定目录；
2.`鼠标右键`，菜单项中选择`Git Bash Here`项目；

![GIt Bash进入目录](http://img.blog.csdn.net/20161110192522196)

![Git命令行窗口替代cmd](http://img.blog.csdn.net/20161110192546400)

3.进行操作；

其他方式，后续了解后补充~




























































































































































