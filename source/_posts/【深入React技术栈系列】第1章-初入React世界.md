---
title: 【深入React技术栈系列】第1章-初入React世界
date: 2018-08-18
categories:  深入React技术栈系列
tags:
    - React
---
1. React**特点**：专注视图层、Virtual DOM、函数式编程。

<!--more-->

2. **JSX基本语法**：

        (1)定义标签时，只允许被一个标签包裹。

        (2)标签一定要闭合。

        (3) DOM元素：小写字母
            组件元素：大写字母

        (4)注释要用{/* 节点注释*/}包裹起来。

        (5)DOCTYPE比较特殊，因为没有闭合，不能直接渲染它。

        常见的做法：构造一个保存HTML的变量，将DOCTYPE与整个HTML标签渲染后的结果串连起来。

        (6)class属性改为className，
            for属性改为htmlFor。

        (7)属性值要使用表达式，用{}替换""



