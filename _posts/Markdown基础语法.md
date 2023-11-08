---
title: Markdown基础语法
date: 2023-11-07 16:48:44
tags: 原创
categories: 
- 杂项
keyword: 
- Markdown
index_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/wallhaven-o571qp.jpg
banner_img: https://picgo-ysc.oss-cn-shenzhen.aliyuncs.com/web/wallhaven-o571qp.jpg
---
Markdown基本语法
<!-- more -->
## 斜体

```md
*这是斜体*
_这也是斜体_
```

## 行内代码

```md
这是`行内代码`
```

## 链接

inline-style 的语法：[link-text](url-link "optional-tips")，其中：

link-text： 显示的 链接文本   
url-link： url链接   
optional-tips： 当鼠标放置在link-text上显示的提示   
reference-style 的语法包括两部分：

[link-text][reference-id]
[reference-id]:url-link "optional-tips"： 在同一个文件的其他段落定义


```markdown
这是[百度搜索](www.baidu.com "使用百度进行搜索")inline-style

这是[百度搜索][baidu]reference-style

[baidu]:www.baidu.com "使用百度进行搜索"
```

## 有序列表

```md
0. 这是一级有序列表
    1. 这是二级有序列表
        1. 这是三级有序列表
8. 这是一级有序列表
0. 这是一级有序列表

```

## 无序列表

```md
* 这是无序列表
+ 这是无序列表
- 这是无序列表

+ 这是一级无序列表
    1. 这是二级有序列表
    1. 这是二级有序列表
+ 这是一级无序列表

```

## 引用

```md
>这是一级引用
>>这是二级引用
>>>这是三级引用
>>这还是三级引用
>这还是三级引用

>新的引用段落

```

## 表格

```md
表格字段一|表格字段二|表格字段三|表格字段四
--|:--|--:|:--:
默认居中对齐|左对齐|右对齐|居中对齐
cell|cell|cell|cell

```

## 分隔行

```md
在单独的一个段落中使用三个或多于三个*或-或_将被渲染成分隔行。
```

## 图片

Markdown中嵌入图片的语法跟链接的语法类似，差别在于嵌入图片比嵌入链接前多了个!特殊字符表示这是一个指向图片的url。

```md
这是一张使用inline-style链接的图片

[图片上传失败...(image-6ec809-1531624818276)]


这是一张使用reference-style链接的图片
![当图片无法显示时出现这个文本][reference-id]

[reference-id]:image-url "optional-tips"
```