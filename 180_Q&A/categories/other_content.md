# Python 其他内容


### 91.解释一下 python 中 pass 语句的作用？
pass是空语句，不做任何操作，一般用作占位，为了保证结构完整性。  
一般在搭建程序框架或写if语句的时候使用。


### 92.简述你对 input()函数的理解
input()接收用户输入。  
python2中input()接收其他数据为字符串，接收纯数值为数值(int, float)，rawinput()接收的数据为字符串。  
python3中只有input()，数据类型为字符串。


### 93.python 中的 is 和==
* is 是身份运算符，判断两个对象内存id是否相等（即：是否为同一对象）；
* == 是比较运算符，判断两个对象的值是否相等；


### 94.Python 中的作用域
* **作用域**：也就是命名空间，python创建、修改和查找变量都在命名空间中。变量在赋值创建时，其赋值的地方决定了其命名空间，即他的可见范围。
* **LEGB**：

	L(Local)：局部作用域；
	E(Enclosing): 内层函数引用到了外层函数的变量就成了闭包，这个外层函数的变量就是闭包作用域。；
	G(Global): 全局作用域，global声明的全局变量；
	B(Built-in): 内建作用域,是一个名为builtins的内置模块，但是必须要导入之后才能使用内置作用域；
	使用LEGB的顺序查找


### 95.三元运算写法和应用场景？
`res = True if a > b else False`：a>b为条件，条件为真时结果为True，否则结果为False。


### 96.了解 enumerate 么？
enumerate()函数用于将可迭代对象（list,set,string等）组合成（索引，数据）的形式，一般用在for循环中遍历。  
`enumerate(sequence, [start=0])`


### 97.列举 5 个 Python 中的标准模块。
os, re, random, math, datetime, threading, multiprocessing, functools, numpy, pandas, matplotlib, pytorch, sikit-learn, pymysql


### 98.如何在函数中设置一个全局变量
1. 在所有函数体外定义的变量均为全局变量；
2. 使用 global 关键字定义的变量均为全局变量。


### 99.pathlib 的用法举例
pathlib 模块提供了一组面向对象的类，这些类可以代表各操作系统上的路径，程序可以使用这些类操作路径。  
可用于查看路径，拼接路径，读写文件。
```python
from pathlib import Path

print(Path.cwd())		# 当前工作路径
print(Path.home())		# home路径
```


### 100.Python 中的异常处理，写一个简单的应用场景
举个栗子，写文件的时候检查是否有权限：
```python
try:
	# 待检查的代码块
	file = open('test.text', 'w')
	file.write('test somthing')
except IOError as e:
	# 想要检测的异常类型
	print('except: ', e)
else:
	# 若没有发生异常
	print('200 OK')
finally:
	# 无论前面结果如何都会执行
	print('I am always here')
```


### 101.Python 中递归的最大次数，那如何突破呢？
* 不同系统和python版本的最大递归次数不同，可以查看：我的win10为1000次；超过递归最大深度会引发不可预知的错误，如C栈溢出或其他错误。
* 突破：手动设置。
```python
import sys
version = sys.version				# python版本
limit = sys.getrecursionlimit()		# 最大递归深度

print(version)						# 3.6.3
print(limit)						# 1000

sys.setrecursionlimit(3000)			# 手动设置最大递归深度
limit = sys.getrecursionlimit()			
print(limit)						# 3000
```


### 102.什么是面向对象的 mro
MRO： Method Resolution Order（方法解析顺序）。  
MRO是类的方法的解析顺序表，也就是继承父类方法时的解析表。  
MRO是多继承和钻石继承的问题上的核心内容，规定了什么时候、如何调用父类的方法。  
`类名.__mro__`：输出类的解析继承关系顺序。

```python
class A:
	def f(self):
		print('A')

class B(A):
	def f(self):
		print('B')

class C(A):
	def f(self):
		print('C')

class D(B, C):
	def f(self):
		super().f()			# 调用B的函数
		super(B, self).f()	# 调用C的函数

if __name__ == '__main__':
	print(D.__mro__)
	# (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
	# class A 继承自object

	obj_d = D()
	obj_d.f()		
```


### 103.isinstance 作用以及应用场景？ 
* **用法**：`isinstance(obj, calssinfo)`，obj为实例对象，classinfo可以为直接或间接类名、基本类型、或他们的元组。  
* **场景**：判断对象的数据类型，判断类的继承关系。type无法判断继承关系。
```python
class A:
	pass

class B(A):
	pass

print(isinstance(A(), A))	# True
print(type(A()) == A)		# True
print(isinstance(B(), A))	# True
print(type(B()) == A)		# False
```


### 104.什么是断言？应用场景？
assert用于判断一个表达式，当表达式为False的时候返回错误。  
断言可以在不满足条件的情况下直接返回错误，而不必等到程序运行失败。  
场景：如程序只能在Linux运行，可以在运行之前判断是否满足。
```python
assert expression [, args]

# 相当于
if not expression:
	raise AssertionError(args)
```


### 105.lambda 表达式格式以及应用场景？
lambda表达式即为匿名函数，通常用在函数体很简单的情况下，用lambda表达式替代函数定义。  
用法： `lambda 参数1, 参数2... : 参数表达式`  
场景：

	功能简单的函数；
	不用关注命名的函数；
	只用一次或很少复用的函数

例1：按绝对值排序
```python
list_demo = [3, 5, -4, -1, 0, -2, -6]
res = sorted(list_demo, key = lambda x: abs(x))
```

例2：输出1-100内的奇数
```python
res = list(filter(lambda x: x % 2 == 1, range(1,101)))
```

例3：闭包lambda
```python
def outer(a, b):
	return lambda x: a*x + b

out = outer(2, 2)
print(out(3))		# 输出8
```


### 106.新式类和旧式类的区别
**区别：** 新式类多继承搜索顺序为广度优先：先在水平方向查找，再向上查找。旧式类多继承搜索顺序为深度优先：先深入继承树，再返回。  
**实现：**   
python2中默认都是经典类，只有显式继承了object的类才是新式类：  
* class A(object): pass  	# 新式类
* class A(): pass  	# 经典类
* class A: pass  	# 经典类  
python3中取消了经典类，默认都是新式类，且不需要显式继承object：  
* class A(object): pass  	# 新式类，推荐写法
* class A(): pass  		# 新式类
* class A: pass  		# 新式类  



### 107.dir()是干什么用的？
* dir() 不带参数时，返回当前作用域的所有变量、方法和定义的类型列表；
* dir() 带参数时，返回参数的属性、方法。
```python
class A:
	def f(self):
		print('A')


if __name__ == '__main__':
	print(dir())
	# ['A', '__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__']

	print(dir(A))
	# ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'f']
```


### 108.一个包里有三个模块，demo1.py, demo2.py, demo3.py，但使用 from tools import \*导入模块时，如何保证只有 demo1、demo3 被导入了。
在Python包中新建__init__.py文件确认导入的包，文件内容如下：
```python
from Demo1 import demo1
from Demo2 import demo2
```


### 109.列举 5 个 Python 中的异常类型以及其含义
	KeyboardInterrupt：用户中断执行（一般是输入^C）；
	MoudleNotFoundError：无法找到模块或找到的是None
	RecursionError：超过递归最大深度；
	TimeoutError：函数在系统级别超时；
	IndentationError：缩进错误；
	SystemError：解释器发现内部错误；
	TypeError：操作或函数发现类型错误的参数；
	ValueError：操作或函数发现类型正确但值错误的参数；
	KeyError：映射中没有这个键；


### 110.copy 和 deepcopy 的区别是什么？
* copy：浅拷贝，仅拷贝对象本身，不拷贝其引用；浅拷贝不会为子对象创建地址空间，当拷贝后的对象的子对象发生改变后，原对象的子对象也改变。
* deepcopy：深拷贝，拷贝对象和其引用的对象；深拷贝会为子对象创建新的地址空间，拷贝后的对象的子对象只是初始化成了和原对象的子对象同样的值，其修改不会相互影响。
```python
import copy

a = [1, 2, [3, 4], 5]

cp = copy.copy(a)
deep_cp = copy.deepcopy(a)

a[0] = 0		# 修改对象
a[2][0] = 0		# 修改子对象

print(cp)		# [1, 2, [0, 4], 5]
print(deep_cp)	# [1, 2, [3, 4], 5]

```


### 111.代码中经常遇到的`*args, **kwargs` 含义及用法。
* `*args`： 传入一个包含任意元素的位置参数元组，\*用于解压缩元组；
* `**kwargs`: 传入一个包含任意元素的关键字参数字典，\*\*用于解压缩字典；
* 位置参数必须位于关键字参数之前，用于定义时无法确定参数个数的函数。
```python
def fun(*args, **kwargs):
	print(args)		# (1, 2, 3)
	print(kwargs)	# {'a': 4, 'b': 5}

fun(1, 2, 3, a = 4, b = 5)
```


### 112.Python 中会有函数或成员变量包含单下划线前缀和结尾，和双下划线前缀结尾，区别是什么?
* 单下划线开头：通常用于模块， 模块内以单下划线开头的变量和方法默认划入模块内部范围。在使用`from module import *`的时候不会引入，在使用`import module`时会引入。
* 单下划线结尾：单下划线结尾通常用于用户自定义变量或方法名与python内置关键字冲突时，加上一个下划线在结尾以示区别。不推荐这样，最好重新命名。
* 双下划线开头结尾：python的魔术对象，比如用于面向对象的`__new__, __init__, __del__`，用于类的`__class__, __call__`，用于属性操作的`__getattr__, __setattr__, __delattr__`, 用于迭代器的`__iter__, __next__`，用于上下文管理器的`__enter__, __exit__`。


### 113.w、a+、wb 文件写入模式的区别
r：读文件，文件不存在会报错；
w：写文件，文件不存在时新建文件，存在时会覆盖原数据；
a：追加数据，文件不存在时新建文件，存在时不会覆盖原数据；
rb，wb：同上，操作二进制文件；
r+：可读可写，文件不存在时报错；
w+：可读可写，文件不存在时新建文件，存在时会覆盖原数据；
a+：可读可追加，文件不存在时新建文件，存在时不会覆盖原数据；


### 114.举例 sort 和 sorted 的区别
* sort是列表的方法，直接在原列表排序；
* sorted是函数，不改变原可迭代对象，而是返回新的排序好的对象。


### 115.什么是负索引？
负索引是指使用负数作为索引，-a代表倒数第a位。


### 116.pprint 模块是干什么的？
pprint用于整齐美观的输出数据。
```python
import pprint

a = [str(i) * 10 for i in range(10)]
pp_obj = pprint.PrettyPrinter(indent = 4)	# 句首缩进
pp_obj.pprint(a)	# 缩进+分行 输出
print(a)			# 一行输出
```


### 117.解释一下 Python 中的赋值运算符
`=, +=, -=, *=, **=, /=, //=, %=`


### 118.解释一下 Python 中的逻辑运算符
`and, or, not`


### 119.讲讲 Python 中的位运算符
`&, |, ^(a^a=0, a^0=a), ~(~x = -x-1), <<, >>`


### 120.在 Python 中如何使用多进制数字？
* 二进制：'0b/0B'加上01串为二进制数，使用int()和bin()进行二进制与十进制之间的转换。
* 八进制：'0o/0O'加上范围为1-7的字符串为八进制数，使用int()和oct()进行二进制与十进制之间的转换。
* 十六进制：'0x/0X'加上范围为[1-9,A-F]的字符串为十六进制数，使用int()和hex()进行二进制与十进制之间的转换。
```python
# 二进制
print(int(0b101))	# 5
print(bin(5))		# 0b101

# 八进制
print(int(0o12))	# 10
print(oct(11))		# 0o13

# 十六进制
print(int(0xFF))	# 255
print(hex(17))		# 0x11
```


### 121.怎样声明多个变量并赋值？
`a, b = 1, 2`