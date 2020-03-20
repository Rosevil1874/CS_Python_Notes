# 20 - 包含min函数的栈

## 题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。


## 题解
使用一个辅助栈存储最小值。
```python
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.stack = []     # 栈
        self.minStack = []  # 存储最小值的栈
 
    def push(self, node):
        # 每次push操作时同时要将当前栈内元素相应的最小值压入辅助栈顶。
        if not self.minStack:
            self.minStack.append(node)
        else:
            self.minStack.append( min(self.minStack[-1], node) )
        self.stack.append(node)
 
 
    def pop(self):
        # 每次pop操作时需要将辅助栈顶也弹出，因为弹出后最小值可能发生改变
        if not self.stack:
            return None
        self.minStack.pop()
        return self.stack.pop()
 
    def top(self):
        # 直接返回栈顶
        if not self.stack:
            return None
        return self.stack[-1]
 
    def min(self):
        # 直接返回辅助栈顶
        if not self.minStack:
            return None
        return self.minStack[-1]
```