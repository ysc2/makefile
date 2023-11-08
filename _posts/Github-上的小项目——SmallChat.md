---
title: Github 上的小项目——SmallChat
date: 2023-11-07 19:17:37
index_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/4x-leaf-teal_01.jpg
banner_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/4x-leaf-teal_01.jpg
tags: 
- 转载
categories: 
- C
- 开源项目
keyword: 
- C
---
Redis创始人仅用200行代码，编写的教育项目——SmallChat
<!-- more -->
# 编译安装
Github仓库地址
仓库地址：https://github.com/antirez/smallchat

## 下载代码
```shell
git clone git@github.com:Tinywan/smallchat.git
```

## 编译
```shell
cd smallchat/
gcc -o smallchat smallchat.c
```
>参数 -o 指定一个输出文件，这里为smallchat。smallchat.c为源文件

编译后会生成一个smallchat 二进制文件

```shell
smallchat$ ls
Makefile  README.md  smallchat  smallchat.c
```
直接启动服务端二进制文件即可

```shell
./smallchat
```
# 聊天

## 端口
服务端默认端口是7771。当然你也可以修改重新编译成自己想要的端口
```c
#define SERVER_PORT 7711
```

## 终端
>终端1

```shell
telnet 127.0.0.1 7711
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Welcome to Simple Chat! Use /nick <nick> to set your nick.
#设置客户端昵称 /nick 你的昵称
/nick tinywan001

#发送消息
This is just a programming example (tinywan001)
```


图片
>终端2
```shell
telnet 127.0.0.1 7711
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Welcome to Simple Chat! Use /nick <nick> to set your nick.

# 设置客户端昵称 /nick 你的昵称
/nick tinywan002

# 发送消息
Since I wrote this little program (tinywan002)
```
![](https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/20231107192426.png)

> 服务端
```shell
./smallchat 
Connected client fd=4
Connected client fd=5
tinywan002> Since I wrote this little program (tinywan002)
tinywan001> This is just a programming example (tinywan001)
tinywan001> 001
tinywan002> 002
tinywan002> 002002002
tinywan001> 001001001001

Disconnected client fd=5, nick=tinywan002
Disconnected client fd=4, nick=tinywan001
```
![](https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/20231107192407.png)
# 其他
## telnet 命令
telnet是一种远程连接协议，用于通过网络连接到远程设备进行控制和操作。其中，`ip`是指连接的远程设备的ip地址。使用`telnet ip`命令，在命令行中输入telnet 后输入连接的ip地址和端口号，就可以远程连接到目标设备进行操作了。

具体命令格式如下：

```shell
 telnet ip_address port
```

# 参考资料

本文章转载自：https://mp.weixin.qq.com/s/m0fztuw3iEHQ4wWmXlAsjA