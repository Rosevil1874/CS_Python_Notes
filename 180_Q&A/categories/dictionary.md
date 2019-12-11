# Python字典

###36.字典操作中 del 和 pop 有什么区别
1. demo_dict.pop(key[,default])：  
key：删除键key对应条目并返回其键值；
defaul：可选，若字典中不存在key则返回default值。

2. del demo_dict[key]：删除键key对应条目；

3. 扩展：
demo_dict.clear()：清空字典所有条目；  
del demo_dict：删除字典。

###37.按照字典的内的年龄排序
知识点：字典列表排序
```python
demo_dict = [
	{'name': 'Amily', 'age': 16},
	{'name': 'Renee', 'age': 23},
	{'name': 'Vivian', 'age': 18},
]

# 1. 按age升序排列
demo_dict.sort(key=lambda item: item['age'])
# 等价于：
sorted(demo_dict, key=lambda item: item['age'])

# 2. 按age降序排列[reverse默认为False，即升序]
demo_dict.sort(key=lambda item: item['age'], reverse=True)

# 3. 先按age，再按name排序
demo_dict.sort(key=lambda item: (item['age'], item['name']))

```

扩展：字典排序【字典没有sort方法，只能用sorted】
```python
demo_dict ={'2':'3', '1':'2', '3':'0'}

# 1. 按键排序，返回键的有序列表:：
keys = sorted(demo_dict)
# keys: ['1', '2', '3']

# 2. 按键排序，返回排序后的字典list：
result = sorted(demo_dict.items())
result = sorted(demo_dict.items(), key = lambda item: (item[0], item[1]))
# result: [('1', '2'), ('2', '3'), ('3', '0')]

# 3. 按值排序，返回排序后的字典list：
result = sorted(demo_dict.items(), key = lambda item: (item[1], item[0]))
# result: [('3', '0'), ('1', '2'), ('2', '3')]
```

###38.请合并下面两个字典 a = {"A":1,"B":2},b = {"C":3,"D":4}
字典a更新为两字典合并后的结果：
```python
a.update(b)
```

###39.如何使用生成式的方式生成一个字典，写一段功能代码。
字典生成式：```d = {key: value for (key, value) in iterable}```
```python
# 例1：
lis = [('name','zhangsan'),('age','11'),('phone','a')]
dic = {k:v for k,v in lis}
# dic: {'phone': 'a', 'name': 'zhangsan', 'age': '11'}

# 例2：
lis = ['1', '2', '3']
dic = {k:'defult_value' for k in lis}
# dic: {'1': 'defult_value', '2': 'defult_value', '3': 'defult_value'}
```

###40.如何把元组("a","b")和元组(1,2)，变为字典{"a":1,"b":2}
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。
如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。
py3中zip()返回一个迭代器，需要手动转换成dict。
```python
keys = ('a', 'b')
values = (1, 2)
zipped = zip(keys, values)
# dict(zipped): {'a': 1, 'b': 2}
# list(zipped): [('a', 1), ('b', 2)]

# 解压缩：
unzipped = list(zip(*zipped))
# unzipped: [('a', 'b'), (1, 2)]
```
