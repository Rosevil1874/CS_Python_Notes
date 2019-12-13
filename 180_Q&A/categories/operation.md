# Python操作类题目

### 49.Python 交换两个变量的值
```python
a, b = b, a
```
### 50.在读文件操作的时候会使用 read、readline 或者 readlines，简述它们各自的作用
* read: 读取整个文件，将文件内容放到一个字符串变量中。如果文件过大，一次读取全部内容到内存容易造成内存不足，更推荐大家使用逐行读取文件的方式。
* readline: 读取文件中的一行，包含最后的换行符“\n”，返回的是一个字符串对象，保持当前行的内存。
* readlines: 每次按行读取整个文件内容，包含最后的换行符“\n”，将读取到的内容放到一个字符串列表中，返回list类型。

```python
with open('path.txt') as file:
	file_content = file.read()
	line_content = file.readline([size]) 	# size参数可选，指定一次最多读取的字符数
	lines_content = file.readlines()
```

### 51.json 序列化时，可以处理的数据类型有哪些？如何定制支持 datetime 类型？
* 序列化：把python的对象编码转换为json格式的字符串，反序列化：把json格式字符串解码为python数据对象。
* 序列化时可以处理的数据类型：列表、元组字典、字符、数值、布尔值、None。(没有set和datetime)
* 定制datetime类型：
```python
from datetime import datetime
import json
from json import JSONEncoder

class DatetimeEncoder(JSONEncoder):
	'''扩展JSONEcoder中的default方法

	判断传入类型是否为datetime类型：
	若是则转为str字符，否则返回父类的值
	'''
	def default(self, o):
		if isinstance(o, datetime):
			return o.strftime('%Y-%m-%d %H:%M:%S')
		else:
			return super(DatetimeEncoder, self).default(o)

if __name__ == '__main__':
	dict_demo = {'name':'Renee', 'data':datetime.now()}
	print(json.dumps(dict_demo,cls=DatetimeEncoder))
```
* isinstance(object, classinfo)认为子类是一种父类类型，考虑继承关系；type(object)不会认为子类是一种父类类型，不考虑继承关系。
* super(type[, object-or-type])：调用父类的方法；
* json.dumps()：将 Python 对象编码成 JSON 字符串。


### 52.json 序列化时，默认遇到中文会转换成 unicode，如果想要保留中文怎么办？
将dumps的默认参数 ensure_ascii 设置为False。

### 53.有两个磁盘文件 A 和 B，各存放一行字母，要求把这两个文件中的信息合并(按字母顺序排列)，输出到一个新文件 C 中。
分为三步：读文件、信息合并、写文件。
```python
def read_file(file_path):
	'''读文件

	读取文件并返回文件内容
	:param file_path: 文件路径
	:return: 文件内容
	'''
	with open(file_path, 'r') as file:
		return file.read()


def write_file(file_path, file_data):
	'''写文件
	
	将数据写入指定文件中
	:param file_path: 要写入的文件路径
	:param file_data: 要写入的数据
	:return: 
	'''
	with open(file_path, 'w') as file:
		file.write(file_data)


def letter_sort(letter_str, reverse_flag=False):
	'''按字典排序

	:param letter_str: 需要排序的字母字符串
	:param reverse_flag: 排序顺序，False为正序，True为反序
	:return: 排序后的新字符串
	'''
	return ''.join(sorted(letter_str, reverse=reverse_flag))


if __name__ == '__main__':
	data1 = read_file('test1.txt')
	data2 = read_file('test2.txt')
	new_data = letter_str(data1 + data2)
	write_file('new.txt', new_data)
```

### 54.如果当前的日期为 20190530，要求写一个函数输出 N 天后的日期，(比如 N 为 2，则输出 20190601)。
```python
from datetime import datetime
from datetime import timedelta


def date_calculation(now_date, offset):
    '''获取日期

    获取几天前或几天后的日期
    :param now_date: 当前日期
    :param offset: 日期偏移量，负数为向前偏移
    :return: 偏移后的日期
    '''
    now_date = datetime.strptime(now_date, '%Y-%m-%d').date()
    offset_date = timedelta(days=offset)
    return (now_date + offset_date).strftime('%Y-%m-%d')


if __name__ == '__main__':
    print(date_calculation('2019-12-13', 7))
```

### 55.写一个函数，接收整数参数 n，返回一个函数，函数的功能是把函数的参数和 n 相乘并把结果返回。
闭包：
* 将内部函数的引用作为返回值；
* 保存运行环境，在闭包内的变量不能被轻易修改；
* 提高代码复用性。
```python
def out_func(n):
    '''闭包函数

    :param n: 整数参数n
    :return: 内层函数
    '''
    def in_func(num):
        return num * n

    return in_func


if __name__ == '__main__':
    demo = out_func(3)
    print(demo(4))
```
此例中n=3, num=4, 最后输出12.


### 56.下面代码会存在什么问题，如何改进？
```python
def strappend(num):        # 函数作用、参数意义不明，需要加注释
	str = 'frist'          # 不能使用关键字"str"作为变量名
	for i in range(num):   # 遍历得到的元素"i"意义不明，无注释
		str += str(i)      # 变量名和关键字在这个时候重名，必定报错，没有了str()方法
return str
```

修改后的代码：
```python
def str_append(num):
    '''字符串添加

    :param num: 添加数字【0到num-1】到字符串末尾
    :return: 修改后的字符串
    '''
    s = 'frist'
    # 获取数字0~num-1，添加到字符串末尾
    for i in range(num):
        s += str(i)
    return s


if __name__ == '__main__':
    print(strappend(5))
```

### 57.一行代码输出 1-100 之间的所有偶数。
```python
print([i for i in range(101) if i % 2 == 0])
```

### 58.with 语句的作用，写一段代码？
### 59.python 字典和 json 字符串相互转化方法
### 60.请写一个 Python 逻辑，计算一个文件中的大写字母数量
### 61. 请写一段 Python连接 Mongo 数据库，然后的查询代码。
### 62.说一说 Redis 的基本类型。
### 63. 请写一段 Python连接 Redis 数据库的代码。
### 64. 请写一段 Python 连接 MySQL 数据库的代码。
### 65.了解 Redis 的事务么？
### 66.了解数据库的三范式么？
### 67.了解分布式锁么？
### 68.用 Python 实现一个 Reids 的分布式锁的功能。
### 69.写一段 Python 使用 Mongo 数据库创建索引的代码。
