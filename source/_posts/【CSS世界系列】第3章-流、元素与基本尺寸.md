---
title: 【CSS世界系列】第3章-流、元素与基本尺寸
date: 2018-08-25
categories:  CSS世界系列
tags:
    - CSS
---
1. 块级元素

<!--more-->

    一个水平流上只能单独显示一个元素，多个块级元素则换行显示。

        常见的有：<div><li><table>等。
    
2. 实际开发中，display要么使用block，要么使用table，并不会使用list-item的原因：

        （1）会出现不需要的项目符号。
            （当然，使用list-style:none可消除）

        （2）IE浏览器不支持伪元素的display值为list-item，兼容性不好。
            （:before或:after）
        
3. width：auto包含了以下宽度表现：

    （1）充分利用可用空间。fill-available

    （2）收缩与包裹。fit-content

    （3）收缩到最小。min-content

    （4）超出容器限制。max-content

4. 外部尺寸与流体特性：

    （1）正常流宽度

    （2）格式化宽度


5. 内部尺寸与流体特性：

    （1）包裹性

    （2）首选最小宽度

    （3）最大宽度

6. 页面某个模块的文字内容是动态的，可能是几个字，也可能是一句话，
然后，希望文字少的时候居中显示，文字超过一行的时候居左显示，该如何实现？

        .box{
            text-align: center;
        }

        .content{
            display: inline-block;
            text-align: left;
        }

7. CSS流体布局下的宽度分离原则

        “宽度分离原则”: 
        
        width属性不与影响宽度的padding/border（有时候包括margin）属性共存。
