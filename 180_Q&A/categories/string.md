# Python字符串

### 19.列举 Python 中的基本数据类型？
类型名		 | 具体类型	
------------ | ------------
数值型(number)  | int， float， bool (True/False)，complex
字符串  | str
列表	 | list
元组	 | tuple
集合	 | set
字典	 | dict

### 20.如何区别可变数据类型和不可变数据类型
  类别		 | 类型名		| 特点	
------------ | ------------ | ------------
可变数据类型	 |  list，set， dict	 | 变量名指向的内存地址可以改变，对其修改是修改了当前地址内的对象。对可变数据类型使用“=”进行复制是浅拷贝，实际上相当于把两个名字不同的指针指向同一地址处的对象，修改其中一个时另外一个也会跟着改变，消除这种影响需要使用深拷贝。
不可变数据类型 | 	number，str，tuple | 	变量名指向的内存地址不可变，对其“修改”相当于重新赋值，会开辟一个新的内存地址来存放。

如何区别：
* 可变数据类型：在一个变量的内存id不变的情况下可以修改其值；
* 不可变数据类型：一个变量的值修改之后其内存id也跟着修改了，本质上不是同一个变量了。

### 21.将"hello world"转换为首字母大写"Hello World"
```python
def first_capitalize(sentence:str) -> str:
	'''
	所有单词首字母大写

	将句子中的每一个单词首字母均转化为大写并返回
	:param sentence: 要转化的句子
	:return: 转化后的句子
	'''
	words = sentence.split(' ')
	for i in range(len(words)):
		words[i] = words[i].capitalize()
	return ' '.join(words)

if __name__ == '__main__':
	sentence = 'hello world'
	print(first_capitalize(sentence))
```

一行代码版本：
```python
def first_capitalize(sentence:str) -> str:
	return ' '.join(list(map(lambda word: word.capitalize(), sentence.split())))
```

### 22.如何检测字符串中只含有数字?
使用isdigit()方法，若字符串string只由数字组成，```string.isdigit()```返回True，否则返回False。

### 23.将字符串"ilovechina"进行反转
方法1：使用列表的reverse函数（注意：字符串没有reverse函数）
```python
string = list(string)
string.reverse()
string = ''.join(string)
```

方法2：使用切片
```python
string[::-1]
```

方法3：使用reduce累加
```python
from functools import reduce
string = reduce(lambda x, y: y+x, string)
```

方法4：使用栈模拟栈的先进后出就成功翻转了
```python
# 模拟入栈
stack = list(string)
result_str = ''
for x in stack:
	# 模拟依次出栈，每次将最后的字符放进结果中
	result_str += stack.pop()
return result_str
```

### 24.Python中的字符串格式化方式你知道哪些？
1. % - 格式化：当字符串较长或参数较多时，可读性和可维护性很差。
```python
%s：字符
%d：整数
%f：浮点数
%x：十六进制整数
%r：原始字符串
```
2. str.format：字典传参时需要重写参数名，不够优雅。
```python
用中括号表示要传入的参数位置，format中的参数按中括号的顺序传入。

"Hello, {}. You are {}.".format(name, age)

支持字典形式传参，format中的参数不用严格按顺序传入。

"Hello, {name}. You are {age}.".format(name=name, age=age)
```

3. f-string格式，py3.6开始支持，形式和foramt类似，形式更为简洁优雅。{}内支持任意表达式，可在其中进行运算和函数调用，性能也比前两种更优。
```python
name = "Eric"
age = 74
f"Hello, {name}. You are {age}."
```

### 25.有一个字符串开头和末尾都有空格，比如“ adabdw ”,要求写一个函数把这个字符串的前后空格都去掉。
```python
去除左边空格：string.lstrip()
去除右边空格：string.rstrip()
去除两边空格：string.strip()
```

### 26.获取字符串”123456“最后的两个字符。
切片：```string[-2:]```

### 27.一个编码为 GBK 的字符串 S，要将其转成 UTF-8 编码的字符串，应如何操作？
str.encode()：将Unicode字符串编码成其他编码形式；
str.decode()：将编码后的字符串解码成未编码的Unicode字符串；
chardet.detect(str)：检查字符串类型并返回（需要import chardet）。

### 28. (1)s="info：xiaoZhang 33 shandong"，用正则切分字符串输出['info', 'xiaoZhang', '33', 'shandong'](2) a = "你好 中国 "，去除多余空格只留一个空格。
(1)正则切分字符串
1. 题意：去除字母和数字以外的字符；
2. compile：生成一个正则表达式对象；
3. \w：匹配包括下划线的任何单词字符。类似但不等价于“[A-Za-z0-9_]”，这里的"单词"字符使用Unicode字符集。\W：匹配任何非单词字符。等价于“[^A-Za-z0-9_]”。
```python
import re
pattern = re.compile(r'\W')
```
(2)去除多余空格
```python
# 使用去除空格的专用函数：
a.strip()	# 去除两端空格
a.rstrip()	# 去除右端空格
```

### 29. (1)怎样将字符串转换为小写 (2)单引号、双引号、三引号的区别？
(1)字符串转换：
1. 字符串中所有字符转大写：string.upper()
2. 字符串中所有字符转小写：string.lower()
3. 字符串中每个单词首字母大写：string.capitalize()
4. 字符串首个单词的首字母大写：string.title()

(2)单引号、双引号、三引号的区别：
1. 单引号和双引号都可以表示字符和字符串，没有区别。只是需要注意，当使用单引号来定义一个字符串时，字符串中的单引号需要转义，而双引号被视为普通字符无需转义。同理，当使用双引号来定义一个字符串时，其中的双引号需要转义而单引号不需要。
2. 当使用单引号或双引号定义字符串时，想要定义一个多行字符串时需要在换行时加上字符\，最终并不能真正换行，而是隔着一段空白。使用三引号可以方便的定义一个多行字符串，字符串在代码中换行则在输出时也会换行。
3. 三引号用于文档字符串docstring，解释函数的作用、输入、输出。
