# Python列表

### 30.已知 AList = [1,2,3,1,2],对 AList 列表元素去重，写出具体过程。
1. 转换成set再转回list。
```python
AList = list(set(AList))
```

2. 使用pandas的unique函数，函数返回array需要转换回list。
```python
import pandas as pd
AList = pd.unique(AList).tolist()
```

3. 使用dict.formkeys(seq[, value]))：函数创建一个新的字典，seq参数是键列表，value参数是对应的值（默认为None）。
```python
AList = list(dict.formkeys(AList))
```

4. 循环判断
```python
AList = [1,2,3,1,2]
result = []
for x in AList:
	if x in result:
		continue
	else:
		result.append(x)
```

### 31.如何实现 "1,2,3" 变成 ["1","2","3"]
```python
string = "1,2,3"
result = string.split(',')
```

### 32.给定两个 list，A 和 B，找出相同元素和不同元素
1. 直接操作list：
```python
same_items = [x for x in A if x in B]
diff_items = [x for x in A if x not in B] + [x for x in B if x not in A]
```
2. 使用set操作：
```python
same_items = list(set(A) & set(B))
diff_items = list(set(A) ^ set(B))
```

### 33.[[1,2],[3,4],[5,6]]一行代码展开该列表，得出[1,2,3,4,5,6]
```python
# 1. 列表推导式
result = [item for inner_list in outer_list for item in inner_list]

# 2. 循环嵌套展开
result = []
for inner_list in outer_list:
	for item  in inner_list:
		result.append(item)

# 3. 用sum对列表求和
result = sum(outer_list, [])
```


### 34.合并列表[1,5,7,9]和[2,2,6,8]
```python
# 1. 使用'+'
result = list1 + list2

# 2. 使用extend
list1.extend(list2)

# 3. 使用append
for x in list2:
	list1.append(x)
```

### 35.如何打乱一个列表的元素？
```python
import random
random.shuffle(a_list)
```


