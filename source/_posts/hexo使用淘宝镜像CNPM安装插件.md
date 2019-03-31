---
title: hexo使用淘宝镜像CNPM安装插件
date: 2019-03-24 14:50:38
tags: 
- 淘宝镜像
- cnpm
categories: 
- hexo
img: https://blog-1252958858.file.myqcloud.com/2019/03/hexo-cnpm.png
newimg: true
comments: true
zhailu: 本文简单介绍下通过cnpm安装hexo锁使用的插件的方法。npm安装插件一直受国内网速的限制很慢，使用cnpm后速度提升很快
---

每次通过npm安装插件都要忍受奇慢无比的网速，后来发现了cnpm，发现速度非常快，特开贴记录

使用方式：

1.首先安装淘宝镜像

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

2.安装模块

```
$ cnpm install [name]
```

name即为插件的名字

例：

```
$ npm install hexo-deployer-ftpsync –save
```

更改后：

```
$ cnpm install hexo-deployer-ftpsync –save
```

淘宝镜像为阿里云产物，服务器架设在国内，当cnpm上没有你需要的插件时，它会自动去npm服务器上寻找同时在保存至cnpm服务器上

> 官方文档：[点我](https://npm.taobao.org/)

