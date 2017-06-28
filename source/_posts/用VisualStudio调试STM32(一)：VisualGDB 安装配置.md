---
title: 用VisualStudio调试STM32(一)：VisualGDB 安装配置
tags: VisualGDB,VisualStudio,STM32
grammar_cjkRuby: true
---

# 0 介绍
众所周知，在调试STM32等ARM芯片的时候，一般就用以下几种编辑器：KEIL，IAR等等。然而，这两款编辑器的编辑功能非常简陋，导致开发人员用起来非常不爽。 特别是在用过Visual Studio之后，完全无法适应功能如此弱小的编辑器。 

所以，有很多想摆脱KEIL等软件束缚的程序员，开始想摆脱他们。比如我。但是，由于网上的资源匮乏，而且，配置也复杂，往往有的就算配置成功也是只能编辑，不能调试。导致不得不放弃该想法。而调试功能也是一个硬伤。 只有KEIL IAR等这种专门做这个的IDE才有，大部分好用的IDE都不具备。

但是，最近在网上找到了一个解决这个问题的办法。能够解决ARM调试+编辑的问题。而且编辑器用的是Visual Studio。这个真是一个振奋人心的消息。于是，就出了本篇笔记。

这是一个Visual Studio插件。 叫VisualGDB。已经实现了在VisualStudio中调试ARM程序，而且可以使用VisualStudio这个强大的编辑器！！
简直不要太爽。


先看效果图：
![visual studio 2015][1]
这个图是我刚刚配置好的 GPIO控制的工程。正常调试当中。


# 	1 前提
- 该工具是用gcc编译的。等于是学习一种新的编译器。和KEIL的armcc不同。各有千秋吧。
- 学习一些新的东西难免要折腾。欢迎喜欢折腾的同学来一起探讨呀。



# 2 安装准备
安装之前需要有如下准备：
1. viusal studio 201x   支持很多版本。我用的是viusal studio2015
2. visual stdtio2015 在安装时要选择 编程语言->Visual C++->适用于Visual C++ 2015的公共工具。
3. 第二点安装完成后  可以创建win32控制台应用程序 则表示OK了。其他版本也是一样。能创建WIN32控制台应用程序，表示已经装了Visual C++支持
4. viusal GDB 以及破解文件。


## 2.1 相关工具
**Visual Studio**
网址http://www.ithome.com/html/win10/164028.htm
这里提供一下两个破解密匙：
专业版：HMGNV-WCYXV-X7G9W-YCX63-B98R2 
企业版：HM6NR-QXX7C-DFW2Y-8B82K-WTYJV 

**Visual GDB**
 百度云
 链接: http://pan.baidu.com/s/1kVltFWN 密码: b1mc



# 3.安装
## 3.1 VS的安装
此处略过
  
## 3.2 VisualGDB的安装

1 关闭VisualStudio
2 安装VisualGDB-5.2r7-trial.msi
![安装ViusalGDB][2]
一直下一步即可

3 安装完成后 再破解
![破解][3]
点击Patch即可 。

4 打开Visual Studio2015
4.1 点击新建工程
![新建工程][4]

出现`Visual GDB`选项卡，表示安装成功啦。


  [1]: http://markdown.jarming.cn/1484373765421.jpg "1484373765421.jpg"
  [2]: http://markdown.jarming.cn/1484376226956.jpg "1484376226956.jpg"
  [3]: http://markdown.jarming.cn/1484376273961.jpg "1484376273961.jpg"
  [4]: http://markdown.jarming.cn/1484376386144.jpg "1484376386144.jpg"