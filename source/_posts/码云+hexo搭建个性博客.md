---
title: 码云+hexo搭建个性博客
date: 2018-08-13 20:29:38
tags: 
- 码云+hexo
- gitee+hexo
categories: 
- hexo
img:  https://blog-1252958858.file.myqcloud.com/2018/12/upload_ee8ca2_167d9ee016e__8000_00000017.jpg
newimg: false
zhailu: 码云pages+hexo搭建个性博客超详细搭建过程，图文搭建过程，适应于github+gitlab+coding+cos
---
> 码云pages+hexo搭建个性博客
> 
> 非常详细的图文教程

# 简介

## 码云pages
- 码云pages是一个静态网站托管地方,再加上码云本来就是个代码托管的地方,集成pages后,可以很方便的部署你的代码

## hexo
- [Hexo](https://hexo.io/zh-cn/ "官网")是一个快速, 简洁且高效的博客框架. 让上百个页面在几秒内瞬间完成渲染. 具有强大的插件整合系统.

- 其实最早出现是github+hexo的整合,但是本人第一个接触的代码托管平台就是码云,而且还是国产的,相比于github访问速度要提高不少,另外github服务器老是不稳定,所以码云有了pages功能后,就直接在这上面做了,其实部署在github上也是可以的！

## 原理
- 利用 马克飞象生成博客的md文件,利用Hexo把代码生成静态页面,再一键部署到码云上,开启pages后就实现了博客的雏形,当然,想要做的更好还可以继续优化

# 使用步骤

## 安装node/git

- 安装[node.js](https://nodejs.org/en/ "node下载地址")

- 安装[git](http://www.runoob.com/git/git-install-setup.html "git下载地址")

cmd输入以下指令 查看是否安装成功,git的环境环境变量跟JDK一样配置,node版本一定要大于6.9
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110438898.jpg">
 

## 安装Hexo

利用 npm 命令即可安装。在桌面任意位置点击鼠标右键,选择Git Base/Git Base Here

### 命令
- npm install -g hexo

注意：-g是指全局安装hexo。

在任意位置创建一个hexo文件夹。进去文件夹  鼠标右键  选择Git Base/Git Base Here

输入以下指令Hexo 即会自动在目标文件夹建立网站所需要的所有文件。

- hexo init

刷新下文件夹 ,会有以下的目录
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110451759.jpg">
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110502137.jpg">

红框内的没有也无所谓,后续会生成的

继续执行以下指令 npm install（安装依赖包）

hexo generate（构建,这时候会有红框内的文件夹了）
## 本地启动
- hexo server
（启动服务,关闭服务是ctrl+c）

启动后   输入路径localhost:4000到游览器即可看到效果了,类似这样的网站
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110511545.jpg">
## 更换主题
这个主题只是官方默认的主题,当然可以自己修改的,但是官方也提供一些网友自己制作的主题,可以直接套用
网址：https://hexo.io/themes/
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110523501.jpg">
黄框内可以点击预览,选择一个自己喜欢的后,点击左下方红框后进入到github中
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110534709.jpg">
选择红框内点击下载,下载下来是一个zip包,把里面的东西解压至hexo/themes中
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/2018050111054889.jpg">
复制这个文件夹名字。再返回上一级,打开_config.yml,
将里面theme 对应的值改为复制的名字
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110602460.jpg">
冒号后面要有个空格,而且是英文下的空格,不然会有错误
修改后保存,再在hexo内打开  git bash,执行以下指令
- hexo generate

- hexo server

现在刷新下4000的页面,就会有新的主题出现了

Hexo中_config.yml 文件的其他配置,官方的文档： https://hexo.io/zh-cn/docs/configuration.html

## 编写博文

咱直接用最容易上手的,马克飞象 链接：https://maxiang.io/,下载客户端

在编辑器里面写好文章后,另存为MarkDown文件,

在这里我说一下,不用工具也可以的,你用txt也可以的,当然要加上下面的开头以便让hexo识别,再存为.md文件就可以

另外开发人员可以在页面写代码的。md支持html语法 ,总归不管什么编辑器,只要生成的是md文件就可以了

博客内部开头要加

title: httpclent调用webservice   #文章标题

date: #文章日期格式：2018-05-30 15:20:36

tags: #文章标签

categories: #文章分类

 
---

冒号后面要有一个空格,categories后空一行,要有3个 - ,用来和文章内容区分
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110712246.jpg">
 
编辑好后点击人头的标志。
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110719923.jpg">
 
选择markdown保存,保存下来是一个zip压缩包。内部是md文件,

将解压的.md文件放入hexo文件夹下的source 目录下的 _posts 文件夹中,可以看到里面有个hello-world.md 文件,这是默认的文章。

现在  在git bash中关掉服务,再hexo server就可以看到刚才的文章了

## 部署到码云

注册什么的就不必多说了。很简单都是中文,新建一个项目
<img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110731918.jpg">
 <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110745339.jpg">

复制https的地址

在git bash内执行以下指令

- npm install hexo-deployer-git --save

这一步是使用hexo-deployer-git插件将代码推送到码云（现在只是安装）

再次打开hexo根目录的_config.yml 文件,修改deploy 的值

修改前：
 <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110803995.jpg">
修改后
 <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110807756.jpg">

 

冒号后面必须要有个空格

Repository就是刚才复制的地址

OK后 在git bash中执行 hexo deploy 将代码部署至码云

随后会出现2个对话框,username 输入码云帐号,password输入码云密码

OK后点击码云中刚才新建的项目
 <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110818207.jpg">

 

在黑框内可以看到刚才提交的代码,时间基本都是刚刚

然后点击服务,红框,点击pages
 <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110832595.jpg">
  <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110854414.jpg">

分支不用改,默认就行,点击启动服务
  <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501110923587.jpg">
点击地址就是外网可以访问的博客了

OK,基本的框架好了。在编写博客的时候,只要重复第四步就可以了

然后推送到码云上,再重新部署下,它会自动归档

hexo命令：

- hexo clean   ##清理

- hexo g          ##构建、编译

- hexo s          ##启动服务

- hexo d          ##上传至服务器

# 域名

Cname据说不得行,所以我直接用了转发,github可以自定义域名,但是github访问速度很慢
点击链接查看转发https://blog.csdn.net/q2158798/article/details/79801226

放上我刚做的     [iyohei.gitee.io](https://iyohei.gitee.io "演示地址")

# 常见问题

- 出现错误的时候,看下到第几步,把这一步删了重新装,检查下命令代码有没有问题

- Node.Js版本一定要大于6.9否则构建hexo时会出现以下错误,hexo默认支持的版本是6.9以上
  <img src="https://huanfan-1252958858.cos.ap-shanghai.myqcloud.com/pic/20180501111415789.jpg">
- 主题有些也有过时的,有时候下载下来的主题不会生效,网站是一大串代码（需要去看hexo主题官网预览页面的博客,肯定会有相关的配置介绍,这些可以说是DIY的了）,当然你也可以再换一个主题

- 关于博客内图片问题,建议使用外链,本地图片部署到码云上不会显示的,外链推荐使用  图床,或者腾讯云COS,[SM.MS](sm.ms "免费图床"),注册个帐号可以免费,不限流量上传图片(我用了CSDN的图片地址,在手机上图片不会显示)

- 关于主题优化问题,一切东西都可以自定义,修改成自己的名字啊,图标啊,什么的都是可以的,还可以集成站长的一些工具,如访问统计,天气之类的,还有绑定域名啊。感兴趣的可以先百度,有时间我会整理一下再发出来！

- 另外教程不易多看,每个人的方法都有不一样的地方,建议一篇看到底

- 有问题请在下方评论区留言！