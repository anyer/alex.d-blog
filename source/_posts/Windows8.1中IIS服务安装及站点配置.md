---
title: Windows8.1中IIS服务安装及站点配置
copyright: true
categories:
  - 安装部署
tags:
  - Windows 8.1
  - IIS
description: 本文记录Windows8.1中IIS服务安装及站点配置过程。
abbrlink: 291f04db
date: 2017-01-12 15:41:20
updated: 2017-01-12 15:41:20
---


### **IIS介绍**

> **IIS（Internet Information Services，互联网信息服务）**,是由微软公司提供的基于运行Microsoft Windows的互联网基本服务。
> IIS是一个World Wide Web server。Gopher server和FTP server全部包容在里面。 IIS意味着你能发布网页，并且有ASP（Active Server Pages）、JAVA、VBscript产生页面，有着一些扩展功能。IIS支持一些有趣的东西，像有编辑环境的界面（FRONTPAGE）、有全文检索功能的（INDEX SERVER）、有多媒体功能的（NET SHOW） 其次,IIS是随Windows NT Server 4.0一起提供的文件和应用程序服务器，是在Windows NT Server上建立Internet服务器的基本组件。它与Windows NT Server完全集成，允许使用Windows NT Server内置的安全性以及NTFS文件系统建立强大灵活的Internet/Intranet站点。IIS（Internet Information Server，互联网信息服务）是一种Web（网页）服务组件，其中包括Web服务器、FTP服务器、NNTP服务器和SMTP服务器，分别用于网页浏览、文件传输、新闻服务和邮件发送等方面，它使得在网络（包括互联网和局域网）上发布信息成了一件很容易的事。。  —— [百度百科](http://baike.baidu.com/link?url=Q-DF9ADl-9bpTlftXpgfytzIT6D5nDVhNfO5796rygpTVLKAE7Y2FsvaPnAcpkPzmVCaR50Svlgpeq3kGlRD6a)

----------

### **IIS安装**

**1. 打开“控制面板” - “程序”- “启用或关闭 Windows 功能”：**

![“控制面板”中选择“程序”](http://img.blog.csdn.net/20170112092115713?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![“程序”中选择“启用或关闭 Windows 功能”](http://img.blog.csdn.net/20170112092513953?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
**2. 选择“Internet 信息服务（或Internet Information Services）”项，勾选IIS服务相关功能（按需勾选）：**

![勾选IIS服务相关内容](http://img.blog.csdn.net/20170112100432717?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
**3. 确定安装:**
点击确定后会出现搜索文件的提示框：

![搜索安装文件](http://img.blog.csdn.net/20170112093953363?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

此时系统有过更新，则会直接安装，如没有更新文件，会提示下载：

![提示下载安装文件](http://img.blog.csdn.net/20170112094102599?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

此时点击“从 Windows 更新下载文件”，等待下载完成后，会自动安装功能。

**注：**在下载时，可能会提示错误代码：0x800F0906，这个是.NET Framework 3.5安装时提示的错误，解决方法可以看[这里](https://support.microsoft.com/zh-cn/help/2734782/.net-framework-3.5-installation-error-0x800f0906,-0x800f081f,-0x800f0907)或[这里](http://blog.csdn.net/haovip123/article/details/17399061)。出现此错误提示时，按上述解决方法安装.NET 3.5后再重复IIS安装步骤，即可快速完成。
另，附上Microsoft .NET Framework 3.5 Service Pack 1 [下载地址](https://www.microsoft.com/zh-CN/download/details.aspx?id=22)

----------


### **IIS服务配置**
**1. 快捷键 `WIN + X` - “计算机管理”:**

![计算机管理](http://img.blog.csdn.net/20170112113713148?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
**2.选择IIS管理器** 

![IIS管理器](http://img.blog.csdn.net/20170112114033964?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

弹出的窗口选择“是”以后，注意启动万维网发布服务（W3SVC）：

![启动万维网发布服务](http://img.blog.csdn.net/20170112114725905?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**注：** 在启动IIS服务前，需要先启动万维网发布服务，不然会出现“万维网发布服务(W3SVC)已经停止。除非万维网发布服务(W3SVC)正在运行,否则无法启动网站。”的错误提示。

启动万维网发布服务后，就可以发现 `Default Web Site` 的网站管理的状态为启动：

![IIS 服务启动](http://img.blog.csdn.net/20170112135609028?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

启动IIS服务后即可以浏览网站，出现类似下图结果表示IIS安装配置完成：

![网站浏览](http://img.blog.csdn.net/20170112135924216?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![IIS](http://img.blog.csdn.net/20170112135955497?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


----------

### **IIS服务器站点配置**
**1. “控制面板” - “管理工具”-“Internet Information Services（IIS）管理器”：**

![IIS管理器界面](http://img.blog.csdn.net/20170112141358615?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
**2. 如图，网站上右键，“添加站点”：**

![添加站点选项](http://img.blog.csdn.net/20170112141932850?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![设置新添加站点信息](http://img.blog.csdn.net/20170112143739522?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

设置完成后，可以在“网站”下看到自己最新添加的站点。如，此处新增站点“HelloWorld”:

![增加的新站点](http://img.blog.csdn.net/20170112144930926?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**注：** 在填写新添加网站信息时，注意端口值，避免冲突。（当其他网站运行时，端口出现冲突时，会有窗口提醒。）

**3. 设置完成后，启动万维网发布服务（W3SVC），然后在新站点名称上右键 - “网站管理”- “浏览”，会出现如下错误提示页面：**

![Http 403错误](http://img.blog.csdn.net/20170112145749097?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

错误提示页面中，清楚的说明了错误可能的原因及解决方法，按照其解决步骤操作后，即可运行成功：

![目录浏览](http://img.blog.csdn.net/20170112152525552?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![启用目录浏览](http://img.blog.csdn.net/20170112152701177?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

设置好目录浏览，再次浏览时，会发现403错误不见了，但只是显示目录结构，此处是“index.aspx”文件不再“默认文档”的配置中，这里添加上，即可解决：

![显示目录结构](http://img.blog.csdn.net/20170112152737201?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![默认文档](http://img.blog.csdn.net/20170112153417695?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![添加index.aspx到默认文档](http://img.blog.csdn.net/20170112153440618?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

最终运行结果：

![Hello World](http://img.blog.csdn.net/20170112153646416?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)