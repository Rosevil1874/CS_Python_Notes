# 语言基础

### 1.列出常用Python标准库和第三方库？

标准库		 | 第三方库	
------------ | ------------
import os	 | 操作系统相关操作	import numpy as np	数学
import sys	 | 命令行参数(sys.path)	import pandas as pd	数据分析模块
import re	 | 正则表达式	import matplotlib	画图
import random	 | 产生随机数	requests	http库
import math	 | 数学模块	scrapy 	爬虫
import datetime	 | 日期时间	flask/djongo	web框架
import threading	 | 线程	pytorch	机器学习
import multiprocessing	 | 进程	sikit-learn	机器学习
import glob	基于文件通配符搜索	 | pymysql	数据库

### 2.Python内建数据类型有哪些？
类型名		 | 具体类型	
------------ | ------------
数值型	 | int， float， complex
布尔型	 | bool (True/False)
字符串	 | str
列表	 | list
元组	 | tuple
集合	 | set
字典	 | dict

### 3.简述 with 方法打开处理文件帮我我们做了什么？
> [with方法详解](https://www.ibm.com/developerworks/cn/opensource/os-cn-pythonwith/)

• with语句适用于对资源进行访问的场合，无论是否发生异常都会进行必要的清理操作以释放资源，如文件使用后自动关闭，线程中自动进行锁的获取和释放等。
• with关键字后面跟着的语句会返回一个上下文管理器，上下文管理器在使用```__enter__()```方法进入运行时上下文，操作结束后使用```__exit__()```退出运行时上下文。
• 读文件：
![read_file](../images/read_file.png)
• 写文件：
![write_file](../images/write_file.png)


### 4.列出 Python 中可变数据类型和不可变数据类型，为什么？
  类别		 | 类型名		| 特点	
------------ | ------------ | ------------
可变数据类型	 |  list，set， dict	 | 变量名指向的内存地址可以改变，对其修改是修改了当前地址内的对象。对可变数据类型使用“=”进行复制，实际上相当于把两个名字不同的指针指向同一地址处的对象，修改其中一个时另外一个也会跟着改变，消除这种影响需要使用深拷贝。
不可变数据类型 | 	数值型，str，tuple | 	变量名指向的内存地址不可变，对其“修改”相当于重新赋值，会开辟一个新的内存地址来存放。

### 5.Python 获取当前日期？
```python
import datetime
datetime.datetime.now()
```

### 6.统计字符串每个单词出现的次数
```python
from collections import Counter
result = dict( Counter（string.split（））)

result = { word：string.split().count( word )  for word in string.split（）}
```

### 7.用 python 删除文件和用 linux 命令删除文件方法
```python
# python方法：
	import os
	os.remove（'demo.txt'）
# Linux方法：
	rm 'demo.txt'
```
	
### 8.写一段自定义异常代码
```python
if xxx: raise ValueError('你这个值有问题')    # 或者其他异常类型，抛出错误后就不会执行下面的语句了
else: print('很棒，没问题')
```

### 9.举例说明异常模块中 try except else finally 的相关意义
	• try：需要检测的异常代码片段
	• except：发生需要重点检查的异常类型时执行的操作
	• else：发生除了上面except中出现的异常以外其他的异常类型时执行的操作
	• finally：不管是否发生异常都会执行的代码段

### 10.遇到 bug 如何处理
	• 根据报错信息找到相应代码，一般的数据结构和算法错误一般找到就能解决；
	• 设置断点进行debug；
	• 上搜索引擎，看看人家怎么解决的类似问题；
	• 长时间解决不出来可以请教他人，别人可能迅速看出来问题而你自己看不出来，因为是你写的bug啊。。
	• 此路不通，绕道迂回。
