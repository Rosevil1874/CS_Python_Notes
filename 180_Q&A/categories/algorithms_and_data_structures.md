# Python 其他内容

### 122.已知：
### (1) 从 AList 和 BSet 中 查找 4，最坏时间复杂度哪个大？
### (2) 从 AList 和 BSet 中 插入 4，最坏时间复杂度哪个大？
1. 查找：list由数组实现，get在平均和最坏情况下均为O(1)；set(dict)由hash实现，get/in平均O(1)最坏O(n)。
2. 插入：list插入时需要移动元素，且时间复杂度随元素增多而变大，平均和最坏均为O(n)；set的插入和元素个数无关，平均O(1)，最坏O(n)。


### 123.用 Python 实现一个二分查找的函数
二分查找元素在列表中的索引，若元素不在列表中则返回其应该插入的索引。
```python
def bin_serach(nums, target):
	'''二分查找

	利用二分查找查找元素索引，若不存在则返回其应该插入的索引
	:param nums:目标列表
	:param target: 带查找数值
	:return: 元素索引/插入索引
	'''
	# corner case
	if not nums:
		return -1

	l, r = 0, len(nums)
	while l <= r:
		mid = (l + r) // 2
		if target < nums[mid]:
			r = mid - 1
		elif target > nums[mid]:
			l = mid + 1
		else:
			return mid
	return l


# # case0: -1
# # nums = []
# nums = None
# target = 4

# # case1: 2
# nums = [1, 3, 4, 6, 9]
# target = 4

# # case2: 3
# nums = [1, 3, 4, 6, 9]
# target = 5

# case3: 0
nums = [1, 3, 4, 6, 9]
target = 0

res = bin_serach(nums, target)
print(res)
```


### 124.python 单例模式的实现方法
1. 装饰器实现
```python
def singleton(cls):
	_instance = {}

	def inner(*args, **kwargs):
		# 若全局都没有cls的实例则创建一个，否则返回这个实例
		if cls not in _instance:
			_instance[cls] = cls(*args, **kwargs)
		return _instance[cls]
	return inner

@singleton
class Demo:
	def __init__(self, val):
		self.val = val


if __name__ == '__main__':
	
	demo1 = Demo(1)
	print('demo1.val: ', demo1.val)		# demo1.val: 1

	demo2 = Demo(2)
	print('demo2.val: ', demo2.val)		# demo2.val: 1

	print(demo1 is demo2)				# True
```

2. `__new__`实现
```python
class Singleton(object):
	_instance = None

	def __new__(cls, *args, **kwargs):
		# 若全局都没有cls的实例则创建一个，否则返回这个实例
		if cls._instance is None:
			cls._instance = super().__new__(cls, *args, **kwargs)
		return cls._instance



if __name__ == '__main__':
	
	demo1 = Singleton()
	demo2 = Singleton()

	print(demo1 is demo2)		# True
```


### 125.使用 Python 实现一个斐波那契数列
实现一个斐波那契生成器：
```python
def fib(n):
	if n == 0:
		yield 0

	prev2, prev1 = 0, 1
	for _ in range(n):
		prev2, prev1 = prev1, prev1 + prev2
		yield prev2


fib_iter = fib(0)		# generator
for i in fib_iter:
	print(i)
```


### 126.找出列表中的重复数字
```python
def find_duplication(nums):
	'''找出数组中的重复数字

	找出数组中的重复数字
	:param nums:目标数组
	:return: 重复数字列表，没有重复数字则返回[]
	'''
	if not nums:
		return []

	res = set()
	showed = set()
	for num in nums:
		if num in showed:
			res.add(num)
		else:
			showed.add(num)
	return list(res)


# # case0: []
# # nums = []
# nums = None

# # case1: 
# nums = [1, 2, 3]

# # case2:
# nums = [1, 1, 2, 3]

# case3:
nums = [1, 1, 2, 3, 3]

res = find_duplication(nums)
print(res)
```

使用collections.Counter():
```python
if not nums:
	return []

cnt = dict(Counter(nums))
return [item[0] for item in cnt.items() if item[1] > 1]
```


### 127.找出列表中的单个数字
```python
cnt = dict(Counter(nums))
return [item[0] for item in cnt.items() if item[1] == 1]
```


### 128.写一个冒泡排序
```python
def buble_sort(nums):
	'''冒泡排序

	使用冒泡排序升序排列列表，依次将未排序列表的最大值冒泡的最后
	:param nums:目标数组
	:return: 排序后的列表
	'''
	if not nums:
		return []

	n = len(nums)
	for i in range(n):
		for j in range(n - i - 1):
			if nums[j] > nums[j + 1]:
				nums[j],  nums[j + 1] = nums[j + 1], nums[j]
	return nums


# # case0: []
# # nums = []
# nums = None

# case1: 
nums = [1, 4, 2, 3]

# # case2:
# nums = [1, 3, 1, 2, 3]


res = buble_sort(nums)
print(res)
```


### 129.写一个快速排序
辅助空间 + 递归: 平均时间复杂度O(nlogn)，平均空间复杂度O(nlogn)：
```python
def quick_sort(nums):
	'''快速排序

	在序列中找出一个轴值，一轮排序后将小于轴值的数放到其左边，大于轴值的数放到其右边。
	然后在左右子序列中递归此项操作，直到子序列的元素个数小于等于1.
	:param nums:目标数组
	:return: 排序后的列表
	'''
	n = len(nums)
	if n <= 1:
		return nums

	pivot = nums[n // 2]
	nums.remove(pivot)

	left, right = [], []
	for num in nums:
		if num <= pivot:
			left.append(num)
		else:
			right.append(num)
	return quick_sort(left) + [pivot] + quick_sort(right)
```

就地递归：平均时间复杂度O(nlogn)，平均空间复杂度O(logn)：
```python
def quick_sort(nums):
	'''快速排序

	在序列中找出一个轴值，一轮排序后将小于轴值的数放到其左边，大于轴值的数放到其右边。
	然后在左右子序列中递归此项操作，知道子序列的元素个数小于等于1.
	:param nums:目标数组
	:return: 排序后的列表
	'''
	n = len(nums)
	quick_sort_recursive(nums, 0, n - 1)


def quick_sort_recursive(nums, l, r):
	if l >= r:
		return
	index = partition(nums, l, r)
	quick_sort_recursive(nums, l, index - 1)
	quick_sort_recursive(nums, index + 1, r)


def partition(nums, l, r):
	pivot = nums[r]
	i = l - 1
	for j in range(l, r):
		if nums[j] <= pivot:
			i += 1
			nums[i], nums[j] = nums[j], nums[i]
	nums[i + 1], nums[r] = nums[r], nums[i +1]
	return i + 1
```


迭代【栈】：平均时间复杂度O(nlogn)，平均空间复杂度O(logn)：
```python
def quick_sort(nums):
	'''快速排序

	在序列中找出一个轴值，一轮排序后将小于轴值的数放到其左边，大于轴值的数放到其右边。
	然后在左右子序列中递归此项操作，知道子序列的元素个数小于等于1.
	:param nums:目标数组
	:return: 排序后的列表
	'''
	n = len(nums)
	quick_sort_recursive(nums, 0, n - 1)


def quick_sort_recursive(nums, l, r):
	if l >= r:
		return
	stack = []
	stack.append(l)
	stack.append(r)

	while stack:
		r = stack.pop()
		l = stack.pop()

		if l >= r:
			continue

		pivot = nums[r]
		i = l - 1
		for j in range(l, r):
			if nums[j] <= pivot:
				i += 1
				nums[i], nums[j] = nums[j], nums[i]
		nums[i + 1], nums[r] = nums[r], nums[i + 1]
		stack.extend([l, i, i + 2, r])
```



### 130.写一个拓扑排序
拓扑排序一般用来解决有执行顺序约束的调度问题。例子参见leetcode207。



### 131.python 实现一个二进制计算。
计算机内存储二进制补码。


### 132.有一组“+”和“-”符号，要求将“+”排到左边，“-”排到右边，写出具体的实现方法。
```python
def char_sort(s: str) -> str:
	if len(s) <= 1:
		return s
	return ''.join(s.split('+') + s.split('-'))
```


### 133.单链表反转
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        new_head, temp = None, None
        curr = head
        while curr:
            temp = curr.next
            curr.next = new_head
            new_head = curr
            curr = temp
        return new_head


head = ListNode(0)
head.next = ListNode(1)
head.next.next = ListNode(2)
head.next.next.next = ListNode(3)

new_head = reverse_linked_list(head)
while new_head:
	print(new_head.val)
	new_head = new_head.next
```


### 134.交叉链表求交点
拼接链表，顺序遍历：
```python
class ListNode:
	def __init__(self, val):
		self.val = val
		self.next = None


def find_intersect(head1: ListNode, head2: ListNode) -> ListNode:
	p1, p2 = head1, head2
	while p1 and p2:
		if p1 == p2:
			return p1
		p1 = p1.next if p1.next else head2
		p2 = p2.next if p2.next else head1
	return None		# 没有交点


head = ListNode(0)
head.next = ListNode(1)
head.next.next = ListNode(2)		# 交点
head.next.next.next = ListNode(3)
joint = head.next.next
head2 = ListNode(9)
head2.next = joint

intersect = find_intersect(head, head2)
print(intersect.val if intersect)
```


### 135.用队列实现栈
使用队列实现栈的下列操作：

	push(x) – 元素 x 入栈
	pop() – 移除栈顶元素
	top() – 获取栈顶元素
	empty() – 返回栈是否为空

参考leetcode 225.


### 136.找出数据流的中位数
大小堆，参考leetcode 295.


### 137.二叉搜索树中第 K 小的元素
中序遍历，参考leetcode 230.
