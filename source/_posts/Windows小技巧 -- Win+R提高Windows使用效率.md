---
title: Windows小技巧 -- Win+R提高Windows使用效率
copyright: true
categories:
  - Windows小技巧
tags:
  - Windows
  - 效率
description: 本文记录Windows下Win+R快捷键提高Windows使用效率的方法总结。
date: 2016-09-15 15:51:28
updated: 2016-09-15 15:51:28
---

追求效率的朋友都需要一款顺手的快速启动工具，Win 平台上有键盘流的RunZ、Listary、ALTRun、Launchy、Wox 和图标流的 Fences、Rolan、 WinLaunch 等，而 Mac 上也有 Alfred、Spotlight。
而对于快速启动工具，最基本需求一般是这样的：
 
 - 体积小，资源占用低，速度快，最好可以不常驻运行。
 - 项目尚有人维护，有反馈渠道。
 - 可扩展性强，支持方便地用脚本扩展功能。

但对于Windows系统，不能忽略的是系统自带的 `Win+R` 功能（你还不知道这个吗？那赶快试试吧~）。下面不妨抛开这些软件，来看看这个“神器”怎么提高使用效率。

### **WIN +Ｒ**
Win+R（开始菜单 > 运行）是 Windows 的一个原生的功能，从 XP 到 Windows 10 都自带了。当用户按下「Win+R」快捷键后，系统会弹出一个小窗口让你输入命令，回车后会立即执行命令并关闭自身窗口。它不会驻留后台、不占用内存而且速度极快，因此很多高手们利用 Win+R 改造成属于自己的快捷启动工具！
说的很厉害的样子，那WIN+R到底可以做什么呢？下面来看看它的神奇之处~


----------


#### **快速启动应用程序**
是否还在为一桌面的快捷方式烦恼呢？是否还在为找一个软件的快捷方式烦恼呢？是否还在为要挑选桌面整理工具而烦恼呢？是否。。。
软件打开那么简单的事情，但却给我们带来了不少的困扰，我们要花功夫来鉴别不同的快捷图标，而哪天图标不小心删除了，又要在安装目录，在开始菜单等地方来查找（当然你可以尝试使用Win+F查找更能来实现），但都耽误不少功夫，而且如果想打开多个软件，那又会花去多少功夫呢？
在平时，`Win+R` 使用最多的应该就是打开`cmd.exe` 命令提示符吧~， 那是否用它打开过其他系统应用呢？
下面来看看Win+R启动系统应用的命令吧：
 

> 系统应用程序
> ---- ------ ----- -------- 
> calc - 启动计算器 
> charmap - 启动字符映射表 
> chkdsk - Chkdsk磁盘检查 
> cleanmgr - 磁盘清理 
> clipbrd - 剪贴板查看器 
> cmd.exe - CMD命令提示符 
> dvdplay - DVD播放器 
> dxdiag - DirectX诊断工具 
> eudcedit - 造字程序（专用字符编辑程序） 
> explorer - 资源管理器 
> iexpress - 木马捆绑工具，系统自带 
> magnify - 放大镜 
> mplayer2 - 简易widnows media
> player msconfig - 系统配置 
> mspaint - 画图板 
> mstsc - 远程桌面连接 
> narrator - 屏幕“讲述人”
> notepad - 打开记事本 
> nslookup - IP地址侦测器 
> osk - 打开屏幕键盘 
> regedit - 注册表编辑器
> regedt32 - 注册表编辑器 
> sndrec32 - 录音机 
> sndvol32 - 音量控制程序 
> taskmgr - 任务管理器
> winchat - XP自带局域网聊天 
> write - 写字板
> 
> dcomcnfg - 系统组件服务 
> ddeshare - DDE共享设置 
> nslookup - 网络管理的工具向导 
> ntbackup - 系统备份和还原 
> mobsync - 同步中心 
> winmsd - 系统信息 
> winver - 检查Windows版本 
> wiaacmgr - 扫描仪和照相机向导 
> wscript - windows脚本宿主设置 
> wupdmgr - windows更新程序
> 
> 管理控制台管理单元文件 
> mmc - 管理控制台
> ------- ------- ------ ----------- 
> certmgr.msc - 证书管理 
> ciadv.msc - 索引服务程序 
> comexp.msc - 组件服务 
> compmgmt.msc - 计算机管理 
> devmgmt.msc - 设备管理器 
> dfrg.msc - 磁盘碎片整理程序 
> diskmgmt.msc - 磁盘管理 
> eventvwr.msc - 事件查看器 
> fsmgmt.msc - 共享文件夹管理器 
> gpedit.msc - 组策略管理器（本地组策略编辑器） 
> lusrmgr.msc - 本机用户和组
> ntmsmgr.msc - 移动存储管理器 
> ntmsoprq.msc - 移动存储管理员操作请求 
> perfmon.msc - 性能监视器
> rsop.msc - 组策略结果集 
> secpol.msc - 本地安全策略 
> services.msc - 本地服务设置
> wmimgmt.msc - windows管理体系结构WMI（控制台根节点\WMI控件）

那么非系统自带的程序，怎么快速启动呢？如qq。设置步骤如下：
##### **新建文件夹**
首先新建一个文件夹，用于存储快速启动的程序的快捷方式，文件夹存放位置任意：
![winr dic][1]
这里新建文件夹”**WinR**“,存放在c盘根目录下。
##### **配置环境变量**
将新建的文件夹的目录，添加到环境变量中，如图：
![set dic system static path][2]
ps:此处可以配置单个应用程序到环境变量path中，这样就可以通过Win+R里输入应用程序的名称，实现快速访问。如将cmder.exe配置到环境变量中：
![cmder][3]
这样就可以通过Win+R快速打开Cmder：
![Win + R run cmder][4]
但这里不这样配置，因为这样配置会导致path里面内容过多，可能会容易出现一些问题，而且一个个添加过于麻烦，所以这里配置文件夹路径，然后通过快捷方式实现快速访问。

**注意：配置环境变量时，注意路径中的冒号、斜杠和封号均为英文半角输入**

##### **放置快捷方式**
将软件的快捷方式，放入”**WinR**“目录中，给快捷方式起一个简单好记的名字（自己能记住的） 。
![WinR dic][5]
如上图中，"**ali**" = "阿里巴巴客户端"，"**aqy**" = "爱奇艺播放器"，"**gc**" = "google chrome浏览器"，以此类推，快捷键名称任起，便于自己记忆就好。

##### **快速启动演示**
如打开chrome浏览器，可以通过输入"**gc**"来快速打开
![chrome][6]

**注意:Win+R访问快捷方式时，英文名不区分大小写，即gc和GC是一样的效果**

----------

#### **快速打开文件/目录**
有时想找某个文件，是否还在为要点卡n多个目录感到苦逼呢？是否为经常重复进一个目录而感觉无奈呢？那可以试试`Win+R`大法~
如果知道一个文件的目录，或者想快速进入一个目录，比如我们会常常进入`system32`目录
进行一些操作，那么别一个个文件点了，直接这样来：
![system32][7]
这里可以像快速打开应用程序一样，设置快捷方式来快速的进入目录或打开文件。
首先进入快捷方式存放目录"**WinR**"，在空白地方右键，新建，快捷方式：
![快捷方式][8]
这里键入的对象位置，可以为应用程序、文件、目录、脚本、网页等地址。这里添加的是目录地址，用于快速进入目录。快速启动文件的设置与此类似。

当然，快速进入目录，可以直接通过在`Win+R`运行窗口中输入地址，来实现快速进入指定的路径。如：c:/WinR
![Win + R][9]


##### **其他应用**
- 快速访问指定站点
  - Win+R运行窗口直接输入
 ![baidu][10]
  - 通过设置快捷方式
![baidu][11]
	
- 快速访问脚本
  - Win+R运行窗口直接输入
![batch file][12]  
  - 通过设置快捷方式
![batch file][13]
 
 - 执行命令
使用Win+R也可以执行一些命令任务，如ping：
![ping][14]

当然，为了提高对于Win系统的使用效率，必要的快捷键，大家还是应该知道的，关于windows快捷键，看看Microsoft官网整理的吧~：[Windows 的键盘快捷键][15]

### **关于Win8/8.1/10的快速启动**
使用Win8以上版本系统，都可以明显发现开机速度优于Win7及XP，这就是因为系统增加了快速启动设置，那么这个设置在哪呢？
在系统任务栏的右下角，点击电池图标，出现如下图选项:
![更多电源选项][16]
选择“**更多电源选项**”，会弹出如下“电源选项”窗口：
![电源选项][17]
选择 ”**选择电源按钮的功能**“项，会进入如下“系统设置”窗口：
![系统设置][18]
在这个窗口中，可以看到底部的”关机设置“中有”启用快速启动（推荐）“的选项，此处已勾选，表示打开了系统的快速启动设置，如果想关闭快速启动，可以选择上面的“**更改当前不可用的设置**"选项。

### **加强版 WIN+R -- nTrun**
当然如果觉得它还不够强大，可以尝试下`nTrun（原名 Win+R Adde）`这款软件，可以轻松的帮你完成Win+R功能的定制
[nTrun官网][19]
[官方微博：《nTrun 快速启动-使用向导》][20]
[官方微博：《nTrun 快速启动-详细介绍》][21]


  [1]: http://7xowma.com1.z0.glb.clouddn.com/winr%20dic.png "winr dic.png"
  [2]: http://7xowma.com1.z0.glb.clouddn.com/path.png "path.png"
  [3]: http://7xowma.com1.z0.glb.clouddn.com/cmder.png "cmder.png"
  [4]: http://7xowma.com1.z0.glb.clouddn.com/cmder2.png "cmder2.png"
  [5]: http://7xowma.com1.z0.glb.clouddn.com/winr2.png "winr2.png"
  [6]: http://7xowma.com1.z0.glb.clouddn.com/gc.png "gc.png"
  [7]: http://7xowma.com1.z0.glb.clouddn.com/system32.png "system32.png"
  [8]: http://7xowma.com1.z0.glb.clouddn.com/kjfs.png "kjfs.png"
  [9]: http://7xowma.com1.z0.glb.clouddn.com/winr3.png "winr3.png"
  [10]: http://7xowma.com1.z0.glb.clouddn.com/winr4.png "winr4.png"
  [11]: http://7xowma.com1.z0.glb.clouddn.com/url.png "url.png"
  [12]: http://7xowma.com1.z0.glb.clouddn.com/winr5.png "winr5.png"
  [13]: http://7xowma.com1.z0.glb.clouddn.com/batch%20file.png "batch file.png"
  [14]: http://7xowma.com1.z0.glb.clouddn.com/ping.png "ping.png"
  [15]: https://support.microsoft.com/zh-cn/kb/126449
  [16]: http://7xowma.com1.z0.glb.clouddn.com/dianyuanxuanx.png "dianyuanxuanx.png"
  [17]: http://7xowma.com1.z0.glb.clouddn.com/dianyuananniu.png "dianyuananniu.png"
  [18]: http://7xowma.com1.z0.glb.clouddn.com/xitongshezhi.png "xitongshezhi.png"
  [19]: https://www.ntrun.com
  [20]: http://weibo.com/p/1001603959933623225958
  [21]: http://weibo.com/p/1001603891377686599332









