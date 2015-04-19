---
layout: post
title: IBMSyntheticDataGenerator(数据生成器)的使用
category: 数挖
tags:  机器学习 数据挖掘
keywords: 数据挖掘 序列生成器
description: 
---

####1. SyntheticDataGenerator简介
&#8194;&#8194;&#8194;&#8194;该工具支持三种生成模式：

- 参数_list_代表生成交易事务数据
- 参数_tax_代表生成分类数据
- 参数_seq_代表生成序列数据

&#8194;&#8194;&#8194;&#8194;由于本次自己用到了的是序列数据生成功能，所以就序列数据的生成使用做详细讲解。

####2. SyntheticDataGenerator下载

在[http://synthdatagen.codeplex.com/releases/view/60659](http://synthdatagen.codeplex.com/releases/view/60659)下载文件

####3. SyntheticDataGenerator初步体验使用

&#8194;&#8194;&#8194;&#8194;该工具的具体使用详见[http://synthdatagen.codeplex.com/documentation](http://synthdatagen.codeplex.com/documentation)，由于在使用过程中发现与官网文档所述稍有不同，故做简单使用记录如下：

- 打开SyntheticDataGenerator下载文件夹，新建一个一\.bat结尾的文件，文件名任意，内容为SyntheticDataGenerator seq -fname test
- 保存文件，并双击运行该文件
- 观察文件夹下多出了四个文件，分别为test\.config、test\.lit\.patterns、test\.seq\.patterns、test\.sequences

####4. SyntheticDataGenerator序列数据生成详解

#####使用
&#8194;&#8194;&#8194;&#8194;命令SyntheticDataGenerator seq options，其中详细可供选择的参数如下：

<table>
	<tr>
		<th>参数</th>
		<th>值类型</th>
		<th>描述</th>
		<th>默认值</th>
	</tr>	
	<tr>
		<td>-fname</td>
		<td>文件名</td>
		<td>输出文件的文件名（不包含后缀）</td>
		<td>没有默认值【必选项】</td>
	</tr>
	<tr>
		<td>-tlen</td>
		<td>double</td>
		<td>交易事务长度</td>
		<td>2.5</td>
	</tr>
	<tr>
		<td>-nitems</td>
		<td>iteger</td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
		<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
	</tr>
</table>