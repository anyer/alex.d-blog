---
title: 免安装MySQL启动3534错误处理
copyright: true
categories:
  - 问题处理
  - 安装部署
tags:
  - MySQL
description: 免安装版MySQL配置完成后，运行服务时报错3534
abbrlink: 6b3d0e5e
date: 2018-06-05 22:02:57
updated: 2018-06-05 22:02:57
---

### **问题描述**
在window10 64位系统环境下，官方下载免安装版MySQL，解压配置后，安装MySQL服务成功，运行时报错，错误提示如下：

![3534错误提示](https://upload-images.jianshu.io/upload_images/111675-3cb77c2f80ec6f14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---

### **问题处理**
 因为没有其他错误提示，首先尝试使用命令`mysqld --console`查看控制台输出，结果如下：
 
![查看控制台信息](https://upload-images.jianshu.io/upload_images/111675-89edbe40051c1c3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


此处会发现有ERROR错误提示，不难发现此处的路径有问题，通过检查配置文件`my.ini`内的路径，发现为转移字符`\t`导致的此错误：

![查看配置文件内配置的路径](https://upload-images.jianshu.io/upload_images/111675-4838a0de07aa0564.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


将地址中的斜杠`\`修改为反斜杠`/`，如下：

![修改配置文件内路径](https://upload-images.jianshu.io/upload_images/111675-f3bfb7377906a633.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


删除已经安装的服务，重新安装，重启：

![依旧报错3534](https://upload-images.jianshu.io/upload_images/111675-091c247ab366c9ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此处依旧报错，命令`mysqld --console`，查看控制台信息：

![查看控制台信息](https://upload-images.jianshu.io/upload_images/111675-fb5239b82faca4d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


提示配置的数据库存放目录（即`my.ini`配置文件中配置的`datadir`，本文配置路径为`D:/work/tools/mysql-5.7.21-winx64/data`）下表不存在，检查数据库存放目录：

![查看数据库存放目录](https://upload-images.jianshu.io/upload_images/111675-6684492422665479.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过查看，发下目录下确实不存在mysql相关表。此处错误因为未初始化数据库，导致配置MySQL数据库存放目录下没有生成对应的数据库表，尝试使用`mysqld --initialize`命令初始化数据库：

- 首先清理配置的数据库数据目录下的文件；
- `mysqld --remove` 命令删除服务
- `mysqld --install` 命令重新创建服务
- `sc query mysql` 命令确认服务是否生成，正常生成，则通过命令`mysqld --initialize` 初始化数据库
- 最后`net start mysql` 启动服务

运行如下：

![处理完成](https://upload-images.jianshu.io/upload_images/111675-0d8fa1b07b584c10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


服务正常启动，此时配置的数据库目录新生成文件如下：

![初始化后，数据库存储目录](https://upload-images.jianshu.io/upload_images/111675-52abbae8cfe081c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


---

### **问题总结**
此问题主要有几个原因导致：
 
 - 配置文件不对
 - 未创建数据库存放目录
 - 创建服务后未初始化直接启动

因此，遇到此错误，则在确保正确配置`my.ini`配置文件后，创建指定的数据库存放目录，然后按照以下命令依次执行即可：

``` cmd
mysqld --remove
mysqld --install
#记得安装服务后，此处要初始化
mysqld --initialize  
net start mysql
	
```
