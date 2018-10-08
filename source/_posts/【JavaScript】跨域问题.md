---
title: 【JavaScript】跨域问题
date: 2018-10-08
categories: JavaScript 
tags:
    - 
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

**三、解决跨域的方法**
1. JSONP
    A. 在HTML标签里，一些标签比如script、img这样的获取资源的标签是没有跨域限制的。

    B. 只能发送GET请求（本质上script加载资源就是GET）

2. 空iframe加form
    A. 

    B.

3. CORS


4. 

**四、CSRF攻击<div id="csrf"></div>**

**五、cookie<div id="cookie"></div>**

**六、Cookie/Session的机制与安全<div id="session"></div>**

**七、Web安全测试之XSS<div id="xss"></div>**

**二、题外话**
1. 参考资料： [不要再问我跨域的问题了](https://segmentfault.com/a/1190000015597029)

