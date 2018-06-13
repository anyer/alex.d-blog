---
title: C#静态调用带有SoapHeader验证的WebService
copyright: true
categories:
  - C#
  - WebService
tags:
  - C#
  - SoapHeader
  - WebService
description: 本文记录带有SoapHeader验证的WebServices服务创建、部署及C#中的静态调用方法。
date: 2017-01-16 14:28:26
updated: 2017-01-16 14:28:26
---


本文记录带有SoapHeader验证的WebServices服务创建、部署及C#中的静态调用方法，基于 `Windows8.1`、`Visual Studio 2013`、`IIS8` 环境实现。

----------


### **WebServices服务创建**

#### **Visual Studio 2013中创建WebServices**
1. 创建一个空的 `ASP.NET Web 应用程序` ：

![新建空的Asp.net的web应用程序](http://img.blog.csdn.net/20170115154108472?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

2. 创建 WebService 服务的程序（asmx格式）文件：

![添加服务程序文件](http://img.blog.csdn.net/20170115154211968?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
首次右键“添加”时，看不到图中所示的 “Web 服务（ASMX）” ，可以点击“新建项（W）”来实现创建：

![创建ASMX文件1](http://img.blog.csdn.net/20170115154501159?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![创建ASMX文件2](http://img.blog.csdn.net/20170115154519987?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

3. 到此 WebService 服务创建完成，可以看到如下基础代码:

![新建ASMX文件内容](http://img.blog.csdn.net/20170115154640067?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

4. 快捷键 `F5` 或 `ctrl + F5` 运行程序如下：

![VS的IIS Express中运行结果](http://img.blog.csdn.net/20170115154918540?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
此时可以点击页面的 `Hello World` 跳转到基于 `HTTP POST` 协议的调用测试页面 ：

![服务测试](http://img.blog.csdn.net/20170115155438119?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

点击“调用”即可以在新的页面看到返回的结果：

![返回结果](http://img.blog.csdn.net/20170115155624292?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


----------

#### 添加SoapHeader验证
创建基础的WebService服务后，根据需要，有时服务会需要权限来保证安全，这里通过添加SoapHeader验证（即Soap的头信息验证）来实现。
1. 首先需要我们自己去实现一个有身份验证信息的类，这个类继承于 `System.Web.Services.Protocols.SoapHeader` , 代码如下：

``` C#
    /// <summary>
    /// 自定义MySoapHeader类
    /// </summary>
    public class MySoapHeader : System.Web.Services.Protocols.SoapHeader {

        private string userName;
        private string passWord;

        public MySoapHeader() { }
        public MySoapHeader(string userName, string passWord) {
            this.userName = userName;
            this.passWord = passWord;
        }

        public string UserName {
            set {
                userName = value;
            }
            get {
                return userName;
            }
        }
        public string PassWord
        {
            set
            {
                passWord = value;
            }
            get
            {
                return passWord;
            }
        }
    }
```
 
2.修改WebService类

``` C#
	
	/// <summary>
    /// WebService1 的摘要说明
    /// </summary>
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [System.ComponentModel.ToolboxItem(false)]
    // 若要允许使用 ASP.NET AJAX 从脚本中调用此 Web 服务，请取消注释以下行。 
    // [System.Web.Script.Services.ScriptService]
    public class WebService1 : System.Web.Services.WebService
    {
        public MySoapHeader soapHeader;
        
        [WebMethod(Description="SoapHeader验证")]
        [System.Web.Services.Protocols.SoapHeader("soapHeader")]
        public string HelloWorld()
        {
            //简单验证用户信息
            //可以通过数据库或其他方式验证
            if ("admin".Equals(soapHeader.UserName) & "admin123".Equals(soapHeader.PassWord))
            {
                return "用户验证通过！";
            }
            else
            {
                return "对不起，您没有访问权限！";
            }
        }
    }
	
```

至此实现了SoapHeader验证的添加，此处**注意Webservice类中的方法上添加上SoapHeader特性**。即上面代码中的`[System.Web.Services.Protocols.SoapHeader("soapHeader")]`

此处为简单实现，高级实现，可以参考MSDN提供的 [教程文档](https://msdn.microsoft.com/zh-cn/library/9z52by6a%28v=vs.100%29.aspx)


----------


### **WebService服务部署**

#### **WebService服务程序的发布**
编写好的web程序或者服务等，可以通过发布直接部署到服务器。这里没有远程服务器，所以使用本地的IIS服务器来运行WebService服务。发布方式如下：

![服务发布](http://img.blog.csdn.net/20170115181940045?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![自定义发布目标配置文件](http://img.blog.csdn.net/20170115182010921?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![发布方法为文件系统（即本地目录）](http://img.blog.csdn.net/20170115182110952?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
后面两项配置默认即可，此时点击发布按钮，等待控制台显示如下提示，即表示发布成功：

![发布成功](http://img.blog.csdn.net/20170115182839612?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

此时可以在发布的目录中看到如下文件：

![目录内容](http://img.blog.csdn.net/20170115183003465?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### **本地IIS服务部署**
在本地IIS的部署可以参看前文 [Windows8.1中IIS服务安装及站点配置](http://blog.csdn.net/u012995964/article/details/54375074) 中站点部署的部分。

部署后浏览结果如下：

![部署后浏览结果](http://img.blog.csdn.net/20170115224443965?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

----------

### **WebService的调用**

#### **创建客户端**
创建控制台应用程序，用来调用测试。
![创建客户端测试程序1](http://img.blog.csdn.net/20170115195741684?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![创建客户端测试程序2](http://img.blog.csdn.net/20170115195758809?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### **添加引用**
新建完项目后，需要引用WebService服务，用于调用WebService

![添加添加引用](http://img.blog.csdn.net/20170115223203724?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![添加服务引用](http://img.blog.csdn.net/20170115223313599?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

添加完引用后，打开“Program.cs”文件的Main方法中输入以下语句：

``` C#

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestService
{
    class Program
    {
        static void Main(string[] args)
        {
			//创建WebService服务实例		
            MyWebServices.WebService1SoapClient service = new MyWebServices.WebService1SoapClient();
			//创建自定义SoapHeader对象实例
            MyWebServices.MySoapHeader header = new MyWebServices.MySoapHeader();

            //未设置SoapHeader的服务调用
            Console.WriteLine("未设置SoapHeader的服务调用:" + service.HelloWorld(header));
            Console.WriteLine();

            //将用户名与密码存入SoapHeader;
            header.UserName = "admin";
            header.PassWord = "admin123";

            ////设置SoapHeader的服务调用
            Console.WriteLine("未设置SoapHeader的服务调用:" + service.HelloWorld(header));
            
			Console.Read();
        }
    }
}

```

运行后，测试结果如下：

![测试结果](http://img.blog.csdn.net/20170115223549226?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMjk5NTk2NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


**源码：** [C#静态调用带有SoapHeader验证的WebServices](http://download.csdn.net/detail/u012995964/9738700)

----------


### **参考及推荐**
关于Web Services学习，可以看这里：

 - w3school 提供的[系列教程](http://www.w3school.com.cn/ws.asp) 
 - MSDN的[ASP.NET XML Web services 基础知识](https://msdn.microsoft.com/zh-cn/library/a7xexaft%28v=vs.100%29.aspx)

关于IIS Express和本地IIS服务的一些介绍比较，可以看[这里](https://msdn.microsoft.com/zh-cn/library/58wxa9w5%28v=vs.120%29.aspx)































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































































