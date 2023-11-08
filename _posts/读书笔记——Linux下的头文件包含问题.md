---
title: 读书笔记——Linux下的头文件包含问题
date: 2023-11-07 16:05:20
index_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/1586853771_daniel-leone-v7datklzzaw-unsplash-modded.jpg
banner_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/1586853771_daniel-leone-v7datklzzaw-unsplash-modded.jpg
tags: 
- 原创
categories: 
- Linux
- 杂项
keyword: 
- Linux
---

《嵌入式C语言自我修养》9.4节的读书笔记。这篇博客将会对工程项目中的头文件问题进行分析
<!-- more -->
## 为什么需要头文件

>主要对一个模块封装的API函数进行声明，其他模块要想调用这个接口函数，要首先包含该模块对应的头文件，然后就可以直接使用了。   

我们在头文件中主要包含了模块函数的声明，在对应的`.c`文件中进行定义。

### 为什么需要先声明后定义

这实际上是一个C语言的历史文件。计算机发展早期，内存很少，编译器在编译工程文件的时候无法同时将所有的文件全部加载到内存中一次性编译，只好以**源文件为单位**逐个进行编译。



一般来讲，变量的定义要放到C文件中，不要放到头文件中，因为这个头文件可能被多人使用，被多个文件包含，头文件经过预处理器多次展开之后也就变成了多次定义。除了函数声明，一般我们还可以放其他一些声明，如数据类型的定义、宏定义等。

那么我们如何防止头文件的多次包含导致的**重定义**错误？

```c
//test.h
#ifndef _TEST_H
#define _TEST_H
.....

#endif
```

## 隐式声明

需要注意的是，对于函数的隐式声明，`ANSI C/C99`标准只是给出一个**warning**，用来提醒程序员，这个隐式声明可能会给程序的运行带来问题。现在最新的`C11`标准和`C++`标准对隐式声明管理得更严格，遇到这种情况，直接报错处理，防患于未然。

在使用一个没有经过声明的对象\函数时，编译器不会直接报错（C89和C99）中。例如：
```c
int mian (int argc,char** argv)
{
    printf("Hello World\n");
    return 0;
}
```
在上面的`printf`函数的使用中，编译器会报错因为你没有包含`stdio.h`头文件。

## 头文件的路径问题

我们知道C语言的头文件包含有两种语法：   
- `include <stdio.h>`
- `include "mytest.h"`

那么这两种语法的区别是什么？

如果你引用的头文件是标准库的头文件或官方路径下的头文件，一般使用尖括号<>包含；如果你使用的头文件是自定义的或项目中的头文件，一般使用双引号""包含。头文件路径一般分为绝对路径和相对路径：绝对路径以根目录“/”或者Windows下的每个盘符为路径起点，相对路径则以程序文件当前的目录为起点。

编译器在编译过程中会按照这些路径信息到指定的位置查找头文件，然后通过预处理器做展开处理。在查找头文件的过程中，编译器会按照默认的搜索顺序到不同的路径下去搜索。

以`＃include<xx.h>`  为例，当我们使用尖括号<>包含一个头文件时，头文件的搜索顺序如下。

● 通过GCC参数gcc-I指定的目录（注：大写的I）。

● 通过环境变量CINCLUDEPATH指定的目录。

● GCC的内定目录。

● 搜索规则：当不同目录下存在相同的头文件时，先搜到哪个就使用哪个，搜索到头文件后不再往下搜索。


`include "test.h"`方式的搜索规则：

● 项目文件夹下 

● 通过GCC参数gcc-I指定的目录（注：大写的I）。

● 通过环境变量CINCLUDEPATH指定的目录。

● GCC的内定目录。

● 搜索规则：当不同目录下存在相同的头文件时，先搜到哪个就使用哪个，搜索到头文件后不再往下搜索。


在程序编译时，如果我们的头文件没有放到官方路径下面，那么我们可以通过gcc-I来指定头文件路径，编译器在编译程序时，就会到用户指定的路径目录下面去搜索该头文件。如果你不想通过这种方式，也可以通过设置环境变量来添加头文件的搜索路径。在Linux环境下我们经常使用的环境变量如下。

● PATH：可执行程序的搜索路径。

● C_INCLUDE_PATH：C语言头文件搜索路径。

● CPLUS_INCLUDE_PATH：C++头文件搜索路径。

● LIBRARY_PATH：库搜索路径。



如何设置环境变量：

```shell
vim ~/.bashrc
#添加如下内容
export PATH="/path/:$PATH"
#或者是
export C_INCLUDE_PATH="/path/"
```

## Linux内核源码中的头文件包含

如果你看过Linux内核源码，你一定看到过下面的头文件包含：

```c
#include <linux/kernel.h>
#include <arm/uaccess.h>
```

那么上面这种形式的包含是什么情况？

打开源码顶层的`Makefile`文件可以查找到`LINUXINCLUDE`变量，用来指定内核编译时的头文件路径。

```Makefile
USERINCLUDE    := \
		-I$(srctree)/arch/$(SRCARCH)/include/uapi \
		-I$(objtree)/arch/$(SRCARCH)/include/generated/uapi \
		-I$(srctree)/include/uapi \
		-I$(objtree)/include/generated/uapi \
                -include $(srctree)/include/linux/kconfig.h
```

编译器通过`-Iinclude`参数指定相对路径的起点后，再指定要包含的头文件路径目录就可以了：`＃include <linux/kernel.h>`，预处理器就会到`include/linux`目录下查找相应的头文件`kernel.h`。

如果arch指定为x86-64，那么`-I$(objtree)/arch/$(SRCARCH)/include/`就会变成`-I$(objtree)/arch/x86-64/include/`，在给目录下有`arm`文件夹。

所以`#include <asm/uaccess.h>`会到指定的文件夹去寻找文件。


## 参考资料

《嵌入式C语言自我修养》9.4