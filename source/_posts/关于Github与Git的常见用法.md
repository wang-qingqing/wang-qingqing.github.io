---
title: 关于Github与Git的常见用法
date: 2018-06-19
categories:  工具类
tags:
    - Git
    - Github
---
平时工作时，我会用到github和git。记录一下常见用法，以备查阅。
<!--more-->
**Github的常见用法**
1. 设置全局配置

        git config --global user.name "your name"
        git config --global user.email "your_email@youremail.com"

2. github上的contributions是根据每个项目的默认分支来统计的。
设置默认分支的操作是:XXX项目 -> Setting -> Branches ->Default branch。

**Git常用命令**

1. 下载默认分支的代码

        git clone [url] 

2. 下载指定分支的代码(以branch分支为例)

        git clone -b branch [url]

3. 在当前目录新建一个git代码库

        git init 

4. 新建一个git的目录

        git init [project-name]

5. 添加文件到暂存区
```
添加当前目录的所有文件
git add .

添加指定目录
git add [dir]

添加指定文件
git add [file1] [file2]
```

6. 提交文件到仓库区
```
提交暂存区到仓库区
git commit -m [message]

提交暂存区的指定文件到仓库区
git commit [file1] [file2] -m [messgae]

提交工作区自上次commit之后的变化，直接到仓库区
git commit -a
```