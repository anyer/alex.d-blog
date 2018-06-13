---
title: Windows下PHP配置成功后phpinfo中找不到MySQL问题处理
copyright: true
categories:
  - 问题处理
tags:
  - Windows 8.1
  - PHP
  - MySQL
  - Error
description: 本文记录Windows下PHP配置成功后phpinfo中找不到MySQL情况的处理。
date: 2016-02-17 22:54:42
updated: 2016-02-17 22:54:42
---

### **问题描述**
本地配置php开发环境（Apache + PHP + MySQL）后，测试时 phpinfo中找不到mysql
![这里写图片描述](http://img.blog.csdn.net/20160217223619021)
且此时PHP的测试程序怎么也连不上数据库，并报`Call to undefined function mysql_connect()` 的错误。

---

### **问题解决**
检测配置文件

- Apache
Apache的配置文件`apache安装路径/conf/httpd.conf`	中检测以下内容
```
[httpd.conf]

	LoadModule php5_module "D:/php/php-5.4.45/php5apache2_2.dll"
	PHPIniDir "D:/php/php-5.4.45/php.ini"
	AddType application/x-httpd-php .php .html .htm
	DocumentRoot "F:/php"
```

> **注意**：PHP的配置文件php.ini应该在PHPIniDir路径下
	 
- PHP
PHP配置文件`php安装路径/php.ini` 中检测下面内容
```
[php.ini]

	extension=php_curl.dll
	extension=php_gd2.dll
	extension=php_imap.dll
	extension=php_mbstring.dll
	extension=php_mysql.dll
	extension=php_mysqli.dll
	extension=php_pdo_mysql.dll
	extension=php_snmp.dll
	extension=php_soap.dll
	extension=php_sockets.dll

	doc_root = "F:/php"
	extension_dir = "D:/php/php-5.4.45/ext"
	session.save_path = "D:/php/php-5.4.45/tmp"

```
检测上面extension内容是否去掉了注释，且doc_root等配置路径是否正确。

- MySQL
在MySQL目录中找到`mysql安装目录/lib/libmysql.dll` 文件，将此文件复制到系统的system32下，基本就解决了上述问题。

----------

最后，保存修改的文件，重启Apache服务，重新运行，此时可以在phpinfo文件中找到mysql了
![这里写图片描述](http://img.blog.csdn.net/20160217225342731)











































