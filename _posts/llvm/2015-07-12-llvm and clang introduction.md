---
layout: post
title: llvm与clang简介
category: llvm
tags: clang 基本概念
keywords: linux clang
description: 
---

&#160; &#160; &#160; &#160;本篇文章主要针对llvm于clang的基本概念做个基本的阐述。刚开始接触llvm与clang的时候只知道clang是一个编译器，那llvm是什么？两者之间的关系是什么？为什么提到llvm必然会提到clang?本篇文章就这些基本概念做个简单的介绍。

###1. **llvm是什么？**###

&#160; &#160; &#160; &#160;llvm是low level virtual machine的简称，其实是一个编译器框架，供了与编译器相关的支持，能够进行程序语言的编译期优化、链接优化、在线编译优化、代码生成。llvm的主要作用是它可以作为多种语言的后端。

###2. **clang是什么？**###
&#160; &#160; &#160; &#160;官方介绍Clang是LLVM native的一个面向C/C++/Objective-C的编译器，目标是要提供一个编译非常快的编译器。

&#160; &#160; &#160; &#160;Clang一般被说是LLVM的一个前端。苹果公司认为GCC的前端越来越不好用，并且不能给苹果的IDE提供很好的服务，所以他们转向了LLVM，Clang的定位就是替代GCC的前端。

&#160; &#160; &#160; &#160;**总结：**Clang 是一个 C++ 编写、基于 LLVM、发布于 LLVM BSD 许可证下的C/C++/Objective C/Objective C++编译器，其目标（之一）就是超越 GCC。

###3. **llvm与clang的关系到底是什么？**###

&#160; &#160; &#160; &#160;我们需要先了解下LLVM的结构。

&#160; &#160; &#160; &#160;传统的静态编译器分为三个阶段：前端、优化和后端。示意图如下所示：

![图挂了，请联系zhangshuzhou.hi@163.com](http://7xiif2.com1.z0.glb.clouddn.com/2015-07-12-001.png "Optional title")

<div style="text-align:center">图1：传统的静态编译器分为三个阶段示意图</div>

&#160; &#160; &#160; &#160;llvm的三阶段的设计如下图所示：

![图挂了，请联系zhangshuzhou.hi@163.com](http://7xiif2.com1.z0.glb.clouddn.com/2015-07-12-002.png "Optional title")

<div style="text-align:center">图2：llvm的三阶段设计图</div>

其中clang就是llvm的一个前端，即图2所示的左边部分。

###4. **编译器为什么要如此设计？**###

&#160; &#160; &#160; &#160;这样做的优点是如果需要支持一种新的编程语言，那么我们只需要实现一种新的前端。如果我们需要支持一种新的硬件设备，那我们只需要实现一个新的后端。不论是支持新的编程语言，还是支持新的硬件设备，这里都不需要对优化阶段做修改。


###参考文献###
[LLVM每日谈之二 LLVM IR ](http://blog.csdn.net/snsn1984/article/details/8037414)