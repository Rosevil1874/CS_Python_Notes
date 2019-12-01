# Python常见数据结构内置方法时间复杂度

>原文: [wiki.python](https://wiki.python.org/moin/TimeComplexity) 

>本文记录了当前版本CPython的各种操作时间复杂度（也即“Big O”），其他Python版本（旧版本或者正在开发的CPython版本）在性能上可能有些许差异，但一般不会超过O(log n)。  
本文中，'n'代表当前容器中的元素数量，'k'代表一个参数的值或此参数中元素的数量。

## 列表 - list
假设平均情况下列表元素是随机的。
list是用Array实现的，最大的开销来自超过当前已经分配大小的增长（因为所有的元素都需要移动），或者需要在接近头部的位置进行插入删除操作时（因为其后的所有元素均需要移动）。需要在列表两端进行添加或删除操作时，最好使用collections.deque。

操作		 | 平均情况  |   均摊最坏情况	
-------- | -------- |  -----------
Copy | O(n) | O(n)
Append[注1] | O(1) | O(1)
Pop last | O(1) | O(1)
Pop intermediate | O(k) | O(k)
Insert | O(n) | O(n)
Get Item | O(1) | O(1)
Set Item | O(1) | O(1)
Delete Item | O(n) | O(n)
Iteration | O(n) | O(n)
Get Slice | O(k) | O(k)
Del Slice | O(n) | O(n)
Set Slice | O(k+n) | O(k+n)
Extend[1] | O(k) | O(k)
Sort | O(n log n) | O(n log n)
Multiply | O(nk) | O(nk)
x in s | O(n) | --
min(s), max(s) | O(n) | --
Get Length | O(1) | O(1)

* 插入和删除操作均需要移动其后所有元素，因此平均情况下为O(n)
* 列表的sort方法使用Timesort算法，混合归并排序和插入排序。
* 列表乘法中，n和k分别代表两个列表长度


## 双向队列 - collections.deque
dequeue数据结构使用双向链表实现(Well, a list of arrays rather than objects, for greater efficiency.) 。双向队列两端可达，但是对中间元素的的查找、添加、删除都会比较慢。

操作		 | 平均情况  |   均摊最坏情况	
-------- | -------- |  -----------
Copy | O(n) | O(n)
append | O(1) | O(1)
appendleft | O(1) | O(1)
pop | O(1) | O(1)
popleft | O(1) | O(1)
extend | O(k) | O(k)
extendleft | O(k) | O(k)
rotate | O(k) | O(k)
remove | O(n) | O(n)


## 集合 - set
未列出的操作时间复杂度可以参考dict，两者实现方式非常类似。

操作		 | 平均情况  |   均摊最坏情况	
-------- | -------- |  -----------
x in s | O(1) | O(n)
Union s\|t | O(len(s)+len(t)) | --
Intersection s&t | O(min(len(s), len(t)) | O(len(s) * len(t))
Multiple intersection s1&s2&..&sn | -- |(n-1)*O(l) where l is max(len(s1),..,len(sn))
Difference s-t | O(len(s))
s.difference_update(t) | O(len(t))
Symmetric Difference s^t | O(len(s)) | O(len(s) * len(t))
s.symmetric_difference_update(t) | O(len(t)) | O(len(t) * len(s))

* 求交集（Intersection s&t）操作需要s和t均为集合，但事实上只要t是可迭代的就能使用此方法，此时平均时间复杂度为O(min(len(s), len(t))
* Difference s-t（即s.difference(t)） ： 获取s中与t不同的部分；s.difference_update(t)：s = s - t。 前者时间复杂度为O(len(s))是因为s中所有不在t中的元素会被加入到新集合，后者时间复杂度为O(len(t))是因为所有出现在t中的元素会从s中删除，决定使用哪一个方法的时候注意哪个集合更长以及是否需要新集合。
* Symmetric Difference: s和t的并集减去两者的差集


## 字典 - dict
字典操作的平均时间复杂度假设哈希函数足够鲁棒使得几乎不出现冲突，同时假设参数中使用的key是从key集合中随机选择的。    
note：使用字符串作为字典的键可以提高运行速度，虽然不会改变时间复杂度，但是会对时间复杂度的常数项产生显著影响。


操作		 | 平均情况  |   均摊最坏情况	
-------- | -------- |  -----------
Copy[注2] | O(n) | O(n)
Get Item | O(1) | O(n)
Set Item[注1] | O(1) | O(n)
Delete Item | O(1) | O(n)
Iteration[注2] | O(n) | O(n)


> 注：
1. 这些操作的时间复杂度依赖于“均摊最坏情况”中的“均摊”情况。根据容器的历史，单个操作可能会花费大量时间。
2. 对于这些操作，最坏情况下的n是容器曾经达到的最大大小，而不是当前的大小。例如，如果将N个对象添加到字典中，然后删除N-1个对象，那么在下一次插入操作之前字典的大小均为按N。