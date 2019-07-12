---
title: 【JavaScript】日历的键盘事件
date: 2019-07-10
categories:  JavaScript
tags:
    - keyCode
---
电脑端的日历插件，需要增加一个键盘上下左右按键的监听事件，改如何实现呢？

<!--more-->

### 背景
在现有的电脑端系统上，城市选择的插件上可以通过键盘的向上向下进行选择，而日历插件上，却没有这个功能。因此，想要实现这一功能。

### 实现
    function newKeyup(){
		var that = this;
        //triggerNode要根据实际情况设置
		$(triggerNode).keyup(function(e) {
			e = e || window.event;
			var oTarget = e.target || e.srcElement;
			var currentValue = oTarget.value;
			var keyCode = parseInt(e.keyCode ? e.keyCode : e.which);
			var keyCodeArr = [37,38,39,40];
			var defaultNum = 24 * 60 * 60 * 1000;
			if(keyCodeArr.indexOf(keyCode) != -1){
				if(e.preventDefault){
					e.preventDefault();
				}else{
					window.event.returnValue = false;
				}
				var nextValue;
                //根据keyCode计算要跳转的日期
				switch (keyCode){
					case 37:// 向左
						nextValue = new Date(new Date(currentValue).getTime() - defaultNum);
						break;
					case 38://向上
						nextValue = new Date(new Date(currentValue).getTime()  - 7 * defaultNum);
						break;
					case 39://向右
						nextValue = new Date(new Date(currentValue).getTime()  + defaultNum);
						break;
					case 40://向下
						nextValue = new Date(new Date(currentValue).getTime()  + 7 * defaultNum);
						break;
				}
				//渲染
                //......
			}
		});
	}

### 总结下键盘对应的健码值
1、数字键0~9（非数字键盘的）： 48~57 

2、字母A~Z： 65~90

3、功能键F1~F12：112~123

4、控制键：
    BackSpace : 8
    Tab : 9
    Clear : 12
    Enter : 13
    Shift : 16
    Control : 17
    Alt : 18
    Cape Lock : 20
    Esc : 27
    Spacebar : 32
    Page Up : 33
    Page Down : 34
    End : 35
    Home : 36
    Left Arrow : 37
    Up Arrow : 38
    Right Arrow : 39
    Dw Arrow : 40
    Insert : 45
    Delete : 46
    Num Lock : 144

