---
title: Markdown常用语法
date: 2018-06-18
categories:  工具类
tags:
    - Markdown
---
在编辑博客或者github的时候，我们都会用到Markdown编辑器。
这篇博客就是来记录下常用的Markdown语法。

<!--more-->

1. 概述
    A.宗旨：易读易写

    B.兼容HTML

    C.特殊字符自动转换        

2. 区块元素
```
A.段落和换行
    使用空行或者<br/>

B.标题
    （1）使用底线的形式，=（H1），-（H2）
    （2）在行首插入1到6个#，对应到标题的H1-6。

C.区块引用
    在每行的最前面加上>

D.列表
    （1）无序列表使用*、+或者-作为列表标记

        + 无序1
        + 无序2
        + 无序3

    （2）有序列表使用数字接着一个英文句点

        1. 有序1
        2. 有序2
        3. 有序3

E.代码区块
    使用<pre><code> XXX </code></pre>标签来把代码区块包起来。

F.分隔线
    在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。
    也可以在星号或是减号中间插入空格。

    * * *
    ***
    - - -
```

3. 区段元素
```
A.链接
    （1）行内式：
        只要在方块括号后面紧接着圆括号并插入网址链接即可，
        用双引号把 title 文字包起来。

        This is [an example](http://example.com/ "Title") inline link.

    （2）参考式：
        在链接文字的括号后面再接上另一个方括号，
        而在第二个方括号里面要填入用以辨识链接的标记。

        This is [an example][id] reference-style link.
        [id]: http://example.com/  "Optional Title Here"

B.强调
    使用星号（*）和底线（_）作为标记强调字词的符号，
    被 * 或 _ 包围的字词会被转成用 <em> 标签包围，
    用两个 * 或 _ 包起来的话，则会被转成 <strong>。

C.代码
    标记一小段行内代码，你可以用反引号把它包起来（`）

D.图片
    （1）行内式：
        方括号里面放上图片的替代文字，
        普通括号里面放上图片的网址，
        最后还可以用引号包住并加上 选择性的 'title' 文字。

        ![Alt text](/path/to/img.jpg)
        ![Alt text](/path/to/img.jpg "Optional title")

    （2）参考式：「id」是图片参考的名称。

        ![Alt text][id]
```

4. 其它
```
A.反斜杠:利用反斜杠来插入一些在语法中有其它意义的符号。
    \   反斜线
    `   反引号
    *   星号
    _   底线
    {}  花括号
    []  方括号
    ()  括弧
    #   井字号
    +   加号
    -   减号
    .   英文句点
    !   惊叹号

B.自动链接:使用尖括号。
```

**参考资料：**
1. [Markdown 语法说明](https://www.appinn.com/markdown/index.html#philosophy)