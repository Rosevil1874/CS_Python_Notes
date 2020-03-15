# Python高级特性

### 70.函数装饰器有什么作用？请列举说明？
函数装饰器是用来修改其他函数功能的函数，主要是在不修改原始代码的情况下对函数进行功能扩展，满足面向对象的“开闭原则”。  

应用场景：

	引入日志
	程序运行时间统计
	函数执行前准备工作
	函数执行后清理工作
	权限校验
	缓存
	事务处理


### 71.Python 垃圾回收机制？
**1. 整数**
* 小整数：python将[-5,257]间的整数视为小整数，在一个python程序中，所有这个范围内的整数使用同一个对象。小整数对象是提前建立好的，因此不会被回收（单个字母同理）。
* 大整数：每一个大整数的创建都会在内存中新分配内存空间，使用结束后会被回收。
**2. 机制：引用计数为主，标记清除和分代回收为辅。**
* **引用计数：** 每个对象有一个结构体PyObject，其中的oj_refcnt为对象的引用计数。当对象新增引用时oj_refcnt加一，反之减一。当oj_refcnt为0时立即将其回收。优点是简单和实时性，缺点是维护oj_refcnt耗费资源，并且可能造成循环引用。
* **标记清除：**基于追踪回收，第一阶段将所有的活动对象打上标记，第二阶段将非活动对象进行回收。标记清除作为引用计数的辅助方式进行容器对象（list， tuple，dict等）的回收，因为字符串和数值不会出现循环引用。
* **分代回收：**空间换时间，将内存根据不同的对象存活时间划分集合，每个集合称为一代。年轻代（第0代），中年代（第1待），老年代（第2代）分别对应一个链表，三个代的垃圾回收频率随存活时间增大而减小。同样也是辅助回收容器对象。


### 72.魔法函数 `__call__`怎么使用?
`__call__`允许一个实例对象像函数一样被调用。

```python
class Entity:
	def __init__(self, a, b):
		self.a = a
		self.b = b

	def __call__(self, a, b):
		self.a = a
		self.b = b

	def get(self):
		print(self.a, self.b)


if __name__ == '__main__':
	demo = Entity(1, 2)
	demo(3, 4)
	demo.get()

```
输出`3 4`。


### 73.如何判断一个对象是函数还是方法？
定义：在类外使用def定义的为函数。在类内的，使用类调用为函数，使用实例化对象调用的为方法。  
可以使用isinstance()进行判断。
```python
from types import FunctionType
from types import MethodType

class DemoClass():
	def __init__(self):
		pass

	def run(self):
		pass

def demo_func():
	pass

if __name__ == '__main__':
	demo_obj = DemoClass()
	print(isinstance(demo_func, FunctionType))
	print(isinstance(DemoClass.run, FunctionType))
	print(isinstance(demo_obj.run, MethodType))
```
输出：
```python
True
True
True
```


### 74.@classmethod 和@staticmethod 用法和区别
@classmethod 和@staticmethod都是装饰器，装饰的成员函数可以不实例化用`类名.方法名()`进行调用。  
用途：
* @classmethod： 多用于工厂模式，在实例化对象之前进行某些逻辑操作；
* @staticmethod： 可以看作该类的一个工具、辅助函数。
区别：
* @classmethod 需要传递参数`cls`，因此可以访问和修改类的属性、方法和实例化对象等，避免硬编码。@classmethod可以判断自己是通过基类还是子类调用。
* @staticmethod 不需要`self`或`cls`参数，和一般函数的使用方法一样。


### 75.Python 中的接口如何实现？
* 接口：只定义了一些功能，而没有去实现，需要被一个类继承之后去实现其中的一个或多个功能。  
* python中的接口：由抽象类和抽象方法实现的，接口不能实例化，只能由继承类去实现功能。


### 76.Python 中的反射了解么?
* 反射：在运行的时候自我检查，并对内部成员进行操作。变量的类型可以动态改变，到使用的时候再确定其作用；
* python中的反射：可以通过一个对象找出其type、class、attribute和method的能力成为反射能力。具有反射能力的有type()、isinstance()、callable()、getattri()等函数。


### 77.metaclass 作用？以及应用场景？
metaclass创建类，可以认为类是metaclass创建出的实例，可以动态修改类。  
场景：将数据库的表映射为类的时候，每个类都要根据表动态定义。


### 78.hasattr() getattr() setattr()的用法
* hasattr(Object, name)：判断对象是否有name属性；
* getattr(Object, name[, defaul])：返回对象的name属性值，若没有属性则返回默认值；
* setattr(Object, name, value)：更改对象的name属性为value，若不存在则创建属性。


### 79.请列举你知道的 Python 的魔法方法及用途。
魔法方法：也就是前后加下划线的方法，这些方法在python中已经定好，在进行某些操作时会被自动调用。  
**最常用的：`__new__，__init__，__del__`**
* `__new__`：创建类并返回这个类的实例；
* `__init__`：使用传入的参数初始化实例，与`__new__`一同构成了构造函数；
* `__del__`：删除实例化的对象，即为析构函数。  
**类操作：**  
* `__class__`：获得已知对象的类，`obj.__class__`；
* `__call__`：可以让实例对象像函数一样被调用；
**属性访问**：
* `__getattr__`：获取属性值；
* `__setattr__`：设置属性值；
* `__delattr__`：删除属性；
**上下文管理器**：
* `__enter__`：进入上下文（with后面的语句出发）；
* `__exit__`：退出当前执行上下文（结束with语句时）；
**迭代器方法**：
`__iter__`：返回一个迭代器；
`__next__`：返回迭代器的下一个元素。


### 80.如何知道一个 Python 对象的类型？
使用type()判断对象类型。


### 81.Python 的传参是传值还是传址？
* 参数为可变类型时为传址，如list、dict；
* 参数为不可变类型时为传值，如int、string、tuple。


### 82.Python 中的元类(metaclass)使用举例
与77题重复了。


### 83.简述 any()和 all()方法
* any()：判断给定的可迭代参数是否有至少一个不为**空、0、False**，是则返回ture;
* all()：判断给定的可迭代参数是否全为**空、0、False**，是则返回ture;


### 84.filter 方法求出列表所有奇数并构造新列表，a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
`b = list(filter(lambda x: x % 2 == 1, a))`


### 85.什么是猴子补丁？
在动态语言中，不改变源码对功能进行追加或修改。


### 86.在 Python 中是如何管理内存的？
**python内存池**：内存池就是预先在内存中申请一定数量的，大小相等的内存块留作备用。当有内存需求时先从内存池中分配，不够了再去申请新的内存。这样可以减少内存碎片，提升效率。  

**python中的内存管理机制--Pymalloc**：在对象小于256bit的时候直接从内存池分配，否则执行new/malloc申请空间。


### 87.当退出 Python 时是否释放所有内存分配？
循环引用其他对象，或引用自全局命名空间的模块，在python退出时并未完全释放。  
解决：循环垃圾回收器可以回收循环引用的对象，使用global()获取全局对象并手动删除。