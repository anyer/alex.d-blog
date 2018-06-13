---
title: Hexo执行清理命令出现警告DEP0061
copyright: true
categories:
  - 问题处理
tags:
  - hexo
  - error
description: Hexo执行清理命令时，提示警告DEP0061.
abbrlink: 932be761
date: 2018-06-12 16:02:57
updated: 2018-06-12 16:02:57
---

### **问题描述**

Win10 64位系统下，Node.js版本 `v8.11.2` 。本地安装部署Hexo执行 `hexo clean` 命令时出现如下警告：

![warning dep0061][1]

---

### **问题处理**
经过查找，因本地Node.js版本为 `v8.11.2` ,而 `fs.SyncWriteStream` 在 `Node.js 8` 中已经被废弃

![node8_fs_SyncWriteStream][2]

而在Hexo的插件 `Hexo-tag-cloud` 依赖 `hexo-fs` 及 `hexo-log` ， 而 `hexo-fs` 需要 `Node.js 6` 的支持。

![hexo-tag-cloud_dependencies][3]

![hexo-fs_config][4]

此处是Node.js版本不支持导致出现警告。可以尝试切换Node.js版本来处理，Node.js版本控制参看[此处][5]。

---

### **问题总结**

- 在Hexo命令执行过程中，如出现问题，可以通过 `--debug` 查看问题，如：

``` bash
$ hexo clean --debug
11:48:34.559 DEBUG Hexo version: 3.7.1
11:48:34.559 DEBUG Working directory: D:\work\000\blog\
11:48:34.684 DEBUG Config loaded: D:\work\000\blog\_config.yml
11:48:34.746 DEBUG Plugin loaded: hexo-algolia
11:48:34.777 DEBUG Plugin loaded: hexo-deployer-git
11:48:34.777 DEBUG Plugin loaded: hexo-fs
11:48:34.777 DEBUG Plugin loaded: hexo-generator-archive
11:48:34.793 DEBUG Plugin loaded: hexo-generator-baidu-sitemap
11:48:34.793 DEBUG Plugin loaded: hexo-generator-category
11:48:34.793 DEBUG Plugin loaded: hexo-generator-index
11:48:34.824 DEBUG Plugin loaded: hexo-generator-feed
11:48:34.824 DEBUG Plugin loaded: hexo-generator-searchdb
11:48:34.840 DEBUG Plugin loaded: hexo-generator-sitemap
11:48:34.840 DEBUG Plugin loaded: hexo-generator-tag
11:48:34.840 DEBUG Plugin loaded: hexo-log
11:48:34.840 DEBUG Plugin loaded: hexo-renderer-ejs
11:48:34.856 DEBUG Plugin loaded: hexo-renderer-marked
11:48:34.856 DEBUG Plugin loaded: hexo-renderer-stylus
11:48:34.965 DEBUG Plugin loaded: hexo-server
11:48:34.981 DEBUG Plugin loaded: hexo-tag-cloud
(node:696) [DEP0061] DeprecationWarning: fs.SyncWriteStream is deprecated.
11:48:35.043 DEBUG Plugin loaded: hexo-wordcount
11:48:35.074 DEBUG Script loaded: themes\next\scripts\merge-configs.js
11:48:35.074 DEBUG Script loaded: themes\next\scripts\tags\button.js
11:48:35.074 DEBUG Script loaded: themes\next\scripts\tags\exturl.js
11:48:35.074 DEBUG Script loaded: themes\next\scripts\tags\center-quote.js
11:48:35.074 DEBUG Script loaded: themes\next\scripts\tags\full-image.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\merge.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\tags\label.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\tags\group-pictures.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\tags\note.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\tags\lazy-image.js
11:48:35.090 DEBUG Script loaded: themes\next\scripts\tags\tabs.js
11:48:35.090 INFO  Deleted database.
11:48:35.090 DEBUG Database saved

```

通过输出，可以发现在加载 `hexo-tag-cloud` 插件时出现的问题，快速的定位到了错误，方便问题的排查。

- 因Node.js的快速发展，版本迭代快速，而部分插件因各种因素，并未同步更新，使得使用过程中，会出现不少因版本不符导致的问题，所以在开发过程中，就需要对Node.js的多个版本进行管理，这时就需要一个趁手的工具，此处推荐几款Node.js版本管理工具，如下（排列不分先后，部分工具的对比及使用说明见[此处][6]）：

> - [n][7]
> - [nvm][8]
> - [wnvm][9]
> - [nodist][10]
> - [gnvm][11] 

---




### **参考**

1. [Node.js 8 说明][12]
2. [基于Hexo+Github+Coding搭建个人博客——基础篇(从菜鸟到放弃)][13]


  [1]: http://p9uy5dyvc.bkt.clouddn.com/warning_DEP0061.png "warning_DEP0061.png"
  [2]: http://p9uy5dyvc.bkt.clouddn.com/node8_fs_SyncWriteStream.png "node8_fs_SyncWriteStream.png"
  [3]: http://p9uy5dyvc.bkt.clouddn.com/hexo-tag-cloud_dependencies.png "hexo-tag-cloud_dependencies.png"
  [4]: http://p9uy5dyvc.bkt.clouddn.com/hexo-fs_config.png "hexo-fs_config.png"
  [5]: https://blog.csdn.net/lpf1215/article/details/52843523
  [6]: https://blog.csdn.net/lpf1215/article/details/52843523
  [7]: https://www.npmjs.com/package/n
  [8]: https://github.com/coreybutler/nvm-windows
  [9]: https://www.npmjs.com/package/wnvm
  [10]: https://github.com/marcelklehr/nodist
  [11]: https://github.com/Kenshin/gnvm
  [12]: http://alinode.aliyun.com/blog/42
  [13]: http://yangbingdong.com/2017/build-blog-hexo-base/