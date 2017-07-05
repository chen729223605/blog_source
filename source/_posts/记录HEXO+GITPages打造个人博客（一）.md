---
title: 记录Hexo+GitPages打造个人博客！！（一）
date: 2017-06-27 23:31:56
tags:
---

[toc]

# 1.准备篇

以下是准备篇目录 ,如果已经做过了,可以略读，或者跳过

1.1 注册github账号
1.2 新建仓库并且设置为博客空间
1.3 下载并配置git
1.4 下载Node.js
1.5 验证这些安装

<!--more-->

## 1.1 注册github账号
到[github官网][1] 注册一个github账号，这是每个程序员都应该有账号的一个平台。当然，想用hexo的话，也需要这个账号。
用自己的邮箱注册，github会给你的邮箱发送注册确认的邮件，一定要确认注册，否则不能使用pages功能。
## 1.2 新建仓库并且设置为博客空间

**新建代码库**
登录之后，点击页面右上角，选择New repository:
![新建仓库][2]
进入仓库创建页面
![创建仓库页面][3]
在Reppository name下填写 yourname.github.io.
Description 下填一些简介什么的 可以不写。
**特别注意：** 我的github名称是`chen729223605` 则我填的是`chen729223605.github.io`   必须要遵循此格式。

**代码库设置**
创建成功后，将会出现如下页面
![创建成功][4]
接着点击Settings
![Settings][5]
找到github Pages配置
![github pages][6]
点击Automatic page generator ,github将会自动替你创建一个gh-pages页面，如果你的配置没有问题，那么大约15分钟之后，yourname.github.io这个网址就可以正常访问了~ 如果yourname.github.io已经可以正常访问了，那么Github一侧的配置已经全部结束了。

如果你的页面如下所示
![成功界面][7]
说明pages已经配置好了，点击链接就能访问到欢迎页面

## 1.3 下载并配置git

请搜索百度下载git安装文件

安装过程非常简单，一路默认NEXT就行。

安装完成后，在资源管理器或者桌面上右键，会有如下2个选项

![右键菜单][8]

选择`Git Bash Here` 打开git控制台

输入以下指令

> 
**特别注意**： 
`youremail@email.com` 填你注册github时所用的邮箱      
`yourname` 填你的昵称

`git config --global user.name "yourname"` 配置你的昵称 
`git config --global user.email youremail@email.com` 配置你的邮箱
`git config --global core.autocrlf false` 设置crlf 这个有兴趣的自行百度 可以不写
`ssh-keygen -t rsa -C youremail@email.com`这行代码表示的是生成一个ssh key代码，该代码可以简单的理解为git与github绑定关联所需要的代码。输入后会出现一大堆信息，然后会出现等待情况，这个时候不用管他，连续敲3个回车即可。

![git配置][9]

到现在为止，git的配置已经接近尾声了。由于刚刚生成了ssh key代码，这个代码需要与github绑定。那怎么绑定呢。

首先，ssh key会生成几个文件`id_rsa`和`id_rsa.pub` ,文件目录在 `C:\Users\username\.ssh`。

其次，用记事本打开`id_rsa.pub`,复制里面所有内容

然后打开github->settings->SSH and GPG keys

![SSH位置设置][10]

在`title`处填名字，这个无所谓，填你喜欢的即可
在`Key`处粘贴刚刚复制的内容
点击`Add SSH key`即可

![SSH设置][11]



## 1.4 下载Node.js
百度Node.js， 下载到安装包，直接安装即可，没有特殊的要求。

## 1.5 验证这些安装
同时按下win+R，打开运行窗口：
![windows 运行界面][12]

在新打开的窗口中输入cmd，敲击回车，打开命令行界面。
输入
```
node -v
npm -v
```
如果结果如下图所示，则表示Node.js安装正确。
![验证node.js][13]






  [1]: https://github.com/
  [2]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082105444.jpg
  [3]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082160169.jpg
  [4]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082374189.jpg
  [5]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082412140.jpg
  [6]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082473617.jpg
  [7]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499082818486.jpg
  [8]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499078779855.jpg
  [9]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499078814030.jpg
  [10]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499078947484.jpg
  [11]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499078985134.jpg
  [12]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499081836665.jpg
  [13]: http://markdown.jarming.cn/shujiang/%E8%AE%B0%E5%BD%95Hexo+GitPages%E6%89%93%E9%80%A0%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%81%EF%BC%81%EF%BC%88%E4%B8%80%EF%BC%89/1499081946388.jpg