---
title: 【JavaScript】移动端上滑加载分页数据
date: 2019-05-17
categories:  JavaScript
tags:
    - Mobile
---
移动端如何实现分页操作？
<!--more-->
### 概述
在移动端，如果一个接口的出参数据量很大，页面可能会有卡顿的现象。

为了解决这个问题，我们使用分页来改善页面响应时长。

移动端的分页呢，不同于网页的按钮点击，常用的是上滑下拉等操作去触发操作。

这里呢，我们使用上滑来实现分页。

### 实现方法
1、获取滑动方向
    （1）根据滑动的位移进行比较，通过X轴计算出向左滑还是向右滑，通过Y轴计算出向上滑还是向下滑。
    （2）此方法只判断了向上滑还是向下滑。
    （3）返回的出参是：0：无滑动 1：向上 2：向下

    function getSlideDirection(startX, startY, endX, endY) {
        var dy = startY - endY;
        var result = 0;
        if(dy>0) {//向上滑动
            result=1;
        }else if(dy<0){//向下滑动
            result=2;
        } 

        return result;
    }


2、绑定事件
    通过监听touchstart和touchend来判断触发事件的时机。

    function  bindSlideUpEvent(elementId,callback){
        var startX, startY;
        document.getElementById(elementId).addEventListener('touchstart',function (ev) {
            startX = ev.touches[0].pageX;
            startY = ev.touches[0].pageY;
        }, false);
        document.getElementById(elementId).addEventListener('touchend',function (ev) {
            var endX, endY;
            endX = ev.changedTouches[0].pageX;
            endY = ev.changedTouches[0].pageY;
            var direction = getSlideDirection(startX, startY, endX, endY);
            if(direction == 1){//上滑
                callback && typeof  callback == "function" && callback();
            }
        }, false);
    }
