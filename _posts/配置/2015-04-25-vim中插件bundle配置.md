---
layout: post
title: vim中插件vundle配置
category: 配置
tags: linux 环境配置
keywords: linux，vim，环境配置
description: 
---

有过vim配置的同学知道，vim配置后可以和IDE媲美，简直是当之无愧的神奇。

现在我就为大家来介绍一款vim的管理插件 --vundle

###1. vundle简介
&#160; &#160; &#160; &#160;Vundle项目托管在github上 [https://github.com/gmarik/vundle](https://github.com/gmarik/vundle)，其特色在于使用git来管理插件,更新方便，支持搜索，一键更新，从此只需要一个vimrc走天下.

###2. vundle配置

- 下载vundle

 
&#160; &#160; &#160; &#160;vundle的源码放在github上，所以先将vundle下载到本地

&#160; &#160; &#160; &#160;`git clone https://github.com/gmarik/vundle.git  ~/.vim/bundle/vundle`

- 配置vim

&#160; &#160; &#160; &#160;使用命令`cd ~ `转换到当前用户的根目录下，然后修改\.vimrc如所示[https://github.com/shuzhou/config_file/blob/master/vimrc](https://github.com/shuzhou/config_file/blob/master/vimrc)

- 当前用户下根目录输入`vim`,然后输入`:BundleInstall`,等待插件安装，安装完毕后就可以使用了




>**注：**
>
>机器上没有安装git命令的童鞋请主动安装git命令

>`sudo apt-get install git`