---
layout: post
title: Windows下搭建Tesseract-OCR开发环境
category: OCR  
tags: 环境配置 文字识别 机器学习
keywords: 环境配置 OCR 文字识别
description: 
---

&#160; &#160; &#160; &#160;OCR(Optical Character Recognition):光学字符识别,是指对图片文件中的文字进行分析识别，获取的过程。

&#160; &#160; &#160; &#160;Tesseract：开源的OCR识别引擎，初期Tesseract引擎由HP实验室研发，后来贡献给了开源软件业，后经由Google进行改进，消除bug，优化，重新发布。当前版本为3.02。

&#160; &#160; &#160; &#160;项目地址：[code.google.com/p/tesseract-ocr](code.google.com/p/tesseract-ocr)【google code由于被墙，访问需要翻墙】


###**1. 下载安装Tesseract-OCR引擎(3.0版本+才支持中文识别)**###


&#160; &#160; &#160; &#160;由于：[code.google.com/p/tesseract-ocr](code.google.com/p/tesseract-ocr)被墙，大家想下载也可以翻墙去下，地址为[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list)。

&#160; &#160; &#160; &#160;下载后直接点击安装，一路点击next即可。

&#160; &#160; &#160; &#160;为了方便我将自己的安装版本上传[tesseract-ocr-setup-3.02.02.exe](http://pan.baidu.com/s/1hmHhc)


###**2. 添加中文字库支持以识别中文**###


&#160; &#160; &#160; &#160;进入安装根目录，我们会发现安装目录下有tessdata目录，该目录存放的是语言字库文件，和在命令行界面中可能用到的参数所对应的文件。 

&#160; &#160; &#160; &#160;由于引擎默认安装只含了英文字库，没有包含中文字库，所以想要进行中文识别需要安装中文字体库。，可以到[https://code.google.com/p/tesseract-ocr/downloads/list]  下载对应的语言的字库文件。下载完成后解压，然后将该文件剪切到tessdata目录下去就可以了。

&#160; &#160; &#160; &#160;本机环境搭建所下载语言包[tesseract-ocr-3.02.chi_sim.tar.gz](http://pan.baidu.com/s/1pJKbNFt)


###**3. 进行文字识别测试**###

- 转到OCR引擎安装的根目录下，然后打开控制台，输入`tesseract`命令，测试该命令是否可用。

- 准备一张只含有英文和数字的图片进行测试英文识别测试

	```
	tesseract 1.png result //1.png是待识别的图片的文件名，result是识别结果输出的文档名称
	```

输入上述命令后，会发现文件夹中多了一个result文件,里面即使识别结果。

- 准备一张含有中文的图片进行中文识别测试
	
	```
	tesseract 1.png result  -l chi_sim //-l chi_sim 表示用简体中文字库
	```

###**附录**###

Usage:tesseract imagename outputbase [-l lang] [-psm pagesegmode] 

[configfile...]

pagesegmode values are:

0 = Orientation and script detection (OSD) only.

1 = Automatic page segmentation with OSD.

2 = Automatic page segmentation, but no OSD, or OCR

3 = Fully automatic page segmentation, but no OSD. (Default)

4 = Assume a single column of text of variable sizes.

5 = Assume a single uniform block of vertically aligned text.

6 = Assume a single uniform block of text.

7 = Treat the image as a single text line.

8 = Treat the image as a single word.

9 = Treat the image as a single word in a circle.

10 = Treat the image as a single character.

-l lang and/or -psm pagesegmode must occur before anyconfigfile.

tesseract imagename outputbase [-l lang] [-psm pagesegmode] [configfile...]

tesseract    图片名  输出文件名 -l 字库文件 -psm pagesegmode 配置文件

例如：

tesseract 1.png result  -l chi\_sim -psm 7 nobatch

-l chi\_sim 表示用简体中文字库（需要下载中文字库文件，解压后，存放到tessdata目录下去,字库文件扩展名为  .raineddata 简体中文字库文件名为:  chi_sim.traineddata）

-psm 7 表示告诉tesseract code.jpg图片是一行文本  这个参数可以减少识别错误率.  默认为 3

configfile 参数值为tessdata\configs 和  tessdata\tessconfigs 目录下的文件名

