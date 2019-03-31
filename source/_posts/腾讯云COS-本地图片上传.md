---
title: 腾讯云COS图床制作
date: 2018-08-13 20:29:38
tags: 
- 腾讯云COS图床
categories: 
- hexo
img:  https://blog-1252958858.file.myqcloud.com/2018/12/upload_ee8ca2_167d9ee016e__8000_00000019.jpg
newimg: false
zhailu: 利用腾讯云COS实现本地图片上传腾讯云，并将URL返回在剪切板中,实现简单的本地图床，而且是免费的
---
> 在图片上右键上传，自动生成`图片URL`到剪切板中，任意地方`Ctrl+v`均可粘贴
> 
> 在文件上右键上传，自动生成`图片URL`到剪切板中，任意地方`Ctrl+v`均可粘贴

## 准备工作

### COS

> 对象存储（Cloud Object Storage，COS）

我们需要一个空间，用于存放图片或者文件，这里推荐使用腾讯云或者七牛云

他们提供的免费额度足够普通用户使用了

腾讯云的免费额度

| 资源类型 | 资源子类型          | 每月免费额度 |
| -------- | ------------------- | ------------ |
| 存储空间 | 存储空间            | 50 GB        |
| 流量     | 外网下行流量        | 10 GB        |
| 流量     | 腾讯云 CDN 回源流量 | 10 GB        |
| 请求     | 读请求              | 100 万次     |
| 请求     | 写请求              | 100 万次     |

### 本地环境

这里以腾讯云接口为例，本地需要`nodejs`运行环境

- [nodejs](https://nodejs.org/en/download/)

- [腾讯云SDK](https://github.com/tencentyun/cos-nodejs-sdk-v5)

  ### 环境变量配置

  ```
  在windows环境变量中增加一项NODE_PATH
  最好同时指向2处，
  例如：
  C:\Users\ZNMLR\node_modules
  lC:\Users\ZNMLR\AppData\Roaming\npm\node_modules
  最少指向一处前者对应npm的本地安装，后者对应npm的全局安装
  ```

  

## 使用

## bat+js

打开注册表编辑器

`WIN+R`调用运行库，输入`regedit`，会打开注册表编辑器

![](https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/2018/07/QQ%E5%9B%BE%E7%89%8720180730193456.png)

找到`计算机\HKEY_CLASSES_ROOT\*\shell`

![](https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/2018/07/QQ%E5%9B%BE%E7%89%8720180730193652.png)

- 新建项`上传腾讯云`，在此项下再次新建项`command`，并修改右侧默认值 `cmd.exe /K "C:\yunCos\1.bat "%1""`

![](https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/2018/07/QQ%E5%9B%BE%E7%89%8720180730194044.png)

在C盘根目录建文件夹：yunCos，新建1.bat,内容如下

- ```
  @echo off
  node C:\yunCos\yunCos.js %1%
  exit
  ```

- 新建   yunCos.js文件，内容暂空

## 安装腾讯云SDK

- 安装运行环境 [node.js](https://nodejs.org/en/)

  这个没什么好说的，双击下一步就好了

- 安装sdk

```
npm i cos-nodejs-sdk-v5 --save -g
```

- 再次安装SDK

> 不要问我为何有这一步，腾讯云文档这样写的  
>
> 先下载[腾讯云SDK](https://github.com/tencentyun/cos-nodejs-sdk-v5)，解压，进入到解压后的目录里执行命令

```
D:\cos-nodejs-sdk-v5-master>npm install -g
```

## 获取腾讯云上传鉴权码

- 请到[腾讯云](https://cloud.tencent.com/product/cos)注册账号并实名认证，

- 新建存储桶

- 获取APPID、SecretId、SecretKey、存储桶名称、所属地域 

  以上步骤请自行阅读腾讯云文档，这里不做说明

## 编写上传脚本

### 官方示例

```
// 引入模块
var COS = require('cos-nodejs-sdk-v5');
// 创建实例
var cos = new COS({
    AppId: '1250000000',   // 修改为自己的appid
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', // 修改为自己的SecretId
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', // 修改为自己的SecretKey
});
// 分片上传
cos.sliceUploadFile({
    Bucket: 'test', // 修改为自己的存储桶名称，由英文、数字和标点符号组成
    Region: 'ap-guangzhou', // 修改为自己的所属地域，应该是纯英文的部分
    Key: '1.zip', // 这个是远端的地址
    FilePath: './1.zip' // 这个是本地地址
}, function (err, data) {
    console.log(err, data);
});
```

### 修改后

```
var picsuffix=new Array(".jpg", ".png", ".bmp", ".jpeg");
function contains(arr, obj) {
  var i = arr.length;
  while (i--) {
    if (arr[i] === obj) {
      return true;
    }
  }
  return false;
}

var filepath=process.argv.splice(2).toString();
var filename = filepath.substring(filepath.lastIndexOf("\\")+1); 
var today = new Date();
var year = today.getFullYear();
var month = today.getMonth() + 1;
var urlkey=year+"/"+(month<10?'0'+month:month)+"/"+filename;
var suffix=filename.substring(filename.lastIndexOf("."), filename.length);

// 引入模块
var COS = require('cos-nodejs-sdk-v5');
// 创建实例
var cos = new COS({
    AppId: '*', // 修改为自己的appid
    SecretId: '*',// 修改为自己的SecretId
    SecretKey: '*',// 修改为自己的SecretKey
});
// 分片上传
cos.sliceUploadFile({
    Bucket: '*',// 修改为自己的存储桶名称，由英文、数字和标点符号组成
    Region: 'ap-guangzhou',// 修改为自己的所属地域，应该是纯英文的部分
    Key: urlkey,
    FilePath: filepath
}, function (err, data) {
	if(err){
		console.log(err);
	}
	else{
		console.log(data);
		const util = require('util');
		var url='';
		if (contains(picsuffix, suffix)) {
			url='![](https://'+data.Location+')';//这里返回的url是md格式，需要可自行更改
		}
		else {
			url='[](https://'+data.Location+')';//这里返回的url是md格式，需要可自行更改
		}
		require('child_process').spawn('clip').stdin.end(url);
	}
});
```

## 关联bat与上传脚本

>打开刚才建的yunCos.js，将上面内容复制进去，并修改相关内容，保存
>在任意文件上点击右键，选择  上传腾讯云   会有脚本框一闪而过，找个文本框粘贴下，就得到你想要的URL

