# 1. 面向对象编程的特点

继承、封装、多态、抽象

1. 封装（Encapsulation）
   - 封装是指将数据（属性）和方法（行为）组合在一个类（Class）中，并对外部隐藏实现细节。封装有助于隐藏对象内部的状态，从而保护数据免受外部修改的影响，并提供了一种通过方法来访问和操作数据的方式。封装增强了代码的可维护性和安全性。
2. 继承（Inheritance）
   - 继承允许创建一个新的类（称为子类或派生类），该类继承了现有类（称为父类或基类）的所有属性和方法。这意味着子类可以重用父类的代码，并可以在必要时覆盖或扩展父类的行为。继承提高了代码的复用性和模块化程度。
3. 多态（Polymorphism）
   - 多态是指允许使用一个接口来表示多种类型的对象的能力。在面向对象编程中，多态意味着同一个方法可以应用于不同的对象，并产生不同的效果。多态可以通过方法重载（Overloading）和方法覆盖（Overriding）来实现。多态提高了程序的灵活性和扩展性。
4. 抽象（Abstraction）
   - 抽象是指通过定义抽象类（Abstract Class）或接口（Interface）来展示对象的本质特征，同时隐藏不必要的细节。抽象类不能实例化，但它可以包含抽象方法，这些方法在派生类中必须被实现。接口定义了对象的行为规范，而不关心其内部实现。抽象帮助简化了复杂系统的设计，并使得设计更加模块化。

# 2.python的装饰器

装饰器本质上是接收一个函数作为参数的函数，返回一个新的函数。可以拓展函数的功能，不需要额外添加代码。

pytest中最常用的装饰器有8个

@pytest.fixture()、@pytest.mark、@pytest.mark.usefixtures()、@pytest.mark.parametrize()、@pytest.mark.skip()、@pytest.skipif()、@pytest.mark.xfail、@pytest.mark.run()

![image.png](https://secure2.wostatic.cn/static/qneTudQ2iArK8PQpDgB1as/image 2.png?auth_key=1726191767-pRGzS2E9tqA7dM4xxH5DPW-0-4c9251dcfb5893350db6a53a824d1c34)

```python
#fixture(scope,autouse,params,ids,name)：
    scope :在什么层级下运行 ，它的值只有 ：session ,package ,module ,class ,function(默认值)
    autouse : 代表的是否自动执行 ，若此参数不加或者设置为False的话，代表不会自动运行 ，设置为True自动执行，无需调用
    params : 进行的数据参数化 ，参数化的数据就是通过此参数传入到测试用例中。
    ids : 它是给生成的结果的fixture进行重命名 ，主要是为了好理解 ，前提是必须要有参数params 
    name : 对fixture的函数名起别名， 或者叫重命名 ,没啥大用处 。
    
    
#fixture可以帮助我们初始化、测试用例参数化以及完成测试后的清理工作
#相当于unitest中的：setUp();参数化测试用例：test_case()；tearDown() 用于测试后的清理工作
```

# 3.is和==的区别

都是用来比较两个对象的

== 是指用来比较两个对象的值是否相等；如果两个对象包含相同的数据，就会返回True；

is 用来比较两个对象的内存地址是否相同，只有它们是同一个对象的时候才会返回True；

```python
a = [1,2,3]
b = [1,2,3]
print(a==b) #输出True
print(a is b)#输出False

x = 5
y = x
print(x is y)#输出True，因为x,y指向同一个对象
```

对于简单类型（如整数、字符串等），当它们的值相同时，可能会复用内存中的同一份数据，

```python
a = 5
b = 5
print(a is b)  # 输出 True，因为小整数可能被缓存并复用

a = 1000000
b = 1000000
print(a is b)  # 输出 False，大整数可能不会被缓存
```

# 3.数组和链表

主要区别在于数据存储方式和访问方式。

数组的插入和删除需要耗费时间，因为需要移动其它元素的位置；适合随机访问元素；适合堆栈队列

链表的插入和删除比较快，只需要修改指针的指向；适合频繁插入和删除元素；适合哈希表和图等数据结构。

# 4.Python异常处理

异常是一个python对象，表示一个错误。

在无法处理正常程序时会发生一个异常。

# 5.python语言慢的原因

动态类型语言，边解释边执行；

GIL无法利用多核CPU并发执行。

# 6.python如何实现多线程？

Python是多线程语言，其内置有多线程工具包。多线程能让我们一次执行多个线程。Python中的GIL（全局解释器锁）确保一次执行单个线程。

一个线程保存GIL并在将其传递给下个线程之前执行一些操作，看上去像并行运行的错觉。事实上是线程在CPU上轮流运行。所有的传递会增加程序执行的内存压力。

# 7.迭代器和生成器

迭代器（Iterator）和生成器（Generator）都是python中用于迭代操作的工具

1.定义方式：迭代器实现了迭代器协议（即 __iter__()和__next__()方法）的对象。

​			生成器使用了yield关键字的函数，当这个函数被调用时，返回一个生成器对象

2.状态保存：生成器在每次产生一个值后会自动保存当前的状态，下次调用时会从上次离开的地方继续执行。

​			迭代器不会自动保存状态，依赖于用户显示地请求下一个值。

3.内存使用：生成器在迭代过程中只会生成当前需要的值，不是一次性生成所有值；可处理大数据集，不会耗尽内存。

​			迭代器可能需要一次性生成所有值。

4.重复使用：迭代器可以被多次迭代，每次迭代都会从头开始。

​			生成器只能被迭代一次，不保存整个序列，只保存当前状态。

5.灵活性：生成器更灵活，可以使用任何类型的控制流语句（如if，while等）。

​			迭代器需要在__next__()方法中实现所有的控制逻辑。

```python
#python 迭代器
class MyInterator:
	def __init__(self,max):
		self.max = max
		self.current = 0
		
  def __iter__(self):
  	return self
  	
  def __next__(self):
  	if self.current >= self.max:
  		raise StopIteration
    else:
    	result = self.current
    	self.current += 1
    	return result
    	
my_iter = MyInterator(5)
for i in my_iter:
	print(i)

#这段代码定义了一个简单的迭代器类MyIterator，它会在每次调用__next__()时返回一个新的整数，直到达到最大值为止。
#结果依次输出0,1,2,3,4

```



```	python
#python 生成器
def my_generator(max):
	current = 0
	while current < max:
		yield current
		current += 1
		
for i in my_generator(5):
		print(i)
```



# 8.Python数据类型

## 数字：整数、浮点数、负数、布尔值

## 字符串：要用 ‘ ’ 或者 ” “ 括起来，特殊符号需要 反斜杠\ 转义

## 列表：可重复有序数据集合

## 元组：元素不会变的数组

### 1.列表和元组最大的区别是，列表是可变的，元组是不可变的。

```python
mylist = [1, 2, 3, 4]
mylist[1] = 5
print（mylist）
#可以修改，修改后为[5, 2, 3, 4]

mytuple = (1, 2, 2)
mytuple[1] = 3
#会报错TypeError: 'tuple' object does not support item assignment

```



### 2.元组解封装

```python 
mytuple1 = (1, 2, 2)
x, y, z = mytuple1
a = x + y + z
print(a)
#输出5
```





## 集合：可变无序且不可重复的元素序列

## 字典：是一系列的键值对，key唯一，value可以重复；

可变的无序对象；字典是python中的内置数据类型，它定义了键和值之间的一对一关系，包含了一对键及其对应的值，字典由键索引



# 9.进程、线程、协程

进程：系统进行资源分配和调度的一个独立单位

线程：进程的一个实体，是CPU调度和分派的基本单位，是比进程更小的独立运行的基本单位；线程间通信主要通过共享内存，上下文切换快，资源开销小，相比于进程不够稳定，易于丢失数据

协程：一种轻量级线程，可以在单个线程内运行；适用与IO密集型程序（大部分时间都在等待数据的读取或写入）

进程与线程比较

1.地址空间：线程是进程内的一个执行单元，进程内至少有一个线程；进程有自己独立的地址空间，线程共享进程的地址空间

2.资源拥有：进程是资源分配和拥有的单位，同一个进程内的线程共享进程的资源

3.线程是处理器调度的基本单位，进程不是

4.都可并发执行

5.线程不能独立执行，必须存在于应用程序中，由应用程序提供多个线程执行控制

协程与线程比较

1.一个线程可以有多个协程，一个进程也可以单独拥有多个协程

2.协程是异步的，线程和进程是同步的

3.协程能保留上一次调用时的状态





# 10.直接赋值、深拷贝和浅拷贝

直接赋值：就是对象的引用

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720931-7116-4AQC6.png)

浅拷贝（copy）：拷贝父对象，不会拷贝对象的内部子对象（子对象是引用关系，b=a.copy（），如果a的子对象发生了变化，则b的子对象也发生变化，因为是引用来的，实际上是同一个子对象）

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720930-6827-Vtk4m.png)

深拷贝（deepcopy）：copy模块的deepcopy方法，完全拷贝了父对象及其子对象（子对象不再是引用关系，b=a.deepcopy 如果a的子对象发生了变化，则b的子对象不变）

![img](https://www.runoob.com/wp-content/uploads/2017/03/1489720930-5882-BO4qO.png)

# 11.常用开发模式

#### 面向过程

- 强调程序的流程控制

- 数据和函数分离

- 简单直观，适合小规模项目

  ```python
  def greet(name):
      return f"Hello, {name}!"
  
  if __name__ == "__main__":
      name = "Alice"
      print(greet(name))
  ```

  

#### 面向对象（OOP）

- 封装：隐藏对象的实现细节，并对外提供一个干净的接口。在 Python 中，可以通过将属性设为私有（通过前缀`_`或`__`）来实现某种程度上的封装。

- 继承：子类可以继承父类的特性

- 多态：不同类的对象可以用相同的接口表示

  ```python
  #Person类，类中定义了数据name，定义个打招呼函数（方法、行为）；这个类可以做的事情是：接受一个name参数，返回一个打招呼；调用这个person类，可以用它打招呼
  
  class Person:
    #构造函数__init__,用于初始化对象的属性，当创建一个新的对象实例时会被调用
  	def __init__(self, name):
  		self.name = name
  		
    def greet(self):
    	return f"Hello,{self.name}"
    	
  if __name__ == "__main__":
  	person = Person("Alice")
  	print(person.greet())
  ```

  



#### 函数式编程

强调函数的重要性，将计算视为函数的求值。这种模式下，函数是第一等公民，可以作为参数传递给其他函数，也可以作为其他函数返回的结果。

```python
def square(x):
    return x * x


numbers = [1, 2, 3, 4]

squared_numbers = map(square, numbers)
print(list(squared_numbers))

#map（）函数的用法
# map(function, iterable, ...)
# function：要应用于每个项目的函数。这个函数应该接受与提供的可迭代对象数量相等的参数。
# iterable：一个或多个可迭代对象。可以是列表、元组、字符串等。
#map调用了square这个函数，传入number这个对象，得到结果
```



#### 元编程

元编程是指在运行时修改程序的行为的能力，或者在编译时生成代码的能力。Python 提供了许多元编程的工具，如装饰器、元类等。

特点：

- 动态类型：可以在运行时改变类型和行为

- 装饰器：可以修改函数的行为

- 元类：可以控制类的创造过程

  ```python
  def log(func):
      def wrapper(*args, **kwargs):
          print(f"Calling {func.__name__}")
          return func(*args, **kwargs)
      return wrapper
  
  #装饰器
  @log
  def add(a, b):
      return a + b
  
  if __name__ == "__main__":
      result = add(1, 2)
      print(result)  # 输出: 3
  ```

  

# 12.闭包、装饰器

##### python的闭包必须通过嵌套函数来实现，但是嵌套函数不一定就是闭包。

产生闭包的三个条件：

- 需要定义嵌套函数

- 嵌套函数需要引用enclosing function（封闭函数）中的变量

- enclosing function（封闭函数）需要返回嵌套函数

  ```python
  def make_printer(msg):
      def printer():
          print(msg)  # 使用括号来适应Python 3
      return printer
  
  printer = make_printer('Foo!')
  printer()#输出Foo！
  
  #闭包机制使得printer函数能能够记住并访问在其定义时，所在的外部函数make_printer的局部变量msg
  ```

  

##### 装饰器是处理函数的函数

python装饰器的功能，是把一个函数转换成另一个函数，

```python
#假如存在一个定义好的装饰器decorate
@decorate
def target():
	print('runing target()')
	

	
#等价于
def target():
	print('runing target()')
	
target = decorate(target) #在函数上方加@，就是@装饰器函数，把下面这个函数处理一下。
```





# 13.垃圾回收机制

#### 引用计数器为主，标记清除和分代回收为辅

python还有缓存机制，帮助部分性能提升

## 1.引用计数器

##### 1.环状双向链表refchain

![image-20240916161857110](/Users/shiyi/Library/Application Support/typora-user-images/image-20240916161857110.png)

python创建的任何对象都会放入refchain中

```python
#当创建对象时
name = “papapig”
age = 3
hobby = ['跳泥坑','画画']

```

```python
内部会创建一些数据【上一个对象、下一个对象、类型、引用个数（这是最基础的四个，每种类型的数据都有）】
name = “papapig”
new = name #这里name被引用了一次

内部会创建一些数据【上一个对象、下一个对象、类型、引用个数、val=18】（这里会存储age对象的value值）
age = 18

内部会创建一些数据【上一个对象、下一个对象、类型、引用个数、items=元素】（这里会存储列表中的元素）
hobby = ['跳泥坑','画画']


```

##### 2.类型封装结构体

``` C
date = 3.14

C语言中，内部会创建：
	_ob_next = refchain中的下一个对象
	_ob_prev = refchain中的上一个对象
	ob_refcnt = 1 #计数器，默认值为1，有其它变量引用时，引用计数器会发生变化
	ob_type = float
	ob_fval = 3.14
```

#### 3.引用计数器

```python
v1 = 3.14 #浮点数
v2 = 999 #整数
v3 = (1,2,3) #元组
```

引用计数器是基于refchain（环状双向链表）和类型封装体来实现的：

当python程序运行时，会根据数据类型的不同，找到不同的类型结构体，根据结构体中的字段来创建相关的数据，然后将对象添加到refchain双向列表中。

在C源码中有两个关键结构体：PyObject（存每种数据结构都有的）、PyVarObject（每种数据类型对应的不同）



<img src="/Users/shiyi/Library/Application Support/typora-user-images/image-20240916163414342.png" alt="image-20240916163414342" style="zoom:80%;" />

- 引用

  ```python
  a = 999
  b = a
  ```

- 删除引用

  ```py
  a = 999
  b = a
  del b #删除对象b：b对象引用计数器 -1
  del a #a变量删除：a对应对象引用计数器 -1
  
  
  ```

##### 垃圾回收

当对象的引用次数为0时，对象没有被使用，变成垃圾，需要回收

回收：1.对象从refchain链表中移除；2.将对象销毁，释放内存



##### 循环引用问题

![image-20240916175137734](/Users/shiyi/Library/Application Support/typora-user-images/image-20240916175137734.png)





## 2.标记清除

目的：解决计数器循环引用的不足

实现：在python的底层，再维护一个链表，链表中存放可能存在循环引用的对象

![image-20240916175408229](/Users/shiyi/Library/Application Support/typora-user-images/image-20240916175408229.png)



在python内部，某种情况下 触发，扫描可能存在循环引用中的链表中的每个元素，检查是否有循环引用，如果有则让双方的引用计数器 -1，如果是0则垃圾回收

问题：

- 什么时候扫描
- 可能存在循环引用的链表扫描代价大，每次扫描耗时久





## 3.分代回收

![image-20240916180218570](/Users/shiyi/Library/Application Support/typora-user-images/image-20240916180218570.png)

可能存在循环引用的对象，维护成3个链表：

- 0代：0代对象个数达到700个，扫描一次

- 1代：0代扫描10次，1代扫描一次

- 2代：1代扫描10次，2代扫描一次

  



## 4.小节

在python中维护了一个refchain的双向环状链表，这个链表中存储程序创建的所有对象，每种类型的对象都有一个_ob_refcnt引用计数器的值，引用个数随着引用和删除进行+1和-1，最后当引用计数器变为0时会进行垃圾回收（对象销毁，从refchain中移除）。

但是，在python中，对于那些可以有多个元素组成的对象，可能存在循环引用问题，为了解决循环引用，引入了标记清除和分代回收，在其内部，变成了总共维护四个链表 ：

- refchain

- 2代

- 1代

- 0代

  refchain存所有对象，后三个存可能循环引用的对象

当源码内部达到扫描的阈值时，会触发扫描下一代链表，0代是700个，触发扫描1代，1代扫描10次触发2代，2代扫描10次触发。触发之后会进行标记清除的动作，有循环引用的各自 -1，引用次数为0的时候进行清除。



BUT，python中还有一些优化机制。

## 5.缓存

### 池

为了避免重复创建和销毁一些常见对象，维护一个池

```python
#启动解释器时，python内部会帮我们创建一些常用值：-5、-4、-3......257
#小数字池
v1 = 3
v2 = 256 #直接去池中取，不会重新开辟内存

v3 = 999
v4 = 10000 #开辟内存，加入refchain


```



### free_list（float/list/tuple/dict）

当一个对象的引用计数器为0时，按理说应该回收，但是内部不会回收，而是将对象添加到free_list链表中当缓存，以后再创建对象时，不在重新开辟内存，而是直接使用free_list

```python
v1 = 3.14 #开辟内存，内部存储结构中定义那几个值，并存到refchain中

del v1 #将对象放入free_list中缓存，超过80个（free_list缓冲池满了）则销毁，

v9 = 999.99 #不会重新开辟内存，而是去free_list中获取对象，将其初始化，然后放到refchain中

#引用计数器为0时，会先判断free_list缓冲池是否已经满了，没满放进去，满了就销毁
```

- float、list、dict的free_list都是存80个

- tuple是元素存20个（索引最多到19）

  ```
  free_list = [0,         1,                2,    3 ... 19]
  					[空元组] [只有1元素的元组] [只有2元素的元组]...
  										2000个
  ```

- str类型维护一个 **unicode_latin[1,256]**



今天学的质量很高，了解了闭包和python的装饰器，了解了python的垃圾回收机制是引用计数器、标记清除和分代回收，缓存free_list



# 14.python中的逻辑运算符

Python中有3个逻辑运算符：and，or，not

顺序 Not >and > or



# 15.为什么不建议以下划线作为标识符的开头

python没有私有变量的概念，所以约定俗成以下划线开头来声明一个变量为私有。如果不想让变量私有，则不要使用下划线开头。

是一种开发规范。



# 16.join（）和split（）

join可以将指定字符添加至字符串中

```python
',' .join('12345')

#运行结果
'1, 2, 3, 4, 5'
```

Split（）可用于指定字符分割字符串

```python
'1, 2, 3, 4, 5'.split(',')

#运行结果
['1', '2', '3', '4', '5']

```



# 17.标识符长度

标识符的长度可以是任意的。

但是命名要遵循：

- 只能以下划线或者A-Z/a-z中的字母开头
- 其余部分可以使用A-Z/a-z/0-9
- 区分大小写
- 关键字不能作为标识符（比如join，split）



# 18.缩进

指定一个代码块，循环、类、函数等中所有的代码块都在缩进块中指定。通常使用四个空格，也就是一个tab。没有正确是缩进python会报错



# 19.什么是python模块？python常用的内置模块

python模块是包含python代码的.py文件。此代码可以是函数或者变量。

常用内置模块：

- pytest（测试框架，动态测试。参数化测试
- unitest（支持断言、设置清理环境）
- mock（集成到unitest.mock中了）用于创建模拟对象
- selenium（UI自动化测试）
- requests（发送HTTP请求的第三方库，用于web服务的API接口测试）
- beautifulSoup（用于解析HTML和XML文档的库，适用于提取web页面中的信息）
- radom、data time、sys、math



# 20.python是一种解释型语言

解释型语言会在每次运行时直接读取并执行，而不是先编译成机器码。

当运行一个python程序时：

- 逐行读取源代码
- 翻译成字节码
- 立即执行字节码

CPython（底层是C语言实现的，它负责解释python代码并执行）的实现会在第一次运行脚本时，将源代码编译成字节码（.pyc文件），以加快后续的执行速度。编译后的字节码仍然是由解释器来执行的，而不是直接由硬件来执行。
