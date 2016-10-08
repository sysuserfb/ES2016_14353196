#Dol 安装日志

##Description
The distributed operation layer (DOL) is a framework that enables the (semi-) automatic mapping of applications onto the multiprocessor SHAPES architecture platform. The DOL consists of basically three parts:

- DOL Application Programming Interface: The DOL defines a set of computation and communication routines that enable the programming of distributed, parallel applications for the SHAPES platform. Using these routines, application programmers can write programs without having detailed knowledge about the underlying architecture. In fact, these routines are subject to further refinement in the hardware dependent software (HdS) layer.

- DOL Functional Simulation: To provide programmers a possibility to test their applications, a functional simulation framework has been developed. Besides functional verification of applications, this framework is used to obtain performance parameters at the application level.

- DOL Mapping Optimization: The goal of the DOL mapping optimization is to compute a set of optimal mappings of an application onto the SHAPES architecture platform. In a first step, XML based specification formats have been defined that allow to describe the application and the architecture at an abstract level. Still, all the information necessary to obtain accurate performance estimates is contained.

##How to install

- 安装一些必要的环境
```
$   sudo apt-get update
$   sudo apt-get install ant
$   sudo apt-get install openjdk-7-jdk
$   sudo apt-get install unzip
```

- 获取文件systemc-2.3.1.tgz和dol_ethz.zip（可用sudo wget命令）
- 解压文件
```
$   mkdir dol
$   unzip dol_ethz.zip -d dol
$   tar -zxvf systemc-2.3.1.tgz
```
- 编译systemc
```
$   cd systemc-2.3.1
$   mkdir objdir
$   cd objdir
    //运行configure(能根据系统的环境设置一下参数，用于编译)
$   ../configure CXX=g++ --disable-async-updates 
```
运行configure得到的结果如图：
![one](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/Ubuntu%2064%20-2016-09-21-20-48-20.png)

```
$   sudo make install
$   cd ..        
$   ls
$   pwd
```
得到的文件列表和路径为：
![two](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/Ubuntu%2064%20-2016-09-21-21-03-27.png)
```
    //修改build.xml文件
    <property name="systemc.inc" value="YYY/include"/>
    <property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
    把YYY改成上页pwd的结果
```

- 编译dol       
```
$   sudo ant -f build_zip.xml all
```
结果如图：
![three](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/Ubuntu%2064%20-2016-09-21-21-10-37.png)
- 我们可以试着运行一下第一个例子
```
$   cd build/bin/main
$   ant -f runexample.xml -Dnumber=1
```
可以看到BUILD SUCCESSFUL:
![four](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/Ubuntu%2064%20-2016-10-08-16-23-10.png)

##Experimental experience
- 总算是配好了dol，之前直到最后一步都是没有问题的，弄了很久之后在最后的步骤加上sudo即可，发现很多人的报错都和我相似，但是问题所在都是不一样的；
- 对于dol框架来说可能我的理解上并不是特别深入和到位，我想随着实验的越做越多，我的理解辉越来越深入的；
- markdown方面由于之前接触过倒是没有太大的问题。

