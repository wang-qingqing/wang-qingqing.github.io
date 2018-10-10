---
title: 【JavaScript】跨域问题
date: 2018-10-08
categories: JavaScript 
tags: 跨域 
---

总结下跨域问题的知识点。

<!--more-->
**一、浏览器的同源策略**
1. 同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。
    这是一个用于隔离潜在恶意文件的重要安全机制。

**二、没有同源策略限制的两大危险场景**
1. 针对接口的请求

    若没有同源策略，则会引起CSRF攻击。

    相关知识点：

    A. [CSRF攻击](#csrf)
    
    B. [cookie](#cookie)

    C. [Cookie/Session的机制与安全](#session)

    D. [Web安全测试之XSS](#xss)

2. 针对DOM的查询

    举个例子：

        // HTML
        <iframe name="yinhang" src="www.yinhang.com"></iframe>
        // JS
        // 由于没有同源策略的限制，钓鱼网站可以直接拿到别的网站的Dom
        const iframe = window.frames['yinhang']
        const node = iframe.document.getElementById('你输入账号密码的Input')
        console.log(`拿到了这个${node}，我还拿不到你刚刚输入的账号密码吗`)

**三、解决跨域的方法——接口请求**
1. JSONP
    A. 在HTML标签里，一些标签比如script、img这样的获取资源的标签是没有跨域限制的。

    B. 只能发送GET请求（本质上script加载资源就是GET）

2. 空iframe加form
    A. GET、POST都可以

    B. demo

        form.action = url
        // 在指定的iframe中执行form
        form.target = iframe.name
        form.method = 'post'
        for (let name in data) {
            node.name = name
            node.value = data[name].toString()
            form.appendChild(node.cloneNode())
        }
        // 表单元素需要添加到主文档中.
        form.style.display = 'none'
        document.body.appendChild(form)
        form.submit()

3. CORS（处理跨域的标准做法，前提是兼容性没问题--IE10或者以上）
    A. Cross-origin resource sharing 跨域资源共享

    B. 浏览器将CORS请求分为两类：**简单请求**（simple request）、**非简单请求**（not-so-simple request）。

    C. 只要同时满足以下两大条件，就属于简单请求：
        （1）请求方法是以下三种方法之一：HEAD、GET、POST

        （2）HTTP的头信息不超过以下几种字段：  
            Accept  
            Accept-Language  
            Content-Language  
            Last-Event-ID  
            Content-Type: 只限于三个值application/x-www-form-urlencoded、
                            multipart/form-data、
                            text/plain 
           
    D. 非简单请求：
        非简单请求会发出一次与检测请求，返回码是204，与检测通过才会真正发出请求，这才返回200.

4. 代理
    A. 可以使用Nginx配置代理。让请求的前端域名，转发到后端域名上。

    B. demo(Nginx配置)
        server{
            # 监听9099端口
            listen 9099;
            # 域名是localhost
            server_name localhost;
            #凡是localhost:9099/api这个样子的，都转发到真正的服务端地址http://localhost:9871 
            location ^~ /api {
                proxy_pass http://localhost:9871;
            }    
        }

**四、解决跨域的方法——DOM查询**
1. postMessage(**常用**)
    A. window.postMessage()是HTML5的一个接口，用来实现不同窗口不同页面的跨域通讯。  

    B. 发送消息方的处理——postMessage

    C. 接收消息方的处理——addEventListener

2. document.domain
    A. 只适合主域名相同，但子域名不同的iframe跨域。

    B.比如主域名是http://crossdomain.com:9099，
    子域名是http://child.crossdomain.com:9099，
    这种情况下给两个页面指定一下document.domain
    即**document.domain = crossdomain.com**
    就可以访问各自的window对象了。

3. canvas操作图片的跨域问题
    看这篇文章：[解决canvas图片getImageData,toDataURL跨域问题](https://www.zhangxinxu.com/wordpress/2018/02/crossorigin-canvas-getimagedata-cors/)

**五、CSRF攻击<div id="csrf"></div>**

**六、cookie<div id="cookie"></div>**

**七、Cookie/Session的机制与安全<div id="session"></div>**

**八、Web安全测试之XSS<div id="xss"></div>**

**九、题外话**
1. 参考资料： [不要再问我跨域的问题了](https://segmentfault.com/a/1190000015597029)

