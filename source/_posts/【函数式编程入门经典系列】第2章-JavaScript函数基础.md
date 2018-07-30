---
title: 【函数式编程入门经典系列】第2章-JavaScript函数基础
date: 2018-07-22
categories:  函数式编程入门经典系列
tags:
    - 函数式编程
---
1. 没有名字的函数称为**匿名函数**。

<!--more-->

2. **箭头函数**：

        () => "Simple Function"

        // ()代表函数参数
        // =>是函数体/定义的开始
        // =>后面的内容是函数体/定义

3. **严格模式**是一种JavaScript的受限变体。

        "use strict"
        （1）若把"use strict"放在JS文件的开头，它将在这个特定的文件中检查所有的函数。

        （2）若只在特定的函数中使用严格模式，
            则严格模式只会应用于那个特定的函数，不会影响其他函数。

4. 在ES6中，如果有一个只有一条语句的函数，那么它隐式地表示它返回了一个值。

        let simpleFn = () => "Simple Function"
        相当于
        let simpleFn = function simpleFn(){
            return "Simple Function";
        }

5. **let**关键字声明的变量是局部作用域的。

6. **const**关键字声明常量，可防止被意外地重新赋值。

7. **export default** XXX

8. **import** XXX **from** '...'

