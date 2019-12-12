# Python综合

### 41.Python 常用的数据结构的类型及其特性？
------- | -------
数据结构 | 特性
list | 可变
set  | 可变，元素唯一
dict | 可变，字典中的键是不可变数据类型，可变数据类型不可作为字典的键
tuple | 不可变

### 42.如何交换字典 {"A"：1,"B"：2}的键和值？
字典推导式：
```python
d = {"A": 1,"B": 2}
res = {v: k for k, v in d.items()}
# res: {1: 'A', 2: 'B'}
```

### 43.Python 里面如何实现 tuple 和 list 的转换？
tuple转list：list(t)
list转tuple：tuple(l)

### 44.我们知道对于列表可以使用切片操作进行部分元素的选择，那么如何对生成器类型的对象实现相同的功能呢？
使用itertools.islice()：
```python
import itertools

# 斐波那契数列生成器
def fbnq(num):
	a, b = 1, 1
	for _ in range(num):
		a, b = b, a + b
		yield a

if __name__ == '__main__':
	generator = fbnq(10)
	# generator是一个迭代器: <generator object fbnq at 0x000001F12536BFC0>
	# 不能直接对生成器取值或切片，如generator[2],generator[2:]

	# itertools.islice对生成器进行切片：
	islice = itertools.islice(generator, 10, 20)
	# islice仍然是一个迭代器: <itertools.islice object at 0x0000022B4DAB3778>
	for x in islice:
        print(x)

```

### 45.请将[i for i in range(3)]改成生成器
```python
gennerator = (i for i in range(3))
```

### 46.a="hello"和 b="你好"编码成 bytes 类型
```python
a="hello"
a1 = a.encode()  
# 编码后 a1: b'hello'
# 检查编码后类型 chardet.detect(a1) : {'encoding': 'ascii', 'confidence': 1.0, 'language': ''}

b="你好"
b.encode()
b1 = b.encode()  
# 编码后 b1: b'\xe4\xbd\xa0\xe5\xa5\xbd'
# 检查编码后类型 chardet.detect(b1) :{'encoding': 'utf-8', 'confidence': 0.7525, 'language': ''}
```

### 47.下面的代码输出结果是什么？
```python
a = (1, 2, 3, [4, 5, 6, 7], 8)
a[2] = 2
```
答：由于元组是不可变数据类型，对其进行修改会报错。 ```TypeError: 'tuple' object does not support item assignment```

### 48.下面的代码输出的结果是什么?
```python
a = (1, 2, 3, [4, 5, 6, 7], 8)
a[3][0] = 2
```
a[3]是列表，可变数据类型，可以进行修改。这里修改的是元组的子对象而不是元组，元组的内存id不会改变，即引用没有改变，是允许的。