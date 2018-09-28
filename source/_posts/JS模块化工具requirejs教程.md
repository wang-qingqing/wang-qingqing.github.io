---
title: JS模块化工具requirejs教程
date: 2018-09-28
categories: JavaScript 
tags:
    - RequireJS
---

RequireJS是一个轻量级的JavaScript模块载入框架，遵循**AMD**规范。

<!--more-->
**一、好处**

1. 模块化加载

2. 防止js加载阻塞页面渲染

        注：当引入某个a.js时（此js中包含了立即执行的alert语句），
        如果未用require的方式引入，则会有页面中html内容是一片空白的场景。
        这就是js阻塞浏览器渲染导致的结果。
        如果使用require的方式，则可避免这种场景。

**二、基本知识**

1. 基本API

    A. **define**：用来定义一个模块。

    B. **require**：加载依赖模块，并执行加载完成后的回调函数。

    C. demo:
    
            (1)定义a.js：
                define(function(){
                    function fun1(){
                        //...
                    }
                })

            (2)在页面中引用a.js：
                //第一个参数表示引入的依赖，一定是个数组。
                //第二个参数可选，是callback的function，用来处理加载完毕后的逻辑。
                require(["js/a"],function(){
                    console.log("load finished");
                });

2. 加载文件 

    A. **require.config**：可用来配置模块加载位置。
    （来自本地服务器、其他网站或CDN的js引入方式）

    B. demo:
    
        require.config({
            paths: {
                "jquery": ["http://libs.baidu.com/jquery/2.0.3/jquery","js/jquery"],
                "a": "js/a"
            }
        })

        require(["jquery","a"],function($){
            $(function(){
                console.log("load finished");  
            })
        })

        注：
        (1)引入模块时，可不写.js后缀。
        
        (2)demo中的callback函数中的$参数，表示依赖jquery模块的输出变量$。


3. 全局配置

    A. 主数据功能：在加载requirejs脚本的script标签加入了**data-main**属性。
        (1)这个属性指定的js将在加载完require.js后处理。
        
        (2)require默认会将data-main指定的js为根路径。

    B. demo：
        (1)main.js:
            require.config({
                paths : {
                    "jquery": ["http://libs.baidu.com/jquery/2.0.3/jquery", "js/jquery"],
                    "a": "js/a"   
                }
            })

        (2)页面：
            <script data-main="js/main" src="js/require.js"></script>

        (3)如果使用require(['jquery'])，在不配置jquery的paths的情况下，
            require会自动加载js/jquery.js这个文件，而不是jquery.js。
            相当于默认配置了：
                require.config({
                    baseUrl: "js"
                })

4. 第三方模块

    A. 通过require加载的模块一般都需要符合AMD规范（通过define声明模块），
    但在加载非AMD规范的js时，需要使用**shim**功能。

    B. 非AMD模块输出，可将非标准的AMD模块shim成可用的模块。

            require.config({
                shim: {
                    "underscore" : {
                        exports : "_";
                    }
                }
            })

            require(["underscore"], function(_){
                _.each([1,2,3], alert);
            })

    C. 插件形式的非AMD模块,使用shim转换：

        require.config({
            shim: {
                "underscore" : {
                    exports : "_";
                },
                "jquery.form" : {
                    deps : ["jquery"]
                }
                //可简写成：
                //"jquery.form" : ["jquery"]
            }
        })

        require.config(["jquery", "jquery.form"], function($){
            $(function(){
                $("#form").ajaxSubmit({...});
            })
        })

**三、题外话**

1. 此篇博客是菜鸟教程的同名文章的笔记。

2. 通读全文以后，即可了解RequireJS如何使用了。


