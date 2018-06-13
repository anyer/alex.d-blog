---
title: 免安装版MySQL安装完成后登陆1045错误处理
copyright: true
categories:
  - 问题处理
  - 安装部署
tags:
  - MySQL
description: 免安装版MySQL配置时，忘记密码，连接登陆时提示1045错误
grammar_cjkRuby: true
abbrlink: af835572
date: 2018-06-06 23:45:57
updated: 2018-06-06 23:45:57
---


### **问题描述**

在Windows 10 64位系统下，[免安装MySQL启动3534错误处理][1]解决后，因安装时未配置密码，则按照网上教程在`my.ini`配置文件内的`[mysqld]`项下添加`skip_grant_tables`，控制台使用命令`mysql -u root -p`，进入mysql命令行（参考文章[详见][2]），然而并未像参考文章内描述的那样解决问题，控制台出现如下错误：

![错误1045][3]

---

### **问题处理**

尝试了很多教程均不可以，最后考虑是否是`mysqld --initialize`命令导致的问题，尝试查找[官网的安装教程][4]，发现该命令初始化数据库时，还会自动生成一个随机密码：

![初始化时生成随机密码][5]

然后问题就是随机生成的密码在哪里，这个可以在[官方安装教程]底部看到，明确指出生成的密码在`data`目录下的错误日志里:

![初始化生成随机密码存放在错误日志内][6]

按说明到`data`目录下，可以看到类似下面的错误日志：

![初始化时生成的错误日志][7]

在错误日志内可以查看到对应生成的随机密码：

![初始化生成的随机密码][8]

使用该密码，正常进入mysql命令行模式，之后就可以尝试使用更新语句来更新root账号密码

``` mysql

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';

```

### **问题总结**

在之前配置时出现3534错误，通过`mysqld --initialize`命令来完成初始化，会对应生成随机密码，并会标记`'root'@'localhost'帐户密码`过期，然后在错误日志显示输出随机密码。使用该随机密码，即可以登录mysql命令行模式，然后修改root密码，至此，才算配置完成。

通过官网配置教程，发现还有另外一个命令`mysqld --initialize-insecure`，使用该命令初始化数据库时，不会生成随机密码，而是直接标记`'root'@'localhost'帐户密码`过期，在错误日志内输出类似如下的提示信息：

``` 
[Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```

官方对于两个命令的说明如下：

![两个命令的区别][9]

使用`mysqld --initialize-insecure`命令初始化数据库后，启动服务，直接通过命令`mysql -u root -p`（提示输入密码时直接回车）即可进入mysql命令行模式。

**注意：** 数据库配置文件`my.ini`不需要配置`skip_grant_tables`!



### **参考**

1. [官网免安装配置教程][4]
2. `mysqld --initialize`命令官网[说明][5]
3. `mysqld --initialize-insecure`命令官网[说明][10]
4. [MySQL-深入分析MySQL ERROR 1045出现的原因][2]

  [1]: https://blog.csdn.net/u012995964/article/details/80588977
  [2]: https://blog.csdn.net/qq_28938933/article/details/72872064
  [3]: http://p9uy5dyvc.bkt.clouddn.com/err_1045.png "err_1045.png"
  [4]: http://https://dev.mysql.com/doc/refman/5.7/en/data-directory-initialization-mysqld.html
  [5]: http://p9uy5dyvc.bkt.clouddn.com/mysqld_initialize.png "mysqld_initialize.png"
  [6]: http://p9uy5dyvc.bkt.clouddn.com/random_password.png "random_password.png"
  [7]: http://p9uy5dyvc.bkt.clouddn.com/error_log.png "error_log.png"
  [8]: http://p9uy5dyvc.bkt.clouddn.com/random_password_2.png "random_password_2.png"
  [9]: http://p9uy5dyvc.bkt.clouddn.com/end.png "end.png"
  [10]: https://dev.mysql.com/doc/refman/5.7/en/server-options.html#option_mysqld_initialize-insecure