---
title: 【JavaScript】上拉加载下拉刷新
date: 2018-09-29
categories: JavaScript 
tags:
    - Mobile
---

上拉加载下拉刷新如何实现呢？

<!--more-->
**一、思路**
1. 界面：

    A. 分成两块，上方的刷新文字是一块，下方的内容是一块。

    B. 将上方的提示内容隐藏在屏幕之外：

        .header{
            width: 100%;
            height: 1rem;//应该与刷新文字一样的高度
            position: fixed;
            z-index: 100;
        }

2. 逻辑：（主要有4步）

    A. 监听事件

        //el为下拉的整个节点
        //这里为添加监听
        this.el.addEventListener('touchstart', this.refreshTouchStart);
        this.el.addEventListener('touchmove', this.refreshTouchMove);
        this.el.addEventListener('touchend', this.refreshTouchEnd);
        //记住在不用的时候要移除监听哦
        this.el.removeEventListener('touchstart', this.refreshTouchStart);
        this.el.removeEventListener('touchmove', this.refreshTouchMovee);
        this.el.removeEventListener('touchend', this.refreshTouchEnd);
        //具体的函数，我们直接在位置计算中看
            
    B. 位置计算

    **下拉刷新的逻辑 = 当前页面的首项在屏幕中且容器向下滑动的距离大于一定值**
    **上拉加载的逻辑 = 当前页面已滑动到底部**

    C. 控制页面变化

    D. 数据更新包
    
    E. 核心代码

        //代码中包含界面变化和数据更新，仔细看哦
        refreshTouchStart(e) {    
            let touch = e.changedTouches[0];    
            this.tipText = '下拉刷新';//下拉提示文字    
            this.startY = touch.clientY;//获得当前按下点的纵坐标
        }

        refreshTouchMove(e) {    
            //与本逻辑无关，滑动时隐藏底部作用 
            this.$store.commit('bottomShowFalse');   
            let touch = e.changedTouches[0];    
            //获得滑动的距离  
            let _move = touch.clientY - this.startY;  
            //滑动到底部标识  
            this.bottomFlag = $('.present-box').offset().top +     
            $('.present-box').height() - document.body.clientHeight <= 40; 
            
            //内容主体超出了一个头部的距离
            if ($('.present-box').offset().top >= this.headerHeight) {        
                //滑动距离>0代表下拉，<1000是为了防止神人无限拉阿拉 
                if (_move > 0 && _move < 1000) {
                    //根据拉的距离，实现界面上的变化（界面变化）
                    this.el.style.marginTop = _move + 'px';
                    //记录滑动的距离，在松手后让他滑啊滑滑回去
                    this.moveDistance = touch.clientY - this.startY;
                    //拉到一定程度再下拉刷新，防止误操作                
                    if (_move > 50) {            
                        this.tipText = '松开即可刷新'//上面有了            
                    }        
                }    
            }
        }

        refreshTouchEnd() {    
            //松开后底部就biu的出现啦 
            this.$store.commit('bottomShowTrue');
            //若符合上拉加载的条件，则直接进行数据更新    
            if (this.bottomFlag) {       
                this.$emit('loadBottom');    
            }    
            
            let that = this;    
            //拉了一定距离才触发加载动作 
            if (this.moveDistance > 50) {       
                this.tipText = '数据加载中...'; 
                //通过一个promise，让数据更新结束后再进行界面变化。
                //也可以采用其他的方式，如async await方式       
                let timer = setInterval(function () {   
                    //如果拉的很长，一次性弹回去影响用户体验，
                    //所以先让他弹到50的高度，然后再进行数据更新                     
                    that.el.style.marginTop = 
                        that.el.style.marginTop.split('px')[0] - 5 + 'px';
                    if (Number(that.el.style.marginTop.split('px')[0]) <= 50) {
                        //小于50后就不进行界面变化了，先进行数据更新再变化                
                        clearInterval(timer);                
                        new Promise((resolve, reject) => {       
                            //通知父控件，下拉刷新条件满足了，你更新吧              
                            that.$emit('loadTop', resolve, reject);              
                        }).then(() => {                  
                            that.resetBox();                
                        }).catch(() => {                  
                            that.resetBox();//界面恢复（也就是弹回去啦）                
                        });           
                    }       
                }, 1);
            } else {        
                this.resetBox();    
            }
        }
        
        resetBox() {    
            let that = this;    //使用定时器的方式，biubiubiu的实现滑动界面刷新的效果。    
            if (this.moveDistance > 0) {        
                let timer = setInterval(function () {            
                    that.el.style.marginTop =             
                    that.el.style.marginTop.split('px')[0] - 1 + 'px';   
                    //这里很重要，不删除，可能看到奇奇怪怪的东西哦               
                    if (Number(that.el.style.marginTop.split('px')[0]) <= 0){
                        clearInterval(timer); 
                    }  
                }, 1)    
            }    
            this.moveDistance = 0;    
        }


**二、题外话**
1. 参考资料： [上拉加载下拉刷新了解下](https://juejin.im/post/5b9091e7e51d450e70423161)

2. 了解思路即可，目前有多种插件可以直接使用。
比如antd-mobile的[PullToRefresh 拉动刷新](https://mobile.ant.design/components/pull-to-refresh-cn/)