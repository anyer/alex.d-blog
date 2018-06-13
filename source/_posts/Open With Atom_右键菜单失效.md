---
title: Open With Atom右键菜单失效
copyright: true
categories:
  - 问题处理
tags:
  - Atom
description: 右键系统存在“Open With Atom”选项，但点击无效，且不加载Atom图标
date: 2017-07-03 18:01:38
updated: 2017-07-03 18:01:38
---

### **问题描述**

更换Win7系统后，重新安装了1.18.0版的Atom，右键菜单中的"Open With Atom"项失效，  且加载不了Atom的图标问题，如下图：

![Atom图标不加载.png](http://upload-images.jianshu.io/upload_images/111675-88c16e4f363b2685.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![在桌面或文件夹内点击Open With Atom显示.png](http://upload-images.jianshu.io/upload_images/111675-0a802af6d211380c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![在文件或文件夹上点击Open With Atom显示.png](http://upload-images.jianshu.io/upload_images/111675-9d7bbfb708aa8286.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

尝试重新安装Atom后，依旧出现类似问题。

---

#### **问题分析**

此处应该是程序安装时，注册表项没有注册完成，或安装后使用软件进行了注册表清理。具体原因不确定，有知道的朋友，望告知~

---

#### **问题解决**
 - 首先修复右键点击目录或空白处时Atom图标不显示及“Open With Atom”无效的情况：
  1.  打开注册表编辑器(`Win + R`运行窗口键入`regedit`快速启动)
  2. 找到`[HKEY_CLASSES_ROOT\Directory\shell\Atom]`及`[HKEY_CLASSES_ROOT\Directory\Background\shell\Atom]`两项，看到类似下图：

![修复1_1.png](http://upload-images.jianshu.io/upload_images/111675-e76aad324a731f98.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  3. 点击上面的Atom项，右侧添加新的字符串值，名字为`Icon`,值为`"C:\Users\[此处为当前计算机用户名，如：Administrator]\AppData\Local\atom\app.ico"`（注意检查app.ico链接的有效性！），修改结果如：

![修复1_2_1.png](http://upload-images.jianshu.io/upload_images/111675-8ad373deee8d297c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在左侧上面的Atom项上右键，新建“项”，名字命名为`command`,点击“command”项，修改右侧的`(默认)`项，值为`"C:\Users\[此处为当前计算机用户名，如：Administrator]\AppData\Local\atom\[此处为atom版本目录，如app-1.8.0]\atom.exe" "%V"`,其中的`app-1.18.0`为本文安装的atom版本对应的目录，此处根据个人具体版本进行替换（注意检查atom.exe链接的有效性！），修改结果如下：

![修复1_2_2.png](http://upload-images.jianshu.io/upload_images/111675-d149590abd1d6ccb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下面的Atom项，操作如上，最终结果如下：


![修复1_2_3.png](http://upload-images.jianshu.io/upload_images/111675-62772a0e2215405d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


至此，右键菜单**“Open With Atom”**项在文件夹及文件夹内空白处右键显示正常，且可以正常打开对应的文件夹。但此时依旧无法在单个文件上起效果。
 

![此时图标正常，且Open With Atom功能正常](http://upload-images.jianshu.io/upload_images/111675-094d5693739f586e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![此时图标正常，且Open With Atom功能正常](http://upload-images.jianshu.io/upload_images/111675-1377d2129840352a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 - 修复右键点击单个文件时Atom图标不显示及“Open With Atom”无效的情况：
 注册表编辑器中，找到`[HKEY_CLASSES_ROOT\*\shell\Atom]`项，如下图：

![修复2_1.png](http://upload-images.jianshu.io/upload_images/111675-787ff12cb7eb0d51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此处可以看到，注册表内的版本（1.2.4）和安装的版本（1.18.0）不匹配（可能是更新或卸载时没有清理干净导致）,且此处的`Icon`对应的值为`atom.exe`而不是`app.ico`修改为对应的版本即可（注意检查app-1.18.0目录链接的有效性）。
如Atom项没有此图中的`Icon`字符串值及`command`项，则根据上续步骤添加对应的值，注意此处的`command`的值为`"C:\Users\[此处为当前计算机用户名，如：Administrator]\AppData\Local\atom\[此处为atom版本目录，如app-1.8.0]\atom.exe" "%1"`
做类似前面的修改，最终结果如下：

![修复2_2.png](http://upload-images.jianshu.io/upload_images/111675-d939e5b90603f453.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![修复2_3.png](http://upload-images.jianshu.io/upload_images/111675-8e22252e4a23f762.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)\

![修复2_4.png](http://upload-images.jianshu.io/upload_images/111675-d1e025263f63e345.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![修复2_5.png](http://upload-images.jianshu.io/upload_images/111675-115a89a91e429993.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

--- 

#### 小记

贴出修复此问题的`.reg`代码，使用方式：复制下列代码到新建的文本文档，做对应修改（主要修改当前计算机用户名及atom的版本目录），保存文件，重命名`xxx.reg`（xxx可以任意），右键执行“合并”，即可快速添加到注册表。

 - 修复右键点击目录（文件夹）时Atom图标不显示及“Open With Atom”无效的情况：

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\Atom]
@="Open with Atom"
"Icon"="C:\\Users\\[此处为当前计算机用户名，如：Administrator]\\AppData\\Local\\atom\\app.ico\"

[HKEY_CLASSES_ROOT\Directory\shell\Atom\command]
@="\"C:\\Users\\[此处为当前计算机用户名，如：]\\AppData\\Local\\atom\\[此处为atom版本目录，如app-1.8.0]\\atom.exe\" \"%V\"

```
 - 修复右键点击目录空白处时Atom图标不显示及“Open With Atom”无效的情况：

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\Atom]
@="Open with Atom"
"Icon"="C:\\Users\\[此处为当前计算机用户名，如：Administrator]\\AppData\\Local\\atom\\app.ico\"

[HKEY_CLASSES_ROOT\Directory\shell\Atom\command]
@="\"C:\\Users\\[此处为当前计算机用户名，如：]\\AppData\\Local\\atom\\[此处为atom版本目录，如app-1.8.0]\\atom.exe\" \"%V\"

```

 - 首先修复右键点击目录或空白处时Atom图标不显示及“Open With Atom”无效的情况：

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\*\shell\Atom]
@="Open with Atom"
"Icon"="C:\\Users\\[此处为当前计算机用户名，如：Administrator]\\AppData\\Local\\atom\\app.ico\"

[HKEY_CLASSES_ROOT\Directory\shell\Atom\command]
@="\"C:\\Users\\[此处为当前计算机用户名，如：]\\AppData\\Local\\atom\\[此处为atom版本目录，如app-1.8.0]\\atom.exe\" \"%1\"

```

至此Atom的右键**Open With Atom**图标不现实及功能失效解决，其他程序，操作类似~