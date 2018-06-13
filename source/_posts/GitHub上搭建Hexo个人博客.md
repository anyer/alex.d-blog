---
title: GitHub上搭建Hexo个人博客
copyright: true
categories:
  - Hexo
  - 安装部署
tags:
  - Node.js
  - Hexo
  - GitHub
description: 本文记录GitHub Pages搭建Hexo静态博客过程及Hexo主题优化。
abbrlink: 9b9a6ada
date: 2015-12-05 00:04:39
updated: 2015-12-05 00:04:39
---

----------

### Hexo介绍
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

<!--more-->
- 风一般的速度
Hexo基于Node.js，支持多进程，几百篇文章也可以秒生成。
- 流畅的撰写
支持GitHub Flavored Markdown和所有Octopress的插件。
- 扩展性
Hexo支持EJS、Swig和Stylus。通过插件支持Haml、Jade和Less.

----------

### Hexo安装
#### **安装前提**

- [Node.js][1]
- [Git][2]
在安装Hexo前，需要确定以上条件是否满足！具体安装步骤不在赘述。

#### **搭建环境**
- [GitHub账号][3]
- 创建新的github仓库
    ![创建仓库](http://img.blog.csdn.net/20151203134110566)
- 获得github仓库地址
    ![获得github仓库地址](http://img.blog.csdn.net/20151203134701461)
- 安装[GitHub for Windows 客户端][4]
	    
	使用GitHub for Windows 客户端一个是因为不用配置ssh，另外就是使用较方便。
	    
- 验证ssh
```
    ssh -T git@github.com
```
    出现如下提示，则表示ssh配置完成了。
![验证ssh](http://img.blog.csdn.net/20151203100653106)
- Clone新建的github仓库到本地
![clone仓库到本地](http://img.blog.csdn.net/20151203134817365)
    
    **提示**：如果出现问题，请卸载 GitHub for Windows 客户端，重新安装一遍，或转到使用 [Git 方法](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)
	常见错误请参考：
	
	> [GitHub Help - Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys/)
	> [GitHub Help - Error Permission denied (publickey)](https://help.github.com/articles/error-permission-denied-publickey/)

#### **Hexo安装**
- 选择本地github仓目录（我的地址为F:\github\anyerblog.github.io），在anyerblog.github.io目录上右击菜单中选择git bash Here,打开git终端。输入如下代码：（**注**：右键菜单没有选项，则在开始菜单中，找到github程序文件夹，打开git bash，之后cd到github仓目录）
   ``` 
       npm install -g hexo
   ```
  
- 检查是否安装
       安装完成后通过`hexo version`查看安装的hexo版本信息
    ![hexo版本信息](http://img.blog.csdn.net/20151203135008066)
    
    
#### **hexo创建**
- 在git bash中输入以下命令，完成hexo的创建:
``` bash
    $ hexo init
```
![hexo init](http://img.blog.csdn.net/20151203135056680)
- 将hexo相关的插件安装到githut仓库目录中 
``` bash
	$ npm install
```
	此时github仓库目录内容如下：(搭建完成后补的图，里面会比实际情况多文件夹)
![添加node_modules目录](http://img.blog.csdn.net/20151203135312071)



----------

### Hexo运行
#### **生成静态页面**
	安装好hexo后，通过下面代码可以生成静态页面，生成的静态页面存储在public目录下:
``` bash
	$ hexo generate  #可简写为`hexo g`	
```

#### **运行服务**
开启预览访问端口（默认端口4000，git bash下 'ctrl + c' 关闭server）
``` bash
	$ hexo server  #可简写为`hexo s`
```

	运行后出现下图结果，则表示服务已启动：
![运行服务](http://img.blog.csdn.net/20151203135516846)
此时在浏览器中访问http://localhost:4000/ ，即可看到hexo自带的hello world 页面
![hexo页面](http://img.blog.csdn.net/20151202210921585)
至此，hexo已经在本地搭建完成。


----------

### NexT主题
#### **修改主题**
hexo默认使用的是landscape主题，下文将采用NexT主题。
- NexT主题
	NexT主题特色：精于心，简于形
	NexT主题是我接触Hexo的第一款主题，一见钟情的一款Hexo主题。
	NexT主题简约却并不简单，功能特性多样；响应式设计，电脑手机访问体验好，超级nice，你值得拥有！	


- 安装主题
将next的代码clone到项目中，保存在github仓库中的`themes/next`目录下:
``` bash
	$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```


- 修改配置
下载完主题后，修改根目录下的_config.yml配置文件：
![配置文件中修改主题](http://img.blog.csdn.net/20151203135907094)
新建的hexo文件中使用的是默认的主题landscape，将其修改为next（next为主题安装的目录名`themes/next`）
	

- 运行新主题
	修改完成后保存，运行代码：
	``` bash
		$ hexo server -g  #为`hexo generate`及`hexo server`的缩写
	```
	
此代码运行吼，NexT的主题页面如下：
![NexT主题页面](http://img.blog.csdn.net/20151202213709271)


#### **主题设置**
- 添加blog名称及副标题
   修改根目录下配置文件_config.yml
   ![添加blog名称](http://img.blog.csdn.net/20151202220352441)

- 修改语言
	
	修改根目录下的_config.yml文件：
![修改页面语言](http://img.blog.csdn.net/20151202220501344)	

- 更改主题方案
	NexT 通过 Scheme 提供主题中的主题。 Mist 是 NexT 的第一款 Scheme。启用 Mist 仅需在 主题配置文件 中将 #scheme: Mist 前面的 # 注释去掉即可。

	修改`themes/next`目录下的_config.yml文件：
	![主题方案设置](http://img.blog.csdn.net/20151203140120654)	

- 头像设置
通过avatar字段设置，站点外头像设置`avatar：图片url`，站点内头像设置`avatar：目录/图片名.图片格式`

	在根目录下的_config.yml文件中，添加avatar字段：
![头像设置](http://img.blog.csdn.net/20151203140225306)	
头像图片存储在`themes/next/source/images/`目录下。

#### **添加页面**
	
- 标签云页面 
	``` bash
		hexo new page tags	
	```
	修改刚创建的tags文件夹(`github仓库目录\source\tags`)下的index.md文件：
![标签与页面设置](http://img.blog.csdn.net/20151203140405938)
	在`themes/next`目录下的_config.yml文件中，将 menu关键字 中 about 前面的注释去掉即可
	
- 分类页面
	``` bash
		hexo new page categories
	```
	修改刚创建的categories文件夹(`github仓库目录\source\categories`)下的index.md文件：
	![分类页面设置](http://img.blog.csdn.net/20151203140747062)	
	在`themes/next`目录下的_config.yml文件中，将 menu关键字 中 about 前面的注释去掉即可
	
- about页面
	``` bash
		hexo new page about
	```
	在`themes/next`目录下的_config.yml文件中，将 menu关键字 中 about 前面的注释去掉即可
	![菜单设置](http://img.blog.csdn.net/20151203140833816)

- 404页面
	腾讯公益404页面使用方法，新建 404.html 页面，放到主题的 source 目录下(`themes/next/source`)，内容如下：

	``` html

		<!DOCTYPE HTML>
		<html>
		<head>
		  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
		  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
		  <meta name="robots" content="all" />
		  <meta name="robots" content="index,follow"/>
		</head>
		<body>
		
		<script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8" homePageUrl="your site url " homePageName="回到我的主页"></script>
		
		</body>
		</html>

	```
		

#### **第三方插件配置**
- 多说配置
登录多说后，点击我要安装：
![多说页面](http://img.blog.csdn.net/20151203141043112)
然后按下图填写自己的信息：
![多说配置](http://img.blog.csdn.net/20151203141144827)
在`themes/next`目录下的_config.yml文件中，修改duoshuo_shortname关键字：
![配置多说](http://img.blog.csdn.net/20151203141340958)

- 百度统计配置
登录百度统计，添加统计网站后，获得下面的定位代码，将baidu_analytics字段设置为下面代码中hm.js？后面的代码（本文为43d55965147dc8e978f7b55a19736357，注意自己的这个代码）。
```
	<script>
		var _hmt = _hmt || [];
		(function() {
		  var hm = document.createElement("script");
		  hm.src = "//hm.baidu.com/hm.js?43d55965147dc8e978f7b55a19736357";
		  var s = document.getElementsByTagName("script")[0]; 
		  s.parentNode.insertBefore(hm, s);
		})();
	</script>	
```
	获得上面的代码后，在`themes/next`目录下的_config.yml文件中，修改baidu_analytics关键字：
![百度统计配置](http://img.blog.csdn.net/20151203141448376)	

- JiaThis分享配置
在`themes/next`目录下的_config.yml文件中，修改baidu_analytics关键字：
	![jiathis配置](http://img.blog.csdn.net/20151203003603950)

- RSS配置
配置RSS，在此之前需要使用 hexo-generator-feed 插件生成 Feed。此时设置rss:，rss值为空的时，默认会使用站点的 Feed 链接。
```
	npm install hexo-generator-feed --save
```
	通过上述代码，生成feed，此时在`themes/next`目录下的_config.yml文件中修改：
![rss设置](http://img.blog.csdn.net/20151202230528241)

#### **添加github绶带**

	通过下面链接，可以获得各种样式的绶带源码，更具自己需要获取：
> [GitHub Ribbons](https://github.com/blog/273-github-ribbons)
	
获取源码后，修改`anyer.github.io\themes\next\layout`目录下的_layout文件：

![绶带设置](http://img.blog.csdn.net/20151203142652048) 

将绶带的代码，添加在`</body>`上方即可。


完成以上步骤后，运行效果：
![页面效果](http://img.blog.csdn.net/20151203004338338)
插件效果：
![插件效果](http://img.blog.csdn.net/20151203004402158)


----------
### GitHub部署
#### **部署设置**
修改根目录下的_config.yml文件：
![这里写图片描述](http://img.blog.csdn.net/20151203123311507)
#### **部署**
```
	hexo clean
	hexo generate  
	hexo deploy
```
- hexo命令

	- 常用命令：
	hexo new "postName" #新建文章
	hexo new page "pageName" #新建页面
	hexo generate #生成静态页面至public目录
	hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
	hexo deploy #将.deploy目录部署到GitHub

	- 常用复合命令：
	hexo deploy -g
	hexo server -g

	- 简写：
	hexo n == hexo new
	hexo g == hexo generate
	hexo s == hexo server
	hexo d == hexo deploy

	部署成功提示如下：
![部署成功](http://img.blog.csdn.net/20151203125204110)

#### **部署注意事项**
- github仓库地址有两种，分别为https和SSH，在配置_config.yml文件时，注意区分。
- 使用https地址时，部署hexo时，会出现如下选项
![https地址提交](http://img.blog.csdn.net/20151203130054286)

- 使用SSH提交时，github for windows可能会出错，具体解决见上文。
-  部署完成后，使用xxx.github.com访问时，可能会出现404页面：
![404](http://img.blog.csdn.net/20151203132425708)
  
  若之前操作没有报错，则此时可能是由于解析未完成，等一段时间登录即可；也可能是邮箱没有验证通过（我的就是这个问题吧。。。）。


----------
### 引用参考

> [github地址][5]
> [中文官网地址][6]
> [Next 官网](http://theme-next.iissnan.com/)
> [Next GitHub](https://github.com/iissnan/hexo-theme-next)
> [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed) 
> [Hexo搭建Github静态博客](http://www.cnblogs.com/zhcncn/p/4097881.html)
> [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
> [Windows下一步步搭建自己的独立博客——使用 GitHub Pages + Hexo 基础教程（一）](http://www.jianshu.com/p/985d07d88ef4)


  [1]: http://nodejs.org/
  [2]: http://git-scm.com/
  [3]: https://github.com
  [4]: https://desktop.github.com/
  [5]: https://github.com/hexojs/hexo
  [6]: https://hexo.io/zh-cn/