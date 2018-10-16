---
title: 【Vue】vue-cli的配置说明
date: 2018-10-16
categories: Vue 
tags:
    - vue-cli
toc: true
---

最近用vue-cli构建了一个vue项目，真的是很好上手啊。<!--more-->
执行一句**vue init webpack XXX（项目名）**的命令，webpack、babel等配置都有了。
本着知其然，也要知其所以然的想法，我还是查阅了一些资料，学习下里面的配置内容。

### 项目文件目录
    
    .
        +-- build    构建脚本目录（包含webpack的配置文件）
        |   +-- build.js
        |   +-- check-version.js
        |   +-- logo.png
        |   +-- utils.js
        |   +-- vue-loader.config.js
        |   +-- webpack.base.config.js
        |   +-- webpack.dev.config.js
        |   +-- webpack.prod.config.js
        |   +-- webpack.test.config.js      
        +-- config   构建配置目录（存放生产环境和开发环境的配置文件）
        |   +-- dev.env.js
        |   +-- index.js
        |   +-- prod.env.js
        |   +-- test.env.js
        +-- node_modules   依赖包
        +-- src       源文件
        |   +-- assets       资源
        |   +-- components   组件
        |   +-- router       路由
        |   +-- App.vue      页面级Vue组件
        |   +-- main.js      整个项目的入口文件
        +-- static   静态文件（第三方的）
        +-- test     测试文件
        |   +-- e2e       
        |   +-- unit       
        +-- .babelrc         babel配置
        +-- .editorconfig    编辑器的配置文件
        +-- .eslintignore    eslint代码检查文件设置
        +-- .eslintrc.js     ES语法检查配置
        +-- .gitingore       git提交时需忽略的文件配置
        +-- .postcssrc.js    postcss配置
        +-- index.html       入口页面
        +-- package.json     整个项目的配置信息
        +-- README.md        项目说明文件

### 题外话
1. 使用的是vue-cli的版本是2.8.1

2. 参考资料：
[vue-cli（vue脚手架）超详细教程](https://blog.csdn.net/wulala_hei/article/details/80488674)
[vue-cli webpack配置分析](https://segmentfault.com/a/1190000008644830)
[【Vue实战之路】一、Vue-cli入门及Vue工程目录全解。](https://www.cnblogs.com/pomelott/p/7857519.html)

