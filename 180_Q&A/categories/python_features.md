# Python语言特性

### 	1. Python与其他语言的区别
	• 语法简洁优美：省略了大括号、分号，以及一些关键字、类型说明；
	• 是一门动态、可移植、可扩展、可嵌入的解释型编程语言；
	• 动态类型语言：变量不用事先声明类型，并且后期可以修改修改数据类型；
	• 强类型语言：很少进行隐式的变量类型转换；
	• 面向对象：```class```是类，```__init__()```是类的构造函数，函数是类的方法，```self```是类的实例代表当前对象的而地址。对象是通多类定义的数据结构实例，包含类变量和实例变量两种数据成员和类定义的方法。
	• 具有强大完备的第三方库，功能强大；
	• 应用广泛：web运维、自动化测试、爬虫、数据分析、人工智能等。
	
### 	2. 解释型和编译型语言
	○ 解释型语言（边解释边执行）：使用解释器将代码逐行解释成机器码并立即执行，相当于把编译和解释混合到一起完成；跨平台容易，只需提供特定平台的解释器；但运行效率低。相当于每次执行都进行一次编译。
	○ 编译型语言（编译后执行）：集中转换，进行整体的编译和链接处理再运行。
	
### 	3. python的解释器种类及相关特点
	CPython：官方解释器，使用C语言开发；
	IPython：基于CPython的交互式解释器，在其基础上交互式有所增强；
	PyPy：采用JIT技术对python进行动态编译，可以显著提升速度，结果可能与CPython结果有所不同；
	Jython：运行在Java平台的Python解释器，可以将Python代码直接编译成Java字节码执行；
	IronPython：运行在微软.Net平台，可以直接把python代码编译成.Net的字节码。

### 	4. python3与python2之间的区别
		a. 编码：
			i. python2字符类型：str:编码后的字节序列，Unicode：编码前的文本字符；
			ii. python3字符类型：str:编码后的Unicode文本字符，bytes：编码钱的字节序列。
			python2中两种状态都有encode和decode方法，python3优化后str只有encode方法转化为字节码，bytes只有decode方法转化为文本字符串。
			python2中需要在文件头上加注释 # coding: utf-8 指定编码格式。
		b. print
		python2中print是class，python3中print是函数。
		
		c. input
		python2中input解析输入为int型，raw_input解析输入为str型；python3中input解析输入为str型。
		
		d. 算术符
		python2中/对于整数除法会将结果省去小数部分，对于浮点数会保留小数部分（真除），python3中/一律保留小数部分。
		
		e. xrange
		python2中使用xrange()创建迭代器对象，使用range()创建一个list；python3中移除了xrange()方法，使用range()创建一个迭代器对象。
		
### 	5. python3和python2中int和long的区别
	python2中有为非浮点数准备的int和long类型，int类型的最大值不超过sys.maxint，且这个值与平台相关。
	python3中只有int类型没有long类型，大多数情况下这里的int很像python2中的long。
	
### 	6. xrange和range的区别
python2中使用xrange()创建迭代器对象，使用range()创建一个list；python3中移除了xrange()方法，使用range()创建一个迭代器对象。