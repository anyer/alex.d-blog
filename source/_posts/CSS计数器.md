---
title: CSS计数器
copyright: true
categories:
  - CSS
tags:
  - CSS3
description: 本文记录CSS的计数器的属性及使用。
date: 2016-07-09 16:44:51
updated: 2016-07-09 16:44:51
---


### **CSS计数器（counter）**

#### **CSS计数器属性**
|属性|属性说明|语法|参数含义|
|:--|:--|:--|:--|
|counter-reset|定义计数器，包括初始化、作用域等|**counter-reset**:<br />[&lt;identifier&gt;&lt;integer&gt;?]+/none/inherit|默认值为none<br />&lt;identifier&gt;:计数器名称<br />&lt;integer&gt;:计数器初始值<br />当元素的display为none时，该属性失效|
|counter-increment|设置计数器的增数|**counter-increment**:<br />[&lt;user-ident&gt;&lt;integer&gt;?]+/none|&lt;user-ident&gt;:需要增数的计数器名称<br />&lt;integer&gt;:计数器增数的值，可以为负数<br />可以同时增数多个计数器<br />当元素的display为none时，该属性失效|
|content|在::before和::after中生成内容|**content**:[&lt;counter&gt;]+<br/>**&lt;counter&gt;**=<br />counter(name)/<br/>counter(name,list-style-type)/<br/>counters(name,string)/<br/>counters(name,string，list-style-type)|使用计数器，需要结合::befer和::after使用。可以同时使用多个计数器|
|counter()|在content属性中使用，用来调用计数器| | |
|@counter-style|自定义列表样式|**@counter-style counterStyleName**{<br/>system:算法;<br/>range:使用范围;<br/>symbols:符号;or additive-symbols:符号;<br/>prefix:前缀;suffix:后缀;<br/>pad:补零(eg.01,02,03);<br/>nagative:负数策略;<br/>fallback:出错后的默认值;<br/>speakas:语音策略;}|@counter-style cjk-heavenly-stem{<br />system:alphabetic;<br />symbols:"\7532""\4E59""\4E19""\4E01";<br /> /* 甲 乙 丙 丁 */<br />suffix:"、";}|

#### **CSS计数器属性代码示例**
|属性|代码|代码解析|
|---|:-----|:-----|
|counter-reset|counter-reset:counterA;<br />counter-reset:counterA 6<br />counter-reset:counterA 4 counterB;<br />counter-reset:counterA 4 counterB 2;|定义定时器counterA,初始值为默认值0<br />定义定时器counterA,初始值为6<br />定义定时器counterA、counterB,初始值分别为4和0<br />定义定时器counterA、counterB,初始值分别为4和2|
|counter-increment|counter-increment:counterA<br />counter-increment:counterA 2<br />counter-increment:counterA 2 counterB -1<br />|增数计算器counterA,每次增加1<br />增数计算器counterA,每次增加2<br />增数计算器counterA、counterB,每次分别增加2、-1|
|content|content:"Fig." counter(imgCounter);<br/>content:"Fig." counter(imgCounter,lower-alpha);<br/>contents(section,".")"";<br/> contents(section,".","lower-roman")"";|混合字符串和计数器imgCounter<br /> 指定计数器的列表格式<br />在计数器之间加上点号，同时在计数器最后添加一个空格<br />定义计数器为小写罗马数字格式，同时加点好，空格|


----------

### **CSS计数器应用**
![css counter](http://img.blog.csdn.net/20160709155729034)
通过CSS计数器功能即实现上图左侧到右侧的效果。

``` html
	<ul class="title">
		<li>一级标题
			<ul class="title2">
				<li>二级标题
					<ul>
						<li>三级标题</li>
						<li>三级标题</li>
						<li>三级标题</li>
					</ul>
				</li>
				<li>二级标题
					<ul>
						<li>三级标题</li>
						<li>三级标题</li>
						<li>三级标题</li>
					</ul>
				</li>
				<li>二级标题
					<ul>
						<li>三级标题</li>
						<li>三级标题</li>
						<li>三级标题</li>
					</ul>
				</li>
			</ul>
		</li>
		<li>一级标题
			<ul class="title2">
				<li>二级标题</li>
				<li>二级标题</li>
				<li>二级标题</li>
			</ul>
		</li>
		<li>一级标题
			<ul class="title2">
				<li>二级标题</li>
				<li>二级标题</li>
				<li>二级标题</li>
			</ul>
		</li>
	</ul>

```

```CSS3
		
	ul {
		list-style: none;	
	}
	.title {
		counter-reset: A_title B_title C_title;
		font-size: 18px;
		font-weight: bold;
		font-family: '宋体';
	}
	.title > li:before {
		counter-increment: A_title ;
		content: counter(A_title)"、";
	}
	.title .title2 > li {
		font-size: 14px;
		font-weight: 500;
	}
	.title .title2 > li:before {
		counter-increment: B_title;
		content: counter(A_title)"."counter(B_title)"、";
	}
	.title .title2 ul > li {
		font-size: 10px;
	}
	.title .title2 ul > li:before {
		counter-increment: C_title;
		content: counter(A_title)"."counter(B_title)"."counter(C_title)"、";
	}

```


----------

### **阅读参考&扩展阅读**

>  [CSS计数器(序列数字字符自动递增)详解](http://www.zhangxinxu.com/wordpress/2014/08/css-counters-automatic-number-content/)
>  [使用CSS计数器](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Counters)
>  [CSS Counter Styles Level 3](https://drafts.csswg.org/css-counter-styles/)
>  [CSS计数器实现数值计算小游戏demo](http://www.zhangxinxu.com/study/201412/css-counters-number-game.html)