---
layout: post
title: windows下搭建jekyll调试博客
category: 配置
tags: 环境配置 github
keywords: github 环境配置
description: 
---


首先对安装的整理流程做个简单叙述：

- 安装Ruby及Devkit
- 使用gem安装Jekyll
- 安装 Pygments
	
	 - 安装 Python
	 - 安装 ‘Easy Install’
	 - 用 “easy_install” 来安装 Pygments
- 启动Jekyll
- 故障诊断


###**1. 安装Ruby及Devkit**
####**1). 安装Ruby**
- 前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)

- 在 “RubyInstallers” 部分，选择某个版本点击下载。（笔者安装版本[下载](http://pan.baidu.com/s/1hqpNBi0)）
例如， Ruby 2.0.0-p451 (x64) 是适于64位 Windows 机器上的 Ruby 2.0.0 x64 安装包。

- 通过安装包安装

	- 最好保持默认的路径 C:\Ruby200-x64， 因为安装包明确提出 “请不要使用带有空格的文件夹 (如： Program Files)”。
	- 勾选 “Add Ruby executables to your PATH”，这样执行程序会被自动添加至 PATH 而避免不必要的头疼（建议将所有可勾选的项全部进行勾选）。

- 验证ruby是否安装成功：打开控制台输入`ruby -v`，例如输出`ruby 2.1.5p273 (2014-11-13 revision 48405) [x64-mingw32]`

####**2). 安装Devkit**

&#160; &#160; &#160; &#160;DevKit是windows平台下编译和使用本地C/C++扩展包的工具。它就是用来模拟Linux平台下的make,gcc,sh来进行编译。但是这个方法目前仅支持通过RubyInstaller安装的Ruby。

- 再次前往 [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)
- 下载同系统及 Ruby 版本相对应的 DevKit 安装包。 例如，DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe 适用于64位 Windows 系统上的 Ruby 2.0.0 x64。(笔者安装的ruby对应的Devkit版本[下载](http://pan.baidu.com/s/1dDcw84T))
- 运行安装包并解压缩至某文件夹，如 C:\DevKit
- 打开控制台，进入解压文件夹目录，输入如下命令

	```
	ruby dk.rb init
	ruby dk.rb install
	```
> 安装Devkit出现问题汇总：
> 
> [http://blog.sina.com.cn/s/blog_7444213001018fa7.html](http://blog.sina.com.cn/s/blog_7444213001018fa7.html)

###**2.使用gem安装Jekyll**

一般情况下经过第1步骤的安装gem已经安装，我们可以通过输入`gem -v`进行检查gem是否安装（Gem是一个管理Ruby库和程序的标准包）

- gem是可以选择源的，默认的源有点慢，可以使用ruby.taobao.org的源
	- 查看当源
		
		输入：	

		```
		gem sources list
		```
		显示：
	
		```
		***CURRENT SOURCES ***
		https://rubygems.org/
		```

	- 添加新源

		```
		gem sources -a http://ruby.taobao.org/
		```

	- 删除默认源
 
		```
		gem sources --remove https://rubygems.org/
		```

	- 再次查看新源,确保只有`http://ruby.taobao.org/`就行了


- 直接如下命令即可安装jekyll，该命令会安装jekyll及所有需要的依赖（但不包括插件）
	
	```
	gem install jekyll
	```


> 网上有人说jekyll的版本1.4.3有个bug,但是我直接安装了最新版本，为2.5.3，没有碰到所谓的bug，估计是新版本已经修复，所以自动略过


###**3.安装 Pygments**
&#160; &#160; &#160; &#160;Jekyll 里默认的语法高亮插件是 Pygments。 它需要安装 Python。

&#160; &#160; &#160; &#160;不久之前，Jekyll 还添加另一个高亮引擎名为 Rouge， 尽管暂时不如 Pygments 支持那么多的语言，但它是原生 Ruby 程序，而不需要使用 Python。

####**1). 安装 Python**

- 建议安装python 2(具体安装略去)
- 配置python环境变量
- `python –V`检查python是否安装成功

####**2). 安装 ‘Easy Install’**

- 浏览 [https://pypi.python.org/pypi/setuptools#installation-instructions](https://pypi.python.org/pypi/setuptools#installation-instructions) 来查看详细的安装指南。

- 对于 Windows 7 的机器，下载 [ez_setup.py](http://pan.baidu.com/s/1qWl38Gc) 并保存，例如，至C:\。 然后从命令行使用 Python 运行此文件：

	```
	python “C:\ez_setup.py”
	```

- 添加 ‘Python Scripts’ 路径 (如： C:\Python27\Scripts) 至 PATH

####**3). 用 “easy_install” 来安装 Pygments**

- 确保 easy\_install 已经正确安装，输入`easy_install --version`检查

- 使用 “easy_install” 来安装 Pygments
	
	```
	easy_install Pygments
	```

###**4.启动Jekyll**

进入待启动的网站目录，然后输入`jekyll serve`，然后既可以通过127.0.0.1:4000进行访问

###参考博客

1. [Windows 上安装 Jekyll ](http://blog.csdn.net/kong5090041/article/details/38408211)

2. [使用Jekyll在Github上搭建个人博客](http://segmentfault.com/a/1190000000406011)