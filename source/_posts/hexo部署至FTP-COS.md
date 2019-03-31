---
title: hexo部署至FTP-COS
date: 2019-03-24 15:13:38
tags: 
- hexo部署至FTP
- hexo部署至COS
categories: 
- hexo
img: https://blog-1252958858.file.myqcloud.com/2019/03/hexo-ftp-cos.png
newimg: true
comments: true
zhailu: hexo部署至FTP服务器和腾讯云cos的方法，除了部署至github和coding等主流的服务器上，还可以有更多的选择
---

主流的部署方式一般都是github、coding、码云、七牛

但是其实也可以有更多的选择，比如FTP服务器和腾讯云COS

## 部署至FTP服务器：

一般有自己的服务器的都喜欢搭建在自己的服务器上，因为主流的服务器都是有不稳定的因素在，时长崩溃，自己有服务器，做个FTP用来存文件也是不错的选择，顺便放放hexo也算物尽其用

### 1.安装插件

```
$ npm install hexo-deployer-ftpsync –save
```

### 2.修改配置

根目录下config.yml增加以下：

```
deploy:
  type: ftpsync #上传方式，固定ftpsync
  host: hfanss.ftp-gz01.com #ftp地址
  user: ****	#帐号
  pass: ****	#密码
  remote: /webroot/ #上传至哪个目录
  port: 8010	#端口
```

## 部署至腾讯云COS：

### 1.安装插件：

```
$ npm install hexo-deployer-cos --save
```

### 2.修改配置：

```
deploy:
 type: cos	#上传方式，固定cos
 appId: 12529*****  #cos的appId
 secretId: AKIDa0CAuP5hW6***********  #cos的secretId
 secretKey: ********** #cos的secretKey
 bucket: *********  #cos的bucket
 region: ap-shanghai  #cos的region
```

## 部署至多个地址：

```
deploy:
   -type: cos
    appId: ***
   -type: git
    repository: *****   #git地址 
  	branch: master
   -type: git
    repository: *****   #git地址 
  	branch: master
   -type: ftpsync
    host: hfanss.ftp-gz01.com
    ....
```

npm安装不成功使用[cnpm](https://hfanss.com/2019/hexo%E4%BD%BF%E7%94%A8%E6%B7%98%E5%AE%9D%E9%95%9C%E5%83%8FCNPM%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6.html)

> 记录贴，大神勿喷！