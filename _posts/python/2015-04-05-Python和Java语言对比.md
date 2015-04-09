---
layout: post
title: Python和Java语言对比
category: python
tags: python
keywords: python java
description: 
---

现在一直习惯于用SSH做WEB开发，但是最近愈来愈感觉对于小的项目工程，Java的SSH框架过于沉重，所以经过调研发现Python语言比较方便，所以最近把python语法看了一遍，故把Python和Java中异同做下对比。

###**1. 缩进**

- python需要用缩进来识别语句之前的逻辑块，需要在行尾加上‘：’表示接下来缩进格式相同的语句是一个语句块【python语句末尾可以不加';',但是必须**采用缩进**】
- Java主要用‘{}’和‘；’来识别，不强制要求缩进（同样建议使用缩进格式）

###**2. 数**

- python只有四种数据：整数，长整数、浮点数和__复数__
- java则有char，short,byte，int，long，float,double类型

###**3. 字符串**

####**3.1. 字符串表示**

 -  Python中没有表示单个常量字符串类型的char类型，其可以用单引号‘’、双引号“”来表示一个字符串，也可以用三引号来表示一个多行字符串 
 -  Java中char表示单个字符，String表示一个字符串，常量字符字符串用双引号“”表示

####**3.2. 多行字符串**

 - Python在字符串末尾加上反斜杠（/）表示字符串在下一行继续
 - Java用加号（+）表示字符串在下一行继续

####**3.3. Python中其它的表示方法**

-  python中还有可以在字符串前加前缀r或R：表示自然字符串，即不对字符串做转移处理(比java方便
-  Python可以加前缀u或U：表示unicode字符串

###**4. 操作符**

- Python中**表示幂计算，如果 X**y表示 $X^y$
- Python中//表示整除，即商的整数部分
- Python中~表示按位翻转，~x就是-(x+1)

###**5. 接口与继承**

- Python中继承示例如下：

```python
class Fruit:
      def __init__(self, color):
           self.color = color
           print "fruit's color: %s" %self.color
 
      def grow(self):
           print "grow..."
```


```
class Apple(Fruit):                               #继承了父类
      def __init__(self, color):                  
           Fruit.__init__(self, color)            #显示调用父类的__init__方法（Python不会自动调用基本类的__init__()）
           print "apple's color: %s" % self.color
```

```
class Banana(Fruit):                              #继承了父类
      def __init__(self, color):                  
           Fruit.__init__(self, color)            #显示调用父类的__init__方法
           print "banana's color:%s" %s self.color
 
      def grow(self):                             #覆盖了父类的grow方法
           print "banana grow..."
```
>**注意：** Python 中的\__init\__（）方法类似与Java中的构造函数，Java构造函数中的self默认存在，不需要在构造函数声明的时候进行显示指明，但是Python需要在\__init__()函数中显示指明（但是ID调用时不用显示进行self传递）

- Python中的接口
Java中的接口接口是为了解决不能多继承的问题，由于Python中支持多继承，所以Python中没有接口的概念。
由于接口是特殊的抽象类，接口没有数据成员，而是一组未实现的方法的集合。要想实现接口的功能，完全可以用一个空的类来做。
例如：

```
    class Fruit():  
        def add(self):  
             pass  
        def remove(self):  
             pass  
```

###**6. 对象的序列化表示**

- Python中可以使用str（）或repr（）函数来实现对象的序列化
- Java中通过toString()方法来实现对象的序列化

###**7. 参数传递中的\*和\****



