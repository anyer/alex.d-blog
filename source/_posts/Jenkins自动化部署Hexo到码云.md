---
title: Jenkins自动化部署Hexo到码云
categories:
  - 安装部署
tags:
  - Jenkins
  - 自动化
  - 部署
  - Hexo
  - 码云
copyright: true
description: 使用自动化服务Jenkins实现Hexo博客的自动化部署到码云上
abbrlink: de4655d2
date: 2018-06-12 21:12:27
updated: 2018-06-12 21:12:27
---

### **开发环境**

本文基于Windows10 64位系统，Node.js  `v8.11.2`， npm `v5.6.0`， Hexo  `v3.7.1`， Jenkins  `v2.121.1`， JDK `v1.8.0_171` ， Tomcat版本

#### Node.js环境

- Node官网[下载][1]Windows安装包进行安装

![node_download][2]

![node_version][3]

- 在nvm的github地址内[下载][4]最新版Node版本管理工具nvm

![nvm_download][5]

![nvm_version][6]

> nvm命令使用等更多内容参看[这里][7]

- 通过命令 `npm install -g nrm`安装npm registry 管理工具



> **注**： 可以通过 `npm install -g cnpm` 命令安装淘宝定制的cnpm来代替npm

#### Hexo博客
#### Jenkins


  [1]: https://nodejs.org/zh-cn/download/
  [2]: http://p9uy5dyvc.bkt.clouddn.com/node_download.png "node_download.png"
  [3]: http://p9uy5dyvc.bkt.clouddn.com/node_version.png "node_version.png"
  [4]: https://github.com/coreybutler/nvm-windows/releases
  [5]: http://p9uy5dyvc.bkt.clouddn.com/nvm_download.png "nvm_download.png"
  [6]: http://p9uy5dyvc.bkt.clouddn.com/nvm_version.png "nvm_version.png"
  [7]: https://github.com/coreybutler/nvm-windows