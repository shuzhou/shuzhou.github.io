---
layout: post
title: ubuntu下MySQL开启远程连接
category: 配置
tags: 环境配置 linux
keywords: ubuntu MySQL
description: 
---

###1. mysql安装后密码无法登陆问题
- 这时你需要进入/etc/mysql目录下，然后查看里面的用户名和密码，然后输入`sudo vim debian.cnf  `
- 使用这个文件中的用户名和密码进入mysql,假如debian.cnf中的用户名为debian-sys-maint,则：`mysql -u debian-sys-maint -p `
- 按回车，这时需要你输入密码，复制debian.cnf中的密码（不要手动输入，因为容易产生错误）。
- 然后修改root用户的密码，如下操作

```
use mysql
show tables;//查看mysql数据库中的表，会看到一个user表。
select * from user;//查看一下这个表中是否有root用户，如果有：
update user set password=password("root") whereuser="root";//更改root用户进入mysql的密码。
flush privileges;
```
- quit退出mysql,然后用root登录 `mysql -u root -proot `

> 如果user表中没有root用户：用grant命令`grant all privileges on *.* to root@localhost identified by'123'`
其中*.*代表所有数据库中的所有表，即database name.your table'123'表示为root用户的密码。
>
>然后输入`flush privileges;`
>
>然后输入`select * from user;`查看一下user这个表中是否有root用户。如果有表示添加成功。

###2. 配置远程连接
- `vim /etc/mysql/my.cnf` 找到bind-address = 127.0.0.1
- 注释掉这行，如：#bind-address = 127.0.0.1 或者改为： bind-address = 0.0.0.0，此表示允许任意IP访问；或者自己指定一个IP地址。
- 重启 MySQL：`sudo /etc/init.d/mysql restart`
- 授权用户能进行远程连接 
  - `grant all privileges on *.* to root@"%" identified by "password" with grant option;`
  - `flush privileges;`
  > 第一行命令解释如下，*.*：第一个*代表数据库名；第二个*代表表名。这里的意思是所有数据库里的所有表都授权给用户。root：授予root账号。“%”：表示授权的用户IP可以指定，这里代表任意的IP地址都能访问MySQL数据库。“password”：分配账号对应的密码，这里密码自己替换成你的mysql root帐号密码。
