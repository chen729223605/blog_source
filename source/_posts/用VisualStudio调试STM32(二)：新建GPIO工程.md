---
title: 用VisualStudio调试STM32(二)：新建GPIO工程
tags: [VisualGDB,VisualStudio,STM32]
grammar_cjkRuby: true
---

1. 选择VisualGDB -> Embeded Peoject Wizard  
确认好工程名后  点击确定

注意 VisualGDB对文件路径上的空格不是很支持，可能会出问题，建议位置选择到一个没有空格的文件路径。像这里的visual studio 2015 这样的路径，是会弹出警告的
![enter description here][1]

2. 这时候自己选择另外一个目录 点击确定
![enter description here][2]

3. 点击NEXT 默认配置
![enter description here][3]

4. 这时候 下一个界面需要你选择编译器 我们就选择ARM

![enter description here][4]

5. 点击install
![enter description here][5]

**注意：**

-  这里会直接到官方网站下载，速度非常慢。如果等不住，可以到官方网站下载[http://gnutoolchains.com/download/][6]
-  如图
![enter description here][7]

- 我本人是自动下载的(等了很长时间)，看了一下默认下载的是5.3版本的gcc

6.下载完成后，显示如下，在Filter搜索自己想要的芯片 
![enter description here][8]

7. 笔者用的是STM32F407VE,选则之后又需要下载驱动程序包BSP，这里笔者没有找到能够额外下载的，只能慢慢下载了。一般如果fanqiang了，下载速度会很快。
 ![enter description here][9]

8. 下载完成后，界面如下 。默认设置，点击next
![enter description here][10]


9. 选则自己板子的LED灯引脚吧。 我是D0。晶振改成自己板子上的晶振频率。
![enter description here][11]

10. 接下来就是选则调试器
笔者用的是Jlink，选则Jlink后，会提示下载一个东西，照着下载就好了。
这里要注意，需要更改的地方就是你的Jlink驱动的路径。需要自己设置，
你根据自己的安装情况选则。 
下一步。
![enter description here][12]

11. 工程创建成功了。接下来找到LEDBlink.cpp吧
 ![enter description here][13]
 
 12. 点击 VisualGDB Debugger 开始调试吧！
 ![enter description here][14]



  [1]: http://markdown.jarming.cn/1484378118548.jpg "1484378118548.jpg"
  [2]: http://markdown.jarming.cn/1484378253171.jpg "1484378253171.jpg"
  [3]: http://markdown.jarming.cn/1484378320959.jpg "1484378320959.jpg"
  [4]: http://markdown.jarming.cn/1484378404829.jpg "1484378404829.jpg"
  [5]: http://markdown.jarming.cn/1484378444342.jpg "1484378444342.jpg"
  [6]: http://gnutoolchains.com/download/
  [7]: http://markdown.jarming.cn/1484378570049.jpg "1484378570049.jpg"
  [8]: http://markdown.jarming.cn/1484378708480.jpg "1484378708480.jpg"
  [9]: http://markdown.jarming.cn/1484378849214.jpg "1484378849214.jpg"
  [10]: http://markdown.jarming.cn/1484378936752.jpg "1484378936752.jpg"
  [11]: http://markdown.jarming.cn/1484378998480.jpg "1484378998480.jpg"
  [12]: http://markdown.jarming.cn/1484379162254.jpg "1484379162254.jpg"
  [13]: http://markdown.jarming.cn/1484379292549.jpg "1484379292549.jpg"
  [14]: http://markdown.jarming.cn/1484379395905.jpg "1484379395905.jpg"