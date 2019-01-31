### 函数

#### 调用函数

python内置了很多常用的函数，可以直接调用，但是需要知道函数的名称和参数，比如求绝对值：`abs`，只有一个参数，内置函数可以通过[python的官方网站查看文档](https://docs.python.org/3/library/functions.html)。也可以使用交互式命令行通过`help(abs)`查看`abs`函数的帮助信息：

```python
###如果调用参数不对，会报TypeError的错误，并且会提示：
abs(1,2)
#TypeError: abs() takes exactly one argument (2 given)
```

`max`函数可以接受任意多个参数，并返回最大的那个：

```python
print(max(1,2))
#2
```

#### 数据类型转换

Python内置的常用函数还包括数据类型转换函数，比如`int()`函数可以把其他数据类型转换为整数：

```python
print(int('123'))
#123
print(float('123.23'))
#123.23
```

#### 函数关键字

​        python中一共含有32个关键字：`false`, `none`, `true`,
`and`, `as`, `assert`, `break`, `class`, `continue`, `def`, `del`, 
`elif`, `else`, `except`, `finally`, `for`, `from`, `global`, `if`, 
`import`, `in`, `is`, `lambda`, `nonlocal`, `not`, `or`, `pass`, 
`raise`, `return`, `try`, `while`, `with`, `yield`

- 关键字-是Python内置的、具有特殊意义的表示符
  ,使用时关键字后面不需要括号。

#### 函数的定义

​        在Python中，定义一个函数要使用`def`语句，依次写出函数名、括号、括号中的参数和冒号`:`，然后，在缩进块中编写函数体，函数的返回值用`return`语句返回。

```python
#定义一个求绝对值的函数
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
print(my_abs(-99))
###99
###什么也不做的函数：空函数
def nop():
    pass
###函数参数出现错误时，设置函数的参数的报告信息：
def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

函数返回多个值：

```python
import math
def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny
x, y = move(100, 100, 60, math.pi / 6)
print(x,y)
#151.96152422706632 70.0
###其实返回值只是一个tuple
r = move(100, 100, 60, math.pi / 6)
print(r)
#(151.96152422706632, 70.0)
```
定义函数时，需要确定函数名和参数个数；
如果有必要，可以先对参数的数据类型做检查；
函数体内部可以用`return`随时返回函数结果；
函数执行完毕也没有`return`语句时，自动`return None`。
函数可以同时返回多个值，但其实就是一个tuple。
#### 函数参数与作用域
python的函数定义非常简单，灵活度非常高，比如：
```python
def cal2(x,n):
    s = 1
    while n > 0:
        n = n -1
        s = s * x
    return s
print(cal2(5,2))
#25
#x，n是位置参数，传入的值一次传递给x,n
```
**默认参数**：
```python
def cal2(x,n=2):
    s = 1
    while n > 0:
        n = n -1
        s = s * x
    return s
print(cal2(5,2))
#25
print(cal2(5))
#25
print(cal2(5,3))
#125
```
而对于`n > 2`的其他情况，就必须明确地传入n，比如`power(5, 3)`。
设置默认参数时，有两点要注意：

1. 必选参数在前，默认参数在后，否则Python的解释器会报错（思考一下为什么默认参数不能放在必选参数前面）；
2. 如何设置默认参数。
   当函数有多个参数时，把变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。

**可变参数**：

参数是可变的，可以将参数作为一个list或tuple传进来，其与可变参数的不同是仅仅在参数前面加了一个`*`号，这样函数定义如下：

```python
###将参数作为一个list或tuple传进来
def calc(Nos):
    sum = 0
    for i in Nos:
        sum = sum + i*i
    return sum
print(calc([1,2,3]))
#14
print(calc([1,2,3,4,5]))
#55
###定义一个可变参数
def calc(*Nos):
    sum = 0
    for i in Nos:
        sum = sum + i*i
    return sum
print(calc())
#0
print(calc(1,2))
#5
```

**关键字参数**:

​        可变参数允许传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。关键字参数使用`**`标记如下：

```python
def roster(name,age,**ot):
    print('name:', name, 'age:', age, 'other:', ot)
print(roster('me',3))
#name: me age: 3 other: {}
def roster(name,age,**ot):
    print('name:', name, 'age:', age, 'other:', ot)
print(roster('me',3))
print(roster('me',3,city ='guangzhou'))
###关键字可扩展函数的功能，真贱可选项
extra = {'city': 'Beijing', 'job': 'Engineer'}
print(roster('Jack', 24, city=extra['city'], job=extra['job']))
#name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
extra = {'city': 'Beijing', 'job': 'Engineer'}
print(roster('me',3,**extra))
#name: me age: 3 other: {'city': 'Beijing', 'job': 'Engineer'}
```

**命名关键字参数**:

限制关键字参数的名字，就可以用命名关键字参数，如，只接收`city`和`job`作为关键字参数。这种方式定义的函数如下：

```python
def roster(name,age,*,city,job):
    print(name, age, city, job)
print(roster('Jack', 24, city='Beijing', job='Engineer'))
#Jack 24 Beijing Engineer
###如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了：
def roster(name,age,*args,city,job):
    print(name, age, args,city, job)
print(roster('Jack', 24, city = 'Beijing',job = 'Engineer'))
#Jack 24 () Beijing Engineer
print(roster('Jack', 24, 'Beijing','Engineer'))
#roster() missing 2 required keyword-only arguments: 'city' and 'job'
print(roster('Jack', 24,22,33, city = 'Beijing',job = 'Engineer'))
#Jack 24 (22, 33) Beijing Engineer
```

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

Python的函数具有非常灵活的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。

默认参数一定要用不可变对象，如果是可变对象，程序运行时会有逻辑错误！

要注意定义可变参数和关键字参数的语法：

`*args`是可变参数，args接收的是一个tuple；

`**kw`是关键字参数，kw接收的是一个dict。

以及调用函数时如何传入可变参数和关键字参数的语法：

可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装list或tuple，再通过`*args`传入：`func(*(1, 2, 3))`；

关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装dict，再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`。

使用`*args`和`**kw`是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。

命名的关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。

定义命名的关键字参数在没有可变参数的情况下不要忘了写分隔符`*`，否则定义的将是位置参数。

#### Homework

​     1. 实现random.sample方法

```python
random.sample
random.sample(sequence, k)，从指定序列中随机获取指定长度的片断。sample函数不会修改原有序列
代码如下:
list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
#从list中随机获取5个元素，作为一个片断返回
slice = random.sample(list, 5)  
print(slice)
#每一次出现的5个list元素不一样
#原有序列并没有改变
print(list)
```

2. 实现Max方法

```python
###类型为字符串,max 返回了最大值
a='1,2,3,4'          
print(max(a))
#4
###类型是列表
a=[1,2,3,4]
print(max(a))
#4
###类型是元组
a=(1,2,3,4)
print(max(a))
#4
#列表里面是元组
a=[(1,2),(2,3),(3,4)]
#按照元素里面元组的第一个元素的排列顺序，输出最大值（如果第一个元素相同，则比较第二个元素，输出最大值）
print(max(a))
#(3,4)
#按ascii码进行排序:a>A,
a=[('a',1),('A',1)]
print(max(a))
#('a', 1)
#比较字典里面的最大值，会输出最大的键值
a={1:2,2:2,3:1,4:'aa'}                 
print(max(a))
#4
```

3. 实现判断两个字符串是否相等的方法

```python
a = input("请输入一个字符a：")
b = input("请输入一个字符b：")
if a == b:
    print("a和b相同")
else:
    print("a和b不相同")
```



























