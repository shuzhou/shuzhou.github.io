---
layout: post
title: ubuntu12.04重新配置llvm开发环境
category: 配置
tags: clang 环境配置
keywords: linux llvm 环境配置
description: 
---



&#160; &#160; &#160; &#160;近期小组用到llvm与clang进行项目开发，小组内部前期分别进行开发没有进行版本统一，但是后期进行系统集成测试的时候需要进行测试环境统一，由于自己之前安装的版本是3.5.1，测试的统一版本是3.6.0，所以需要重新安装llvm。将重新安装的步骤记录如下：

###**1. 卸载llvm3.5.1**
转到llvm安装的根目录，输入如下命令进行卸载llvm

```
sudo make uninstall
```

然后输入`clang --version`会发现clang已经被彻底删除

###**2.安装llvm3.6.0**
在正式开始安装llvm3.6.0之前，我们需要做一些准备工作，在[http://llvm.org/releases/download.html](http://llvm.org/releases/download.html)下载如下文件

- llvm源代码：llvm-3.6.0.src.tar.xz
- clang源代码：cfe-3.6.0.src.tar.xz
- compiler-rt源代码：compiler-rt-3.6.0.src.tar.xz

然后依次输入如下命令进行安装llvm

1).解压源代码，并配置对应目录结构

```
tar xf llvm-3.6.0.src.tar.xz
mv llvm-3.6.0.src llvm

cd llvm/tools
tar xf cfe-3.6.0.src.tar.xz
mv cfe-3.6.0.src clang

cd ../projects
tar xf compiler-rt-3.6.0.src.tar.xz
mv compiler-rt-3.6.0.src compiler-rt
```

2).配置编译选项

```
cd ..
./configure --enable-optimized CC=gcc CXX=g++
```

3).编译llvm

```
make -j2 //-j2代表用2线程进行源码编译
```
编译成功后提示

```
llvm[0]: ***** Completed Release+Asserts Build
```

4).安装编译好的llvm

```
make install
```

5).检查clang的版本

```
clang --version
```

如果还是旧版本，需要将/usr/bin/clang指向clang 3.6.0：

```
ls -s /usr/local/bin/clang /usr/bin/clang
```
