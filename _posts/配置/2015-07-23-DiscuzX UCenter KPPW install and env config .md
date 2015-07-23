---
layout: post
title: DiscuzX UCenter KPPW安装与配置
category: web
tags: 环境配置 web开发
keywords: 
description: 
---

注意点：

1. 下载的三个文件的安装包的编码要一致，否则整合容易失败

2. 本次安装配置所使用版本信息
	- Discuz! X3.2
	- UCenter 1.6.0
	- KPPW2.6.2

###**1.安装三个系统**

安装时Ucenter在discuz之前安装即可，安装顺序没有其他额外要求。

- 按照官方安装说明安装kkpw
- 按照官方安装说明安装Ucenter
- 按照官方安装说明安装Discuz
	- 安装时选择`仅安装 Discuz! X (手工指定已经安装的 UCenter Server)`
	- 填写`UCenter 的 URL`一项是，不论是在服务器配置还是在本地配置都选择填写`http://127.0.0.1/UCenter安装的路径`，因为直接填写公网ip的话discuz无法识别，然后需要后期手动修改配置文件（修改方法详见第二章节问题1）


###**2.修改配置文件**

####1. 问题1：Discuz中集成的UCenter无法访问的问题####

- **问题描述：**

&#160; &#160; &#160; &#160;登录Discuz后台会发现discuz中已经集成了UCenter,如果配置是在服务器进行，则UCenter点击后无法访问

- **解决办法：**

&#160; &#160; &#160; &#160;修改discuz/config/config\_ucenter.php,将`UC_API`的值改为UCenter的实际访问地址


####2. 问题2：UCenter集成的应用Discuz通信失败####

- **问题描述：**

&#160; &#160; &#160; &#160;登录Ucenter点击应用管理，看下整合的应用是否通信成功，如果没有通信成功请修改配置内容

- **解决办法：**

	- 确保应用的主URL是正确的
	- 应用IP如果空着请填写127.0.0.1
	- 确保两边通信秘一致

###**3.在kppw中配置UCenter**
- 全局配置->会员整合->开启

- 注意UCenter连接方式请选择mysql，否则容易出错

- `UCenter IP 地址:`填写127.0.0.1（服务器整合的话没有填写该项可能会失败）

- `UCenter应用 ID:`填写UCenter整合应用中最大ID号+1

- 进入UCenter查看通信是否成功，如果不成功按照如下思路进行排查
	- `应用的主 URL:`是否正确
	
	- `应用 IP:`填写是否是127.0.0.1

	- 两边的通信密钥是够一致


###**4.测试同步注册**

- 在KPPW于Discuz分别注册一个账号，然后观察UCenter中是否有该账号，如果有则同步注册已经成功一半
	- 若出现KPPW无法注册或者登录的情况，请检查KPPW于Discuz中的config_ucenter.php中内容除`UC\_KEY`和`UC\_APPID`项内容外全部一致，不一致时请参考Discuz配置文件修改KPPW配置文件

- 在KPPW中用Discuz中刚才注册的账号登录，检测能否登录成功，登录成功后则KPPW数据库中添加了Discuz中刚才注册的账号

- 同理在Discuz中用KPPW中刚才注册的账号登录，检测能否登录成功，登录成功后则Discuz数据库中添加了KPPW中刚才注册的账号

如果以上步骤均成功执行，则说明三个系统的同步注册已经整合成功


###**4.测试同步登录与注销**

- 在KPPW中登录一个账号，然后访问Discuz会发现该账号已经登录（注意：所登录的账号必须在两个系统的数据库已经存储）

- 在Discuz中登录一个账号，然后访问KPPW会发现该账号已经登录（注意：所登录的账号必须在两个系统的数据库已经存储），如果失败请参考下面内容：

	- Discuz设置`站长->Ucenter设置->是否允许其他应用的会员在站点激活:`选择是
	
	- 打开两个系统uc\_client\data\cache\apps.php文件对比差异(发现KPPW的apps.php文件中的内容较Discus中apps.php文件多了一项配置)
	
	- 将KPPW的apps.php文件中的多出的配置复制到Discus中apps.php文件中，然后重新测试，发现已经成功


