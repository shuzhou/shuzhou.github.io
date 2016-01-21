---
layout: post
title: 使用extundelete恢复linux上被删除的文件
category: 其它
tags: 数据恢复 linux
keywords: 数据恢复 linux
description: 
---


### 1.背景简述

&#160; &#160; &#160; &#160;最近项目刚上线，前端有些bug需要修改，然后直接在服务器上进行的修改，我重新部署的时候，打算删了久的备份，然后重新备份一份就部署一下，然后一不小心用了`rm -r edu.*`命令，然后以`edu`开头的所有的文件夹都被删了（不清楚为啥这个命令会删除掉`edu`文件夹，不应该是删除`edu.*`文件夹么？），当然也包括这段时间修改好bug代码的`edu`文件夹！！然后只能尝试使用恢复软件进行修复。

使用以上命令删除的是如下所示红色框框中的文件：

![](http://i.imgur.com/PEPATJV.png)


所以以后使用rm 命令一定要三思而后行阿！

### 2.注意事项及常用工具说明

> 其实我们删除文件时，文件在磁盘上并没有真正的删除，只是系统对这些文件进行了删除标记，以后写入新文件时才会覆盖掉这些被删除的文件 

> 所以进行文件恢复的时候，一定要记得切勿对原磁盘进行写入操作，最简单的方式是再挂载一块磁盘上去，所有的恢复软件安装及恢复文件的位置全在新的磁盘上进行


参考这篇博客[http://blog.csdn.net/chinalinuxzend/article/details/3990658](http://blog.csdn.net/chinalinuxzend/article/details/3990658)得知了常用的恢复软件如下

1. The Sleuth Kit [http://www.sleuthkit.org/sleuthkit](http://www.sleuthkit.org/sleuthkit)[Autopsy是它的一个图形前端)
2. [Foremost](http://foremost.sourceforge.net)
3. Finaldata[未找到对应的资料]:

	一个全能的工具，Finaldata,可以恢复unix/linux/dos下误删的文件。对于unix，支持这些产品,Solaris、AIX和HP-UX。对于linux，支持EXT2的文件系统。对于dos，支持FAT 12/16/32, NTFS 4/5/5.1 的文件系统。
- debugfs 恢复ext3被rm的资料
- ext4magic
- e2fsprogs
- photorec 

	[参考文章链接](http://www.91cto.com.cn/detail/udepnxs/)
	第一尝试使用的工具就是`photorec`,这个工具可以自己指定恢复目录，可以选择恢复文件的格式，但是他的特点如下：
	- 恢复文件的目录是 类似recup_dir.1的目录存储的，到达一定数量后会按数字一次新建目录。
	- 恢复后文件有可能后缀会稍有差别，这是我遇到的情况，有可能之前是png后缀的图片恢复后是gif格式。这有可能和文件头有关系。
	- 恢复后的文件采用系统规则命名，所以文件名有所改变。
	
	由于不能根据删除的目录恢复，所以导致删除文件全在一起，所以其对照片之类的文档恢复绝对是利器，但是针对目前的情况就不适合了。

- testdisk
	[参考文章链接](http://www.91cto.com.cn/detail/udepnxs/)
	当时看到了这个感觉简直是神奇阿，可以根据删除的文件夹恢复，所以我当时尝试photorec不理想的情况下，testdisk成为了第二个尝试。
    使用过程汇中虽然可以看到删除的文件和文件夹，但是自己恢复出来的文件都是空的，不知道是不是自己使用的方式不对，所以这种工具我使用失败
- extundelete
	
	看名字就知道专门对于ext文件系统进行文件恢复的工具。下面将会详细介绍。

### 3.extundelete使用说明

系统中磁盘及分区情况如下：

![](http://i.imgur.com/3XDcdJW.jpg)

其中`sdb1`是文件被删除之后挂载上去的一块新的磁盘`/dev/mapper/Template--vg-root`是被删除文件所在磁盘

#### 3.1 安装extundelete

1. 下载文件 	

		wget http://nchc.dl.sourceforge.net/project/extundelete/extundelete/0.2.4/extundelete-0.2.4.tar.bz2

2. 解压后进行编译安装

		./configure --prefix=/temp-disk/install/
		make && make install

> 在实际线上恢复过程中，切勿将extundelete安装到你误删的文件所在硬盘，这样会有一定几率将需要恢复的数据彻底覆盖。

### 3.2数据恢复

> 任何的文件恢复工具，在使用前，均要将要恢复的分区卸载或挂载为只读，防止数据被覆盖使用

直接运行对应文件夹下的`extundelete`即可

其中一些参数可以用`./extundelete --help`进行查看。

此处简单介绍几个自己恢复的过程中用到的几个参数：

	--restore-all //恢复所有删除的文件
	--restore-dir your_dir/  //恢复your_dir中删除的文件
	--after time //恢复指定时间戳(time)之后删除的文件
	--before time //恢复指定时间戳(time)之前删除的文件

例如我是在2016-1-20下午2：00以后删除的文件

	date -d "Wed Jan 20 14:00:00 CST 2016" +%s

得出时间戳为1453269600

例如我需要恢复指定删除的文件夹，则输入如下命令：

	./extundelete  /dev/mapper/Template--vg-root --after 1453269600 --restore-dir /usr/local/tomcat7/webapps/