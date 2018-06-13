---
title: WAMP(Windows + Apache + MySQL + PHP) 环境配置
copyright: true
categories:
  - 安装部署
tags:
  - MySQL
  - Windows
  - Apache
  - PHP
description: 本文记录WAMP环境配置。
abbrlink: f06be05a
date: 2016-08-01 12:23:05
updated: 2016-08-01 12:23:05
---


### **WAMP(Windows + Apache + MySQL + PHP) 环境配置**

wamp集成环境的下载地址：[http://www.wampserver.com/](http://www.wampserver.com/)，集成环境安装这里不做记录，本文仅记录Windows+Apache+MySQL+PHP集成环境的配置。

- 各模块下载地址
> Apache：http://httpd.apache.org/docs/current/platform/windows.html
> MySQL：http://dev.mysql.com/downloads/mysql/5.0.html#win32
> PHP：http://windows.php.net/download

- 独立安装各模块顺序:
> Apache -> PHP -> MySQL

#### **Apache服务安装**
下载Apache，上面给出的地址是免安装版，用命令行配置可以更加清晰地看到错误信息，方便于调试。

![Downloading Apache for Windows](http://img.blog.csdn.net/20160801120856209)

进入下载链接之后有如上的几个下载地址，我们选择第一个。点击进入，就可以看到最终的下载位置，按你的操作系统选择下载32位或64位：

![apache download](http://img.blog.csdn.net/20160801120959726)

下载完成后，将下载的压缩包解压到`D:\PHP\ ` 目录（目录可以自定义，注意不适用中文） 下，然后命令提示符(管理员模式，非管理员模式进入安装时提示权限问题)进入bin目录下，输入命令：`httpd –k install`

![httpd -k install](http://img.blog.csdn.net/20160801121059401)
执行命令后会发现，**Apachefu service is successfully installed.**
但会发现下面出现错误，这里是ServerRoot目录指向没有配置。打开`../ApacheXX/conf/`目录下的httpd.conf，并定位到ServerRoot，配置当前的apache目录：

![ServerRoot](http://img.blog.csdn.net/20160801121224277)

然后在命令提示符中使用命令`httpd -k uninstall` 先卸载服务，然后再执行`httpd –k install`命令来安装服务，最后执行`httpd –k start`命令来测试。

浏览器中输入`http://localhost/` 出现类似下面含有 **it works** 字样提示的页面，表示安装完成

![It Works](http://img.blog.csdn.net/20160801121425981)

如果不成功，可能是本地80端口被占用，可以到 `../ApacheXX/conf/` 目录中的httpd.conf文件里，将所有80的端口改成8080，再次输入`http://localhost/`，如果出现类似上图提示，表示安装成功。

#### **PHP环境安装**
下载PHP，注意选择有**Thread Safe**的版本，php位数根据系统位数选择：
![php download](http://img.blog.csdn.net/20160801124525073)
同样，将下载的压缩包解压到D:\PHP\ 目录下，方便环境配置。之后将php.ini-development文件修改为php.ini。然后用文本编辑器打开编辑 （不建议使用记事本）,定位到extension_dir，将：
> ; extension_dir = "./"

修改为：
> extension_dir = "D:/PHP/php5.6.24/ext"

![extension_dir](http://img.blog.csdn.net/20160801121544481)

定位到date.timezone修改时区
> date.timezone = RPC 或date.timezone = Asia/Shanghai

![date.timezone](http://img.blog.csdn.net/20160801121659075)

定位到default_charset修改编码格式
> default_charset ="UTF-8"

然后修改如下内容：
``` php
;extension=php_bz2.dll
extension=php_curl.dll
;extension=php_fileinfo.dll
extension=php_gd2.dll
;extension=php_gettext.dll
;extension=php_gmp.dll
;extension=php_intl.dll
extension=php_imap.dll
;extension=php_interbase.dll
;extension=php_ldap.dll
extension=php_mbstring.dll
;extension=php_exif.dll      ; Must be after mbstring as it depends on it
extension=php_mysql.dll
extension=php_mysqli.dll
;extension=php_oci8_12c.dll  ; Use with Oracle Database 12c Instant Client
;extension=php_openssl.dll
;extension=php_pdo_firebird.dll
extension=php_pdo_mysql.dll
;extension=php_pdo_oci.dll
;extension=php_pdo_odbc.dll
;extension=php_pdo_pgsql.dll
;extension=php_pdo_sqlite.dll
;extension=php_pgsql.dll
;extension=php_shmop.dll

; The MIBS data available in the PHP distribution must be installed.
; See http://www.php.net/manual/en/snmp.installation.php
extension=php_snmp.dll

extension=php_soap.dll
extension=php_sockets.dll
;extension=php_sqlite3.dll
;extension=php_sybase_ct.dll
;extension=php_tidy.dll
;extension=php_xmlrpc.dll
;extension=php_xsl.dll
```
即去掉；号（去除注释）来实现php扩展的引入，如下图:

![php.ini extension](http://img.blog.csdn.net/20160801121818972)

最后将`D:\PHP\php5.6.24;D:\PHP\php5.6.24\ext `添加到环境变量

#### **MySQL安装**

MySQL的安装可以看 [Windows 7系统安装MySQL5.5.21图解](http://blog.csdn.net/longyuhome/article/details/7913375)
。注意修改安装路径到`D:\PHP\ `


### **整合Apache、MySQL、PHP**
- **Apache**
打开 `..\Apache2.x\conf\httpd.conf `文件，添加如下信息：

``` http.conf

#添加PHP的php.ini配置文件目录
PHPIniDir "D:/PHP/php5.6.24/php.ini"

#加载PHP编译模块，注意Apache2.4需要与php5apache2_4.dll配合，否则Apache Server启动时加载出错。
LoadModule php5_module "D:/PHP/php5.6.24/php5apache2_4.dll"

#设置的PHP支持的文件解析
<IfModule mime_module>
...
AddType application/x-httpd-php .php .html .htm
...
</IfModule>

#修改网站根目录（此处按自己需要修改，默认为Apache下的htdocs目录）
DocumentRoot "D:/PHP/develop"
#修改DocumentRoot 同时要修改其下面的Directory标签名后的地址（两者需要统一）
<Directory "D:/PHP/develop">

# 添加默认文档类型 （此处按自己需求修改）
<IfModule dir_module> 
#默认为index.html                   
DirectoryIndex index.html index.php    
</IfModule>

#修改监视端口为8008或其它，避免与IIS的80端口冲突，导致无法启动Apache Server （本地开发学习，可不做修改，视情况而定）
Listen 8008
ServerName localhost:8008

```

- **PHP**
打开`..\php5.x\php.ini `文件，配置如下信息：

```php.ini

doc_root = "D:/PHP/develop"
session.save_path = "D:/php/php-5.4.45/tmp"

```

- **MySQL**
在MySQL目录中找到mysql安装目录 `/lib/libmysql.dll `文件，将此文件复制到系统的system32目录下

至此，环境配置完成，可以在工程目录下（本文目录为`D:/PHP/develop `），创建index.php页面，页面中写入：
```php

<?php
    phpinfo();
?>

```
启动服务，浏览器中输入`http://localhost/index.php `，出现如下页面，说明配置完成：

![phpinfo](http://img.blog.csdn.net/20160801121853926)





































































































