# xv6-labs：lab 1

### 作业内容
#### 实验背景
xv6只支持少量的shell命令，因此需要添加常用的shell命令。

#### 实验内容 1：实现sleep命令 （🍰）
为xv6实现用户级的sleep命令，类似于UNIX中的'sleep'命令。实现的'sleep'应该暂停一段用户指定的时钟滴答数。在xv6内核中，滴答（tick）是一个时间概念，来自计时器芯片的两次中断之间的时间。

##### 提示
+ 在开始编码之前，阅读xv6书籍的第1章。
+ 将你的代码放在'user/sleep.c'文件中。查看'user/'目录中的其他一些程序，例如'user/echo.c'、'user/grep.c'和'user/rm.c'，以了解如何将命令行参数传递给程序。
+ 将你的'sleep'程序添加到Makefile中的UPROGS；完成后，使用'make qemu'将编译你的程序，然后你可以从xv6 shell中运行它。
+ 如果用户忘记传递参数，'sleep'应该打印一个错误消息。
+ 命令行参数以字符串形式传递；你可以使用'atoi'函数将其转换为整数（请参阅'user/ulib.c'）。
+ 使用系统调用'sleep'。
+ 查看xv6内核代码中实现'sleep'系统调用的部分（查找'sys_sleep'），在'user/user.h'中查看从用户程序中可调用'sleep'的C定义，以及在'user/usys.S'中查找从用户代码跳转到内核执行'sleep'的汇编代码。
+ 'sleep'的'main'函数在完成时应该调用'exit(0)'。
+ 查看Kernighan和Ritchie的书《C程序设计语言》（第二版）（K&R）以了解有关C语言的知识。

##### 结果自测
sleep命令执行后的效果
```
$ make qemu
  ...
 init: starting sh
$ sleep 10
(无任何输出持续一小会）
$
```


#### 实验内容 2：实现find命令 （🍰🍰）
为xv6实现find命令，简化版的类似于UNIX 'find' 程序，查找具有特定名称的目录树中的所有文件。

##### 提示
+ 查看'user/ls.c'以了解如何读取目录。
+ 使用递归来使'find'能够进入子目录。
+ 不要递归进入“.”和“..”。
+ 文件系统的更改在qemu运行时保持不变；要获取干净的文件系统，请运行'make clean'，然后再运行'make qemu'。
+ 你需要使用C字符串。参考K&R（C语言教材），例如第5.5节。
+ 请注意，'=='不像Python中那样比较字符串。应使用'strcmp()'代替。
+ 将程序添加到Makefile中的UPROGS。

##### 结果自测
```
$ make qemu
...
init: starting sh
$ echo > b
$ mkdir a
$ echo > a/b
$ mkdir a/aa
$ echo > a/aa/b
$ find . b
./b
./a/b
./a/aa/b
$
```