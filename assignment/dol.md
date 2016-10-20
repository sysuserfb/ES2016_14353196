#dol
>Task
>1. 修改example2，让3个square模块变成2个, tips:修改xml的iterator
>2. 修改example1，使其输出3次方数，tips:修改square.c

###example1
>我们可以简单地根据tips来修改相应的内容

1.修改square.c的内容
```
if (p->local->index < p->local->len) {
    DOL_read((void*)PORT_IN, &i, sizeof(float), p);
    i = i*i;
    DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
    p->local->index++;
}
```
改为:
```
if (p->local->index < p->local->len) {
    DOL_read((void*)PORT_IN, &i, sizeof(float), p);
    i = i*i*i;
    DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
    p->local->index++;
}
```
即将i的公式改成3次方

2.删除原来的编译文件，重新编译
```
$ sudo ant -f build_zip.xml all
$ cd build/bin/main
$ sudo rm -r example1
$ sudo ant -f runexample.xml -Dnumber=1
```
得到结果如下:
![example1](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/assignment/Ubuntu-2016-10-16-23-28-59.png)
得到的dot文件截图如下：
![dot1](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/assignment/Ubuntu-2016-10-16-23-37-57.png)
###example2
1. 修改example2.xml的内容
```
<variable value="3" name="N"/>
```
改为：
```
<variable value="2" name="N"/>
```
因为：
```
  <iterator variable="i" range="N">
    <process name="square">
      <append function="i"/>
      <port type="input" name="0"/>
      <port type="output" name="1"/>
      <source type="c" location="square.c"/>
    </process>
  </iterator>
```
2. 删除原来的编译文件，重新编译
```
$ sudo ant -f build_zip.xml all
$ cd build/bin/main
$ sudo rm -r example2
$ sudo ant -f runexample.xml -Dnumber=2
```
得到结果如下:
![example1](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/assignment/Ubuntu-2016-10-16-23-18-47.png)
得到的dot文件截图如下：
![dot1](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/assignment/Ubuntu-2016-10-16-23-38-26.png)

- 和原来相比少了一个square模块

###实验感想
- 这次实验比较简单，特别是在TA的提示下，很容易就做完了，同时也对于dol的结构由更加深入的了解；
- example中包括生产者，消费者，处理模块三个部分，同时用一个xml文件将三者的连接方式定义好；
- 每个模块都要协商XXX_fire函数，这是一个信号产生函数，而整个结构要做的事情在处理模块的fire函数里面定义；
- 那么xml是如何定义连接方式的呢？可以从关键词看出；首先我们要定义进程process，在进程内部需要定义它的端口port和运行的文件source，然后定义通道sw_channel，通道内部也需要定义它的两端端口port，最后我们定义连接connection，将模块的端口和通道的端口连接起来(从origin到target)，成为一个完整的结构。
- 不知我是否算入门了？



