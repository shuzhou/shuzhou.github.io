---
layout: post
title: VS2013下编译Tesseract-OCR
category: OCR
tags: 环境配置 文字识别 机器学习
keywords: 环境配置 OCR 文字识别
description: 
---


### 1. 所需环境说明

因为Tesseract在google code上，所以下载很多东西需要翻墙，如果不能翻墙的同学，可以根据文章整理的[文件链接](http://pan.baidu.com/s/1i4s2Rdz)进行打包下载。

[点此访问Tesseract-ocr Google code主页](https://code.google.com/p/tesseract-ocr/)

1. VS2013(建议版本统一，VS2015编译器增加了新的编译规则会导致代码失败)
- python2.7及以上（由于python3语法不向前兼容python2语法，所以请勿安装python3）
- jdk1.7及以上（图形界面调试环境需要使用）(配置参考[这里](http://zhangshuzhou.cn/2014/02/11/Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE%E5%8F%8A%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98.html))


### 2. 配置目录结构

1. [下载](http://code.google.com/p/leptonica/downloads/detail?name=leptonica-1.68-win32-lib-include-dirs.zip)`leptonica-1.68-win32-lib-include-dirs.zip`，解压到`C:\BuildFolder`(此目录可以是任何目录，此处只是以`C:\BuildFolder`目录为例)

2. 安装linux命令模拟器（因为Leptonica需要使用一些简单的linux命令，例如`rm`、`diff`、`sleep`等），官方推荐[cygwin](http://tpgit.github.io/UnOfficialLeptDocs/vs2008/installing-cygwin.html),下载`cygwin.setup-x86_64.exe`安装即可

	> 安装过程汇中源的选择需要注意

	经过以上步骤目录结构为：
	
		C:\BuildFolder\	
			  
			  include\
			     leptonica\
			     file1
				 file2
				 ......
			
			  lib\
			     giflib416-static-mtdll-debug.lib
			     giflib416-static-mtdll.lib
			     libjpeg8c-static-mtdll-debug.lib
			     libjpeg8c-static-mtdll.lib
			     liblept168-static-mtdll-debug.lib
			     liblept168-static-mtdll.lib
			     liblept168.dll
			     liblept168.lib
			     liblept168d.dll
			     liblept168d.lib
			     libpng143-static-mtdll-debug.lib
			     libpng143-static-mtdll.lib
			     libtesseract302.dll
			     libtesseract302.lib
			     libtesseract302d.dll
			     libtesseract302d.lib
			     libtesseract302-static.lib
			     libtesseract302-static-debug.lib
			     libtiff394-static-mtdll-debug.lib
			     libtiff394-static-mtdll.lib
			     zlib125-static-mtdll-debug.lib
			     zlib125-static-mtdll.lib


3. [下载Tesseract-OCR VS2008](http://code.google.com/p/tesseract-ocr/downloads/detail?name=tesseract-ocr-3.02-vs2008.zip)工程 `tesseract-ocr-3.02-vs2008.zip`，然后将结业文件夹内的`tesseract-ocr`文件夹命名为`tesseract-3.02`，拷到`C:\BuildFolder\`文件夹中

	文件夹结构如下：
	
		C:\BuildFolder\
			  
			  include\
			     leptonica\
			  lib\
		   	  tesseract-3.02\
			     vs2008\
			        ambiguous_words\
			        classifier_tester\
			        cntraining\
			        combine_tessdata\
			        dawg2wordlist\
			        doc\
			        include\
			        libtesseract\
			           libtesseract.vcproj
			        mftraining\
			        port\
			        shapeclustering\
			        sphinx\
			        tesseract\
			           tesseract.vcproj
			        unicharset_extractor\
			        wordlist2dawg\
			
			        tesseract.sln
			        tesshelper.py

 
4. 下载并解压[Tesseract-OCR源码](http://code.google.com/p/tesseract-ocr/downloads/detail?name=tesseract-3.02.tar.gz)文件`tesseract-ocr-3.02.02.tar.zip`，将得到的`tesseract-ocr`文件夹命名为`tesseract-3.02`，拷到`C:\BuildFolder\`文件夹中与原有的文件夹合并
 
	得到如下目录结构:
	
		C:\BuildFolder\		  
			  include\
			     leptonica\
			  lib\
			  tesseract-3.02\
				 api\
			     ccmain\
			     ccstruct\
			     ccutil\
			     classify\
			     config\
			     contrib\
			     cube\
			     cutil\
			     dict\
			     doc\
			     image\
			     java\
			     image\
			     neural_networks\
			     tessdata\
			     testing\
			     textord\
			     training\
			     viewer\
			     vs2008\
			     wordrec\

5. 检查`C:\BuildFolder\include\tesseract`是否存在，如过存在则删除。进入`C:\BuildFolder\tesseract-3.02\vs2008`目录，打开cmd控制台，然后运行`python tesshelper.py .. copy ..\..\include`

	目录结构结果如下：
	
		C:\BuildFolder\		  
			  include\
			     leptonica\
				 tesseract\
			  lib\
			  tesseract-3.02\
				 api\
			     ccmain\
			     ccstruct\
			     ccutil\
			     classify\
			     config\
			     contrib\
			     cube\
			     cutil\
			     dict\
			     doc\
			     image\
			     java\
			     image\
			     neural_networks\
			     tessdata\
			     testing\
			     textord\
			     training\
			     viewer\
			     vs2008\
		     wordrec\

### 3. 项目编译

1. 用VS2013打开`C:\BuildFolder\tesseract-3.02\vs2008\tesseract.sln`(忽略2013的提示即可)

2. 在以下四种编译模式中选择一种进行编译<模式名称记为`ConfigurationName`>，建议选择`DLL_Release`版本（某些机器缺少库，导致DLL_Debug版本无法启动）
		
		DLL_Debug
		DLL_Release
		LIB_Debug
		LIB_Release

3. 首先编译`libtesseract302`(在libtesseract302项目上右键->选择生成)
  
	编译完成后`C:\BuildFolder\tesseract-3.02\vs2008\<ConfigurationName>\`文件夹下新增如下文件：
	
		static libraries:
		   libtesseract302-static.lib
		   libtesseract302-static-debug.lib
	
		DLLs:
		   libtesseract302.lib  (import library)
		   libtesseract302.dll
		   libtesseract302d.lib (import library)
		   libtesseract302d.dll

	> 编译生成的文件会自动拷到`C:\BuildFolder\lib`下即可
	
	
	> 编译过程中会出现以下错误：

	
		1>  equationdetect.cpp
		1>..\..\ccmain\equationdetect.cpp : warning C4819: 该文件包含不能在当前代码页(936)中表示的字符。请将该文件保存为 Unicode 格式以防止数据丢失
		1>..\..\ccmain\equationdetect.cpp(251): error C2146: 语法错误: 缺少“}”(在标识符“銆”的前面)
		1>..\..\ccmain\equationdetect.cpp(251): error C2146: 语法错误: 缺少“;”(在标识符“銆”的前面)
		1>..\..\ccmain\equationdetect.cpp(251): error C2065: “銆”: 未声明的标识符
		1>..\..\ccmain\equationdetect.cpp(251): error C2146: 语法错误: 缺少“;”(在标识符“銆”的前面)
		1>..\..\ccmain\equationdetect.cpp(251): error C2065: “銆”: 未声明的标识符
		1>..\..\ccmain\equationdetect.cpp(251): error C2146: 语法错误: 缺少“;”(在标识符“銆”的前面)
		1>..\..\ccmain\equationdetect.cpp(251): error C2065: “銆”: 未声明的标识符
		1>..\..\ccmain\equationdetect.cpp(251): error C2143: 语法错误 : 缺少“;”(在“}”的前面)
		1>..\..\ccmain\equationdetect.cpp(253): error C2065: “kCharsToEx”: 未声明的标识符
		1>..\..\ccmain\equationdetect.cpp(253): fatal error C1903: 无法从以前的错误中恢复；正在停止编译
	
	
	> 解决办法如下：
	
	> 打开出错的文件，然后选择vs2013的菜单“文件 -- 高级保存选项”，在窗口中选择“简体中文（gb2312）-代码页936”，保存后重新编译生成`libtesseract302`


4. 然后再编译`tesseract`（在项目tesseract上选择右键生成）
	
	在对应编译模式的文件夹下将会产生可执行，其可执行文件下所示

		LIB_Release: tesseract.exe
		LIB_Debug:   tesseractd.exe
		DLL_Release: tesseract-dll.exe
		DLL_Debug:   tesseract-dlld.exe

5. 测试的`tesseract.exe`
	
	在`C:\BuildFolder\`目录下新建一个`testing`文件夹，然后将如下文件拷到当前目录

		liblept168d.dll//在C:\BuildFolder\lib目录下
		libtesseract302d.dll//在C:\BuildFolder\lib目录下
		tesseract-dll.exe//在C:\BuildFolder\tesseract-3.02\vs2008\<ConfigurationName>目录下

	选取一张含有文字的截图放到当前目录下，然后打开cmd控制台，输入如下命令进行识别测试

		tesseract-dll.exe test.jpg out
	
	如果运行成功，会在当前目录下生成out.txt文件，打开即为识别结果

	> 如果提示找不到英语语言包eng.traineddata，可以下载语言包按照提示放到对应目录下。

### 4. 安装图形界面调试环境

需要jar包列表如下	
	
	piccolo2d-core-3.0.jar//编译ScrollView.jar需要的
	piccolo2d-extras-3.0.jar//编译ScrollView.jar需要的
	ScrollView.jar//已编译好，在附录中

如果有人希望自己编译java代码，可以参考[官方说明](https://code.google.com/p/tesseract-ocr/wiki/ViewerDebugging)


1. 修改源码 

	在`tesseract\tesseractmain.cpp`的以下代码

		if (!api.ProcessPages(image, NULL, 0, &text_out)) {
		  fprintf(stderr, _("Error during processing.\n"));
		}

	之前加入

		api.SetVariable("tessedit_dump_pageseg_images", "true");    //show no lines and no image picture
		api.SetVariable("textord_show_blobs", "true");  //show blobs result
		api.SetVariable("textord_show_boxes", "true");  //show blobs' bounding boxes
		api.SetVariable("textord_tabfind_show_blocks", "true"); //show candidate tab-stops and tab vectors
		api.SetVariable("textord_tabfind_show_reject_blobs", "true");   //show rejected blobs
		api.SetVariable("textord_tabfind_show_initial_partitions", "true"); //show initial partitions
		api.SetVariable("textord_tabfind_show_partitions", "1");    //show final partitions
		api.SetVariable("textord_tabfind_show_initialtabs", "true");    //show initial tab-stops
		api.SetVariable("textord_tabfind_show_finaltabs", "true");  //show final tab vectors
		api.SetVariable("textord_tabfind_show_images", "true"); //show image blobs

	以上代码控制Tesseract输出所有结果。

2. 启动调试程序
	
	附件中`ScrollView.jar`是已经编译好调试程序，打开控制台输入`java -jar ScrollView.jar`即可运行服务端调试程序，如果该文件运行成功会在控制台输出以下信息：
		
		Socket started on port 8461

3. 启动OCR识别引擎
	
	打开控制台，输入`tesseract-dll.exe test.jpg out`命令启动OCR引擎，即可看到调试界面



