---
title: 用VisualStudio调试STM32(三)：适配CubeMX生成的代码
tags: VisualGDB,VisualStudio,STM32
grammar_cjkRuby: true
---



# 1.说明

虽然说VisualGDB十分强大，已经实现了MCU调试开发由KEIL转向VisualStudio 。但是最为一个STM32的开发者，肯定还没有满足。因为，如果这样的话，CubeMX将何去何从。要知道，CubeMX也是一个神器啊！直接就能生成KEIL工程，初始化等繁琐操作直接交给CubeMX有没有。代码直接将你写好。而且代码风格也不错。但是，CubeMX并没有强大到直接生成VisualGDB工程。

---

这篇心得简要的介绍了如何新建一个VisualGDB工程，适配CubeMx生成的代码。当默认生成的工具是KEIL时，能够实现KEIL和VisualGDB同时都能编译下载。 想用哪个用哪个。不可谓不爽啊！

--- 

网上也有一些方法适配CubeMX，包括官方也有相关的资料。但是始终存在一些问题。满足不了个人的需求。
比如
1. 用官方的导入功能导入时，CUBEMX生成的HAL库默认将被屏蔽掉，而使用VisualGDB自带的HAL库。这就不太爽了，因为VisualGDB更新肯定没有CubeMX来的快啊。有时候CubeMX的固件库已经到1.14了。
自带的固件库才1.13. 我就想用新版本咋办。
2. 官方有的HAL库 只是作为链接到本工程，本地并没有。需要手动设置一下才会拷贝到本地。

---

**注意：**
1. 我用的不是最简便的方法，反而有一些麻烦。但是，为了工程的好用性，这些麻烦也是值得的。其实比自己手动新建一个KEIL工程要快的多。
2. 有一些步骤是可以保存下来 给以后使用的。理论上，以后新建会更快。



# 2.过程

1. 新建CubeMX工程，或者就用原来已经就有的CubeMX生成的工程。工程设置和原来一样，不需要有啥变化。下面是我正在使用的工程配置。
![enter description here][1]

2. 生成代码。在工程文件夹新建一个VS-ARM文件夹。
![enter description here][2]

3. 打开VS->新建VisualGDB工程，注意工程路径的选择，点击确定
![enter description here][3]


4. NEXT
![enter description here][4]

5. 选择自己的芯片 后 next
![enter description here][5]

6. 这里是主函数功能，我们后续不用的。所以无需理会。next
![enter description here][6]


7. 选择自己的下载器 。点击finish
![enter description here][7]


8. 接下来是重头戏。在新建的工程上修改。右键工程名，选择VisualGDB Project Properties.
![enter description here][8]

9. 如下图，取消勾选自带的HAL库,Embedded Frameworks->取消STM32Cube HAL前面的勾。 这个自带的库是在VisualGDB里的。这里我们要用自己工程里面的
![enter description here][9]

10. 点击 MSBuild Settings 。这一步是最烦的。

![enter description here][10]
 **注意：** 
 JM_DEBUG是我自己定义的。使用者无需定义。
 ARM_MATH_CM4 我是用了DSP库 的 ，不用的也可以不用定义
 **原则就是将KEIL中的定义复制过来，包括define 和 include。但是宏定义的分隔符 keil中是逗号，vs中是分号。**

![enter description here][11]

配置全部完成之后 点击OK。


11. 接下来添加工程内的库文件。
在VS工程目录里的  Source文件夹新建HAL文件夹，
![enter description here][12]


然后 右键HAL->添加->现有项 选择需要的hal库文件
![enter description here][13]

原则也是一样 和 keil相同
![enter description here][14]

12. 添加用户自己的文件 
 这里推荐一个方法，只要添加一个文件夹，就可以将文件夹内所有文件都添加进来。包括文件夹里的文件夹。
 右键Source files->添加->Import folder recursicely.表示递归添加文件夹。
 ![enter description here][15]
  选则工程目录下的Src文件夹
![enter description here][16]
点击OK。
结果就一次性将所有文件都加进来了。效果如下
![enter description here][17]

13. 移除原来自带的源文件 
移除自动生成的2个文件 `LEDBlink.cpp`，`system_stmf4xx.c`.
system_stmf4xx.c在原来的工程里就有 这里就不需要了。
![enter description here][18]

14. 删除VS工程目录下的文件
`LEDBlink.cpp`
`sys32f4xx_hal_conf.h ` ==>这个文件必删 因为这个文件是配置文件。VS默认调用这个。但是在原始工程的inc文件夹里已经有了。
`system_stm32f4xx`
![enter description here][19]

15. 编译工程吧 下载吧 调试吧 尽情享受VS的能力吧 当然想回KEIL的时候 随时打开KEIL工程即可用keil编写调试。互相独立 完全不影响。公用的只有源代码。
 ![enter description here][20]

15. 献上我的工程的调试图吧
 ![enter description here][21]

# 附录 
1. 编译的时候有可能出现以下问题


![enter description here][22]
这个是由于在工程中使用了printf。printf的处理 keil和VS是不一样的。
需要在工程里加一个syscall.c。 
这里附上我的文件。
这个文件不一定是最好的。希望大家使用者去自己好好研究一下。
=[syscall.c][23]

2. 我的include记录
```
../../../Drivers/CMSIS/Device/ST/STM32F4xx/Include;../../../Drivers/CMSIS/Include;../../../Drivers/STM32F4xx_HAL_Driver/Inc;../../../Drivers/STM32F4xx_HAL_Driver/Inc/Legacy;../../../Inc;../../../Src;../../../Src/BaseLibrary;../../../Src/BSP;../../../Src/ymodem
```


  [1]: http://markdown.jarming.cn/1484559639707.jpg "1484559639707.jpg"
  [2]: http://markdown.jarming.cn/1484559711476.jpg "1484559711476.jpg"
  [3]: http://markdown.jarming.cn/1484559785744.jpg "1484559785744.jpg"
  [4]: http://markdown.jarming.cn/1484559972625.jpg "1484559972625.jpg"
  [5]: http://markdown.jarming.cn/1484560030214.jpg "1484560030214.jpg"
  [6]: http://markdown.jarming.cn/1484560107370.jpg "1484560107370.jpg"
  [7]: http://markdown.jarming.cn/1484560136050.jpg "1484560136050.jpg"
  [8]: http://markdown.jarming.cn/1484560266362.jpg "1484560266362.jpg"
  [9]: http://markdown.jarming.cn/1484560470033.jpg "1484560470033.jpg"
  [10]: http://markdown.jarming.cn/1484566517456.jpg "1484566517456.jpg"
  [11]: http://markdown.jarming.cn/1484560900515.jpg "1484560900515.jpg"
  [12]: http://markdown.jarming.cn/1484561166902.jpg "1484561166902.jpg"
  [13]: http://markdown.jarming.cn/1484561277831.jpg "1484561277831.jpg"
  [14]: http://markdown.jarming.cn/1484565088343.jpg "1484565088343.jpg"
  [15]: http://markdown.jarming.cn/1484565263636.jpg "1484565263636.jpg"
  [16]: http://markdown.jarming.cn/1484567673468.jpg "1484567673468.jpg"
  [17]: http://markdown.jarming.cn/1484565565162.jpg "1484565565162.jpg"
  [18]: http://markdown.jarming.cn/1484565679886.jpg "1484565679886.jpg"
  [19]: http://markdown.jarming.cn/1484565876548.jpg "1484565876548.jpg"
  [20]: http://markdown.jarming.cn/1484566034385.jpg "1484566034385.jpg"
  [21]: http://markdown.jarming.cn/1484567216810.jpg "1484567216810.jpg"
  [22]: http://markdown.jarming.cn/1484566709842.jpg "1484566709842.jpg"
  [23]: http://markdown.jarming.cn/syscalls.c