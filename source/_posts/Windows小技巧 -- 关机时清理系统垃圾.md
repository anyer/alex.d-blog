---
title: Windows小技巧 -- 关机时清理系统垃圾
copyright: true
categories:
  - Windows小技巧
  - Shell
tags:
  - Windows
  - 脚本
description: 本文记录Windows下添加关机脚本及系统垃圾处理脚本介绍。
date: 2017-01-16 16:32:03
updated: 2017-01-16 16:32:03
---


虽然垃圾清理时“老生常谈”的事情了，但由于不太喜欢管家等套件工具，又觉得CCleaner、FCleaner、Glary Utilities等这样的清理维护工具要安装、破解、点击清理等比较繁琐。所以，最后又回归bat批处理清理垃圾的老路。本文简单整理记录下，关于关机时自动调用批处理文件清理系统垃圾的实现。

### **垃圾文件**
- Windows在安装和使用过程中产生的垃圾：
  - 临时文件（如*.tmp、*._mp等）
  - 临时备份文件（如*.bak、*.old、*.syd等）
  - 临时帮助文件（*.gid）
  - 磁盘检查数据文件（*.chk）
  - *.dir、*.dmp、*.nch等其他临时文件

-   软件等使用垃圾：
 - 暴风影音、爱奇艺等播放器的播放记录
 - office等办公软件的使用记录
 - QQ、WeChat等使用时产生的一些零时文件
 - 其他软件应用软件使用时的记录等

- 浏览器使用的垃圾：
 - Cookies
 - 历史记录（包括地址栏历史记录）
 - 各种密码表单账户
 - 脱机缓存文件（图片）
 - 各种搜索记录等。

---

### **清理系统垃圾的批处理文件**

关于清理系统垃圾的批处理代码网上很多，这里提供一种做参考。

``` bat

@echo off
echo -----------------------------------------------------------------------
echo 清空清空COOKIES和IE临时文件目录...
rem del /f /q %userprofile%\COOKIES s\*.*
rem del /f /q %userprofile%\recent\*.*
del /f /s /q "%userprofile%\Local Settings\Temporary Internet Files\*.*"
del /f /s /q "%temp%\*.*"
echo 清除系统临时文件...
:del /f /s /q %systemdrive%\*.tmp
:del /f /s /q %systemdrive%\*._mp
:rd /s /q %windir%\temp & md %windir%\temp
echo 备注：其它系统临时文件比如日志类要谨慎清理，如果不需要也可以直接在上面一句下增加其它文件删除即可。
echo 清空垃圾箱，备份文件和预缓存脚本...
:del /f /s /q %systemdrive%\recycled\*.*
:del /f /s /q %windir%\*.bak
:del /f /s /q %windir%\prefetch\*.*
echo 清理SYSTEM32\DLLCACHE下无用文件...
:%windir%\system32\sfc.exe /purgecache
echo 清除完成！
echo -----------------------------------------------------------------------
pause

```

#### **批处理文件创建**
新建文本文档，复制粘贴上面代码后，保存时名称任意（便于自己记忆就好），最后修改此文本文档的格式（.txt）为 `.bat` 格式，即可以生成批处理文件，双击即可执行。

---

### 添加到关机脚本中

添加到关机组策略中，以满足关机时自动调用批处理文件对垃圾文件的清理。

1. 快捷键 `Win + R`  - “运行” - 输入`gpedit.msc` - 回车打开“本地组策略编辑器”

![运行](http://img.blog.csdn.net/20170116162939627?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![本地组策略编辑器](http://img.blog.csdn.net/20170116162955299?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

2. “本地计算机 策略” - “计算机配置” - “Windows 设置” - “脚本（启动/关机）” - 双击右侧的“关机” - “关机属性”中点击“添加（D）..” - “添加脚本”窗口中点击“浏览（B）..” - 找到本地刚新建的清理垃圾的bat文件：

![添加关机脚本](http://img.blog.csdn.net/20170116163022581?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
”

3. 添加脚本后，可以在关机属性中，看到新添加的脚本，此时点击“应用” - “确定” 即可完成配置：


![添加脚本成功](http://img.blog.csdn.net/20170116163042486?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

当然，根据自己的需要，也可以在系统启动、登陆、注销等时候添加一些脚本，操作步骤类似。不会的话，可以参考微软官方文档，地址见扩展阅读。

---

### 扩展阅读
[微软官网文档 - 使用启动、关机、登录和注销脚本](https://technet.microsoft.com/zh-cn/library/cc753404(v=ws.11).aspx)