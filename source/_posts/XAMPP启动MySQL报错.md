---
title: XAMPP启动MySQL报错
copyright: true
categories:
  - 问题处理
tags:
  - XAMPP
  - MySQL
  - Error
description: 本文记录Windows下XAMPP启动时MySQL报错情况的处理。
date: 2016-02-15 16:55:55
updated: 2016-02-15 16:55:55
---


### **问题重述**
XAMPP启动mysql时，出现错误，提示如下：
![mysql_start_error](http://img.blog.csdn.net/20160215041503587)


----------


### **问题适用情况**
在安装XAMPP环境之前，本地独立安装了MySQL开发环境，此时在XAMPP启动MySQL时就会出现上面问题，是这样的情况，可以试试下面的方法来解决。


----------


### **解决方案**
打开注册表（快捷打开方式：`cmd->regedit`）,找到`[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL]` 下的ImagePath项，如下图：
![mysql_ImagePath](http://img.blog.csdn.net/20160215035530845)
此时mysql的ImagePath值为`D:\mysql-5.1.73-winx64\bin\mysqld --defaults-file=my.ini MySQL` ， 即指向本地mysql安装路径下。
![这里写图片描述](http://img.blog.csdn.net/20160215040027847)
将此处修改为 `D:\xampp\mysql\bin\mysqld --defaults-file=my.ini MySQL` ，其中`D:\xampp\mysql\bin\mysqld` 为XAMPP环境中mysql的路径，并指定默认的配置文件为my.ini。
修改完后，关闭注册表，关闭任务管理器中的`mysqld.exe` (如果有此项的话) ，打开服务，找到MySQL服务，查看属性，我们可以看到此时MySQL的可执行文件路径指向到了XAMPP下的MySQL路径
![这里写图片描述](http://img.blog.csdn.net/20160215152627788)
之后在XAMPP控制台中重新启动MySQL，此时我的MySQL终于启动了。
![mysql_start_success](http://img.blog.csdn.net/20160215041738556)


----------


### **最终解决**
不难发现，其实XAMPP并没有启动MySQL，因为在进程中可以看到，任务只是mysqld.exe进程启动，且MySQL显示启动中。通过phpmyadmin，我们可以清晰的看到MySQL服务还是有问题的。
![这里写图片描述](http://img.blog.csdn.net/20160215153826761)
此时的MySQL服务会一直启动中，且停止服务时，会出现无法停止服务的提示
![mysql_stop](http://img.blog.csdn.net/20160215043135070)
而此时的进程中，可以发现mysqld.exe进程启动了，但没有正常启动服务
![mysqld](http://img.blog.csdn.net/20160215043244625)
进服务管理器（快捷方式`cmd->services.msc`）中发现，启动MySQL时出现了1053错误
![mysql_error:1053](http://img.blog.csdn.net/20160215043511329)
此时，我的解决方法就是再还原MySQL的ImagePath值。
然后关闭XAMPP及MySQL服务和mysqld.exe进程，之后运行XAMPP控制台，此时报如下错误：
![这里写图片描述](http://img.blog.csdn.net/20160215162041528)
可以发现错误中，说明了是路径问题，所以我复制了`Expected Path` 后的路径`d:\xampp\mysql\bin\mysqld.exe --defaults-file=d:\xampp\mysql\bin\my.ini mysql` 到MySQL的ImagePath，此时运行，会出现下面错误
![这里写图片描述](http://img.blog.csdn.net/20160215163101502)
于是按照错误打开日志，即XAMPP控制台中，MySQL的后log按钮，打开日志，会看到下面错误
![这里写图片描述](http://img.blog.csdn.net/20160215163422081)
日志里面说`InnoDB: Cannot create D:\xampp\mysql\data\ib_logfile101` ，于是将`D:\xampp\mysql\data` 目录下的`ib_logfile101`删掉了，顺手我还把`ibdata1`文件删了，之后关闭控制台，重新尝试，发现还是这个错误，再打开日志和上面类似
![这里写图片描述](http://img.blog.csdn.net/20160215163843653)
可以看到`ib_logfile101` 文件创建成功，但是这里`Cannot create D:\xampp\mysql\data\ib_logfile1` 又不能创建 `ib_logfile1` 文件了，于是将`D:\xampp\mysql\data` 下的`logfile` 和`ibdata1` 全删了，之后关闭控制台，重新启动，终于启动MySQL了。
![这里写图片描述](http://img.blog.csdn.net/20160215164242616)
关闭重新尝试，也没有问题了，此时控制台还会提示如下：
![这里写图片描述](http://img.blog.csdn.net/20160215164706178)
就是建议采用管理员模式运行XAMPP。

> **注**：这里要注意的就是，将`logfile`和`ibdata1` 文件复制、替换 `D:\xampp\mysql\data` 下的`logfile`和`ibdata1` 文件，使用MySQL启动时，依旧会报上面的错误，具体原因不是很清楚，有知情者，望不吝告知，谢谢。

----------

这里不知道有没有更好的解决方式，因为此法只是可以让XAMPP启动集成环境中的MySQL，此时本地单独安装的MySQL要启动需要换回ImagePath值。所以个人觉得如果要使用XAMPP集成环境，还是卸载本地安装的MySQL，之后重新安装XAMPP环境，可能会省事点。如果有更好的解决方式，希望可以留言告知，谢谢！