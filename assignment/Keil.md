###一、Keil的简介
Keil 是Keil Software公司出品的51系列兼容C语言软件开发系统，与汇编相比，C语言在功能上、结构性、可读性、可维护性上有明显的优势，因而易学易用。Keil提供了包括C、宏汇编、链接器、库管理和一个功能强大的仿真调试器等在内的完整开发方案，通过一个集成开发环境（μVision）将这些部分组合在一起。Keil软件的运行环境是WIN98、NT、WIN2000、WINXP、WIN10等操作系统。

![Keil结构介绍图](http://upload-images.jianshu.io/upload_images/3250499-4bfd65a2ae04a7ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###二、Keil调试器的使用
####1.打开工程
+ 解压FubctionalDebugging.zip
+ 点击Project->Open Project，选择解压好的路径下FunctionalDebugging文件夹中的.uvproj文件
+ 可以看到两个.s文件，Startup.s和main.s
####2.开始调试器
+ 点击Debug->Start/Stop Debug Session，启动调试器

  在调试状态，Debug 菜单项中的命令可以使用了，有关编译的工具栏按钮消失了，出现了一个用于运行和调试的工具栏，Debug 菜单上的大部份命令都有相应的快捷按钮。

  从左到右依次是复位、运行、暂停、单步跟踪、单步、执行完当前子程序、运行到当前行、下一状态、打开跟踪、观察跟踪、反汇编窗口、观察窗口、代码作用范围分析、1＃串行窗口、内存窗口、性能分析、工具按钮命令

####3.基本调试操作
+ 单步跟踪运行
+ 全速运行
+ 观察／修改存储器的数据
+ 复位 
+ 设置断点 
+ 带断点的全速运行 
+ 退出仿真 

###三、代码运行结果

总运行情况:

![总运行情况](http://upload-images.jianshu.io/upload_images/3250499-06a053cd8238d6ff.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Happy:

![Happy](http://upload-images.jianshu.io/upload_images/3250499-a6467218d003e13d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Sad:
![Sad](http://upload-images.jianshu.io/upload_images/3250499-24c01eebadc44e30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Cnt:

![Cnt](http://upload-images.jianshu.io/upload_images/3250499-2c84bda2a945fc29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
结合代码中的以下片段：

```
THUMB
SIZE     EQU   20
;  RAM Section
       AREA    DATA, ALIGN=2
       ; Declare arrays to collect instrumentation data  
HappyBuf SPACE SIZE    ; 20 instances of happy
SadBuf   SPACE SIZE    ; 20 instances of sad
Cnt      SPACE 4       ; offset(index) into arrays
M        SPACE 4       ; random number store
happy    SPACE 1      ; strategic variables 
sad      SPACE 1      ; happy and sad 
```

可以知道，第五段HappyBuf，第六段至第十段SadBuf，第十一段Cnt，第十二段M

运行一次迭代后的内存情况：

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/3250499-0946eb087a0c845d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到第一段和第六段的内存出现第一对8bit的值，第十一段的值为1，所以之前的分析时对的。



