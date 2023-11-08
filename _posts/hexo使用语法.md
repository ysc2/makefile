---
title: hexo使用语法
index_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/alexandre-lallemand-JE8vJ-sk1K4-unsplash.jpg
banner_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/alexandre-lallemand-JE8vJ-sk1K4-unsplash.jpg
---
hexo基本使用
<!-- more -->
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

开头的变量含义：  
```txt
title: stm32  
date: 2023-10-29 17:59:15  
index_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/%E5%BD%92%E6%A1%A3.jpg  

在外面看文章显示的图片

banner_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/%E5%88%86%E7%B1%BB.jpg   

打开文件显示的主图片

tags:      标签
    - 原创   
categories:   分类目录
  - STM32   
  - 测试   这个表明是STM32目录下的测试目录
keyword:    
  - STM32   
sticky:    文章在网站中的优先级,100最高
  - 100   
当文章设置了 sticky 后，主题会默认在首页文章标题前增加一个图标，来标识这是一个置顶文章，你可以通过主题配置去关闭或修改这个功能：

index:
  post_sticky:
    enable: true
    icon: 'iconfont icon-top'
    
hide: true  隐藏文章不在首页和其他归档分类页里展示

archive: true 如果只是想让文章在首页隐藏，但仍需要在归档分类页里展示    
```
### 便签
```txt
在 markdown 中加入如下的代码来使用便签：

{% note success %}
文字 或者 `markdown` 均可
{% endnote %}

或者使用 HTML 形式：
<p class="note note-primary">标签</p>
可选便签：

primary

secondary

success

danger

warning

info

light
```
>WARNING使用时 {% note primary %} 和 {% endnote %} 需单独一行，否则会出现问题

### 折叠块
```txt
使用折叠块，可以折叠代码、图片、文字等任何内容，你可以在 markdown 中按如下格式：

{% fold info @title %}
需要折叠的一段内容，支持 markdown
{% endfold %}
info: 和行内标签类似的可选参数 title: 折叠块上的标题
```
### hexo fluid官方手册
https://fluid-dev.github.io/hexo-fluid-docs/guide/#tag-%E6%8F%92%E4%BB%B6