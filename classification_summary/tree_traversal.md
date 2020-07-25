# 树的遍历

树的遍历方法一共有四种：
- 先序遍历：根-左-右
- 中序遍历：左-根-右
- 后序遍历：左-右-根
- 层次遍历：每一层依次遍历


## 递归
### 先序遍历
```python
res = []
def preorderTraversal(root):
	if not root:
		return

	res.append(root.val)
	preorderTraversal(root.left)
	preorderTraversal(root.right)
```

### 中序遍历
```python
res = []
def inorderTraversal(root):
	if not root:
		return
		
	preorderTraversal(root.left)
	res.append(root.val)
	preorderTraversal(root.right)
```

### 后序遍历
```python
res = []
def postorderTraversal(root):
	if not root:
		return
		
	preorderTraversal(root.left)
	preorderTraversal(root.right)
	res.append(root.val)
```


## 迭代
### 先序遍历
压栈时先右后左，出栈时才符合先左后右。
```python
def preorderTraversal(root):
	if not root:
		return

	res = []
	stack = [root]
	while stack:
		curr = stack.pop()
		res.append(curr.val)
		if curr.right:
			stack.append(curr.right)
		if curr.left:
			stack.append(curr.left)

	return res
```

### 中序遍历
```python
def inorderTraversal(root):
	if not root:
		return

	res = []
	stack = []
	curr = root
	while curr or stack:
		while curr:
			stack.append(curr)
			curr = curr.left
		curr = stack.pop()
		res.append(curr.val)
		curr = curr.right
	return res
```
### 后序遍历
前序遍历和后序遍历之间的关系：
- 前序遍历顺序为：根 -> 左 -> 右
- 后序遍历顺序为：左 -> 右 -> 根

我们将前序遍历中节点插入结果链表尾部的逻辑，修改为将节点插入结果链表的头部  
那么结果链表就变为了：右 -> 左 -> 根

接下来如果我们将遍历的顺序由从左到右修改为从右到左，
那么结果链表就变为了：左 -> 右 -> 根

这刚好是后序遍历的顺序

```python
def postorderTraversal(root):
	if not root:
		return

	res = []
	stack = [root]
	while stack:
		curr = stack.pop()
		res.insert(0, curr.val)
		if curr.left:
			stack.append(curr.left)
		if curr.right:
			stack.append(curr.right)

	return res
```


## 层次遍历
```python
def levelTraversal(root):
	if not root:
		return

	res = []
	curr_level = [root]
	while curr_level:
		curr_vals = []
		next_level = []
		for node in curr_level:
			curr_vals.append(node.val)
			if node.left:
				next_level.append(node.left)
			if node.right:
				next_level.append(node.right)
		curr_level = next_level
		res.append(curr_vals)

	return res
```