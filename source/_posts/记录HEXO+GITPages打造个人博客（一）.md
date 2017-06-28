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
## 1.2 新建仓库并且设置为博客空间
## 1.3 下载并配置git

请搜索百度下载git安装文件

安装过程非常简单，一路默认NEXT就行。

安装完成后，在资源管理器或者桌面上右键，会有如下2个选项

![右键菜单](http://upload-images.jianshu.io/upload_images/4052214-c7b0d879d910f368.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

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

![git配置](http://upload-images.jianshu.io/upload_images/4052214-935f07bf2f0e7d9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到现在为止，git的配置已经接近尾声了。由于刚刚生成了ssh key代码，这个代码需要与github绑定。那怎么绑定呢。

首先，ssh key会生成几个文件`id_rsa`和`id_rsa.pub` ,文件目录在 `C:\Users\username\.ssh`。

其次，用记事本打开`id_rsa.pub`,复制里面所有内容

然后打开github->settings->SSH and GPG keys

![SSH设置位置](http://upload-images.jianshu.io/upload_images/4052214-1e5de895570adc76.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在`title`处填名字，这个无所谓，填你喜欢的即可
在Key处粘贴刚刚复制的内容
点击Add SSH key即可

![ssh设置](http://upload-images.jianshu.io/upload_images/4052214-21b9a83958cbecbb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




## 1.4 下载Node.js

## 1.5 验证这些安装