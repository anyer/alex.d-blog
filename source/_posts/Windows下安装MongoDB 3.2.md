---
title: Windows下安装MongoDB 3.2
copyright: true
categories:
  - 安装部署
tags:
  - Windows
  - MongoDB
description: 在安装MongoDB 3.2.0版本时，翻看官网安装说明，参照成功安装。为方便日后安装参考，记录此文。文章自己简单翻译，有出入望指教。
abbrlink: 9a06f51f
date: 2016-03-21 23:02:57
updated: 2016-03-21 23:02:57
permalink:
---

### **MongoDB** 
在安装MongoDB 3.2.0版本时，翻看官网安装说明，参照成功安装。为方便日后安装参考，记录此文。文章自己简单翻译，有出入望指教。

----------

### **MongoDB 安装**
#### **确定MongoDB版本**
官网提供了三个版本下载：
- `MongoDB for Windows 64-bit` 适合 64 位的 Windows Server 2008 R2, Windows 7 , 及最新版本的 Window 系统。
- `MongoDB for Windows 32-bit` 适合 32 位的 Window 系统及最新的 Windows Vista。 32 位系统上 MongoDB 的数据库最大为 2GB。
- `MongoDB for Windows 64-bit Legacy` 适合 64 位的 Windows Vista, Windows Server 2003, 及 Windows Server 2008 。
MongoDB官网下载地址：[MongoDB downloads pages](https://www.mongodb.org/downloads#production)
, 此时官网最新版本为3.2.4 。
![MongoDB Download Pages ](http://img.blog.csdn.net/20160321105603123)

根据系统下载对应版本，64版本的MongoDB不支持Windows 32位系统。不知道本机的位数，可以通过以下代码查看：
```
wmic os get caption   #查看系统的版本  win xp/win 7...
wmic os get osarchitecture  #查看系统架构（位数）  x86/x64
```
![os](http://img.blog.csdn.net/20160321160357683)
通过查询可以知道，本机是64位系统，所以使用64的`mongodb-win32-x86_64-2008plus-ssl-3.2.0-signed.msi` 。

#### **安装MongoDB**
![install](http://img.blog.csdn.net/20160321112539059)

![install_Choose 'Custom'](http://img.blog.csdn.net/20160321112620807)

选择自定义安装模式，选择安装目录 `d:\MongoDB` 
![install_Choose location path](http://img.blog.csdn.net/20160321113719603)

注：MongoDB是独立的，没有任何其他系统的依赖。你可以在任何你选择的文件夹运行MongoDB。所以你可以在任意文件夹中安装MongoDB（如`D:\test\ MongoDB`）。 注意避免中文目录。

----------

### **MongoDB 无人值守安装**

文档中介绍了Unattended Installation的安装方式，想要采用此方式安装，可以参看。
要使用无人值守安装，需要用到 `msiexec.exe` 。
#### **打开管理员命令提示**
需要通过管理员模式的命令提示符，来执行安装命令。
管理员命令提示打开方式：

-	快捷键`win+r`打开“运行”窗口，输入`cmd`
![run](http://img.blog.csdn.net/20160321165520814)

- 快捷键 `Ctrl + Shift + Enter` ，则可以打开	”管理员命令提示“。（win xp/win 7下）

#### **Windows安装MongoDB**
选择修改`.msi`安装文件的安装路径并执行，语句如下：

```
msiexec.exe /q /i mongodb-win32-x86_64-2008plus-ssl-3.2.0-signed.msi ^
            INSTALLLOCATION="C:\mongodb" ^
            ADDLOCAL="all"
```
通过`INSTALLLOCATION`值可以指定安装路径。默认使用这种方式安装，可以通过`AddLOCAL`来安装MongoDB组件集，这里设置`all` 表示全部安装，也可以选择安装组件集，各组件之间使用逗号隔开。组件集如下：
|Component Set|	Binaries|
|:---|:---|
|Server	|mongod.exe|
|Router	|mongos.exe|
|Client	|mongo.exe|
|MonitoringTools	|mongostat.exe, mongotop.exe|
|ImportExportTools	|mongodump.exe, mongorestore.exe, mongoexport.exe, mongoimport.exe|
|MiscellaneousTools	|bsondump.exe, mongofiles.exe, mongooplog.exe, mongoperf.exe|
例如只安装MongoDB的工具和调用组件：
```
msiexec.exe /q /i mongodb-win32-x86_64-2008plus-ssl-3.2.0-signed.msi ^
            INSTALLLOCATION="C:\mongodb" ^
ADDLOCAL="MonitoringTools,ImportExportTools,MiscellaneousTools"
```

----------

### **MongoDB 运行**

#### **设置MongoDB运行环境**
MongoDB需要数据目录来存储所有的数据，其默认的数据目录为`\data\db` ，可以通过`mongod.exe --dbpath`命令来指定MongoDB的数据目录。例如：
```
mkdir D:\MongoDB\data\db;
D:\MongoDB\bin\mongod.exe --dbpath D:\MongoDB\data\db
```
如果路径里面包含空格，就用双引号括住整个路径，例如：

```
D:\MongoDB\bin\mongod.exe --dbpath "D:\MongoDB db data"
```
![set dbpath](http://img.blog.csdn.net/20160321211411290)
看到上面的提示底部出现` waiting for connections` 字样，则表示dbpath配置完成，且MongoDB启动成功。
而且此时打开资源管理器，进入MongoDB的dbpath目录，内容如下：
![show dbpath](http://img.blog.csdn.net/20160321204852913)
可以发现本地确实初始化数据库了。
创建成功时，MongoDB会根据系统安全级别，弹出mongod.exe网络通信的安全警告，选择允许，且需要选择网络时，应该选择私有网络，如家庭和工作网络。更多MongoDB的信息安全，请参见 [Security Documentation](https://docs.mongodb.org/manual/security/)。

#### **运行MongoDB**
通过运行mongo.exe启动MongoDB。例如：
```
D:\MongoDB\bin\mongo.exe 
```
命令行窗口显示如下内容：
![mongo](http://img.blog.csdn.net/20160321211537261)
窗口中可以看到当前MongoDB shell的版本，及此时连接的数据库。

注：如果想要使用.net开发应用程序，更多信息可以参看文档 [C# and MongoDB](https://docs.mongodb.org/ecosystem/drivers/csharp)

#### **开始使用MongoDB**

为了帮助您开始使用MongoDB，MongoDB提供了各种驱动版本的入门指南 [Getting Started Guides](https://docs.mongodb.org/manual/#getting-started)。

在MongoDB Shell中，通过`help` 来查看命令说明：
![MongoDB Shell help](http://img.blog.csdn.net/20160321223352064)

在生产环境中部署MongoDB之前，考虑生产记[Production Notes](https://docs.mongodb.org/manual/administration/production-notes/)录文件。

最后想停止MongoDB，可以在mongod.exe的命令行窗口，使用快捷键Ctrl+c即可。
![MongoDB Stop](http://img.blog.csdn.net/20160321223524456)
出现如框中的路径时，表示MongoDB已停止。

----------

### **配置MongoDB的Windows服务**
在上面的配置中，虽然启动了服务，且可以进行数据库操作，但是开两个窗口很不方便，所以可以通过配置文件，来配置windows服务。

#### **创建目录**
为您的数据库和日志文件创建目录：

```
mkdir D:\MongoDB\data\db
mkdir D:\MongoDB\data\log
```
![mkdir db/log ](http://img.blog.csdn.net/20160321223830367)



#### **创建cfg配置文件**
创建一个配置文件，文件内必须设置MongoDB日志路径 systemLog.path。包扩一些其他的附加配置选项。
例如，在在`D:\MongoDB\` 下创建mongod.cfg，并在文件内指定systemlog.path和storage.dbpath：

```
systemLog:
    destination: file
    path: D:\MongoDB\data\log\mongod.log
storage:
    dbPath: D:\MongoDB\data\db
```

#### **安装MongoDB服务**
注意：
运行所有的命令都应该在管理员命令行窗口内。（管理员权限运行cmd）
通过运行mongod.exe的--install安装选项和--config和配置选项，指定先前创建的配置文件安装MongoDB服务。

```
"D:\MongoDB\bin\mongod.exe" --config "D:\MongoDB\mongod.cfg" --install
```
设置独立的数据库地址dbpath，可以通过配置文件或者命令--dbpath来设置。

如果需要，你可以安装多个实例的mongod.exe或mongos.exe服务。安装的每个服务设置唯一的 --serviceName 和--serviceDisplayName。仅当有足够的系统资源和系统设计要求时，设置多个实例。


如要让服务自动启动，可以通过下面命令：

```
sc.exe create MongoDB binPath= "D:\MongoDB\bin\mongod.exe --service --config=\"C:\MongoDB\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
```
sc.exe中在“=”和配置值（如“binpath =”）之间需要一个空格，且用一个“\”转义双引号，以逃避双重引号。

如果成功创建，下面的日志信息将显示：
```
[SC] CreateService SUCCESS
```

#### **开启服务**
```
net start MongoDB
```
![start MongoDB service](http://img.blog.csdn.net/20160321224026948)


#### **关闭和删除服务**

停止MongoDB服务使用以下命令：
```
net stop MongoDB
```
删除MongoDB服务使用以下命令：

```
"D:\MongoDB\bin\mongod.exe" --remove
```

----------


### **参考内容**
[官网3.2版本文档：安装说明](https://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows/)
关于无人值守安装，可以看看Microsoft的[What Is Unattended Installation?](https://technet.microsoft.com/zh-cn/library/cc785644%28v=ws.10%29.aspx)
百度百科介绍，点这里：[无人值守安装](http://baike.baidu.com/link?url=61J8JJWNp7ba1jBUhnp79ZkdoVFSJsyVJkgwfENozbn8zoT-WPlOPD_EL8EtYE0A65piO9TpChwA4ZvKGSgViq)