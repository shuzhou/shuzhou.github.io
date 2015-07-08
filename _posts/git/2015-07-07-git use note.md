---
layout: post
title: git使用笔记
category: git
tags: git学习
keywords: git
description: 
---




&#160; &#160; &#160; &#160;git作为一个分布式的版本控制工具，其具有集中式版本管理工具所不具有的优点。关于其具体优点不做过多的赘述，下面就git的简单使用进行简单记录

###**预备工作**
1.注册github账号

2.window上安装git

3.配置机器账号

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
4.创建SSH Key

```
 ssh-keygen -t rsa -C "youremail@example.com"
```

> **为什么GitHub需要SSH Key呢？**
> 
> &#160; &#160; &#160; &#160;因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
>
> &#160; &#160; &#160; &#160;当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。



###**1. 从远程仓库克隆**

假设你需要将某个远程仓库的代码clone下来，那么你就需要用该模块的知识。
例如输入如下命令：

```
git clone git@github.com:shuzhou/shuzhou.github.io.git
```
