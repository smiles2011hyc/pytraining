#### Python条件语句

Python条件语句是通过一条或多条语句的执行结果（True或False）来决定执行的代码块。我们可以通过下图来简单了解条件语句的执行过程：

```flow
st=>start: Start
Condition?=>condition: Condition？
Conditioncode=>operation: Condition code
e=>end: End

st->Condition?
Condition?(yes)->Conditioncode->e
Condition?(no)->e
```

![1548777470173](C:\Users\18019\AppData\Roaming\Typora\typora-user-images\1548777470173.png)

```python
i = 20
if i >=19:
    print('The number is',i)
    print('big')
```

​    添加`else`语句,意思是，如果`if`判断是`False`，不要执行`if`的内容，去把`else`执行了：

```python
i = 20
if i >=19:
    print('The number is',i)
    print('big')
else:
    print('The number is',i)
    print('little')
```

可以用`elif`做更精细的判断：

```python
i = 3
if i >=19:
    print('The number is',i)
    print('right')
elif i >=6:
    print('The number is',i)
    print('middle')
else:
    print('The number is',i)
    print('little')
```

`elif`是`else if`的缩写，完全可以有多个`elif`，所以`if`语句的完整形式就是：

```python
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```

#### 循环语句

python的循环有两种，一种是**for...in...循环**，依次把list或tuple中的每个元素迭代出来：

```python
a = ['b','c','d']
for i in a:
    print(i)
###此循环是把每个元素带入变量i，然后执行缩进块的语句
###比如进行加和1，2，3...10
sum = 0
i = [1,2,3,4,5,6,7,8,9,10]
for x in i:
    sum += x
print(sum)     #print()必须删除缩进，不然会输出计算出来的每一个循环中的变量值
###由于1-100写出来有点困难，故使用range()函数生成，并使用list()函数转换为list
print(range(5))
#range(0, 5)
print(list(range(5)))
#[0, 1, 2, 3, 4]
sum = 0
n = list(range(101))
for i in n:
    sum += i
print(sum)
```

另一种是**while循环**，只要条件满足，就不断循环，条件不满足时退出循环，比如求100内偶数之和，可用while循环实现：

```python
sum = 0
n = 100
while n > 0:
    sum =sum + n
    n = n-2
print(sum)
```

**break语句**可以提前退出循环，如：

```python
###正常输出1~100的数字
n = 1
while n <= 100:
    print(n)
    n += 1
print('End')
###提前结束循环
n =1 
while n <= 100:
    if n > 10:
        break
    print(n)
    n +=1
print('End')
```

continue语句可以跳过当前循环，直接开始下一次的循环：

```python
n =0 
while n <= 100:
    n +=1
    if n % 2 == 0:  #如果n是偶数，执行continue语句
        continue    #continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)
#1，3，5，7...99
```

则`continue`的作用是提前结束本轮循环，并直接开始下一轮循环。

#### 三目表达式

python中的三目表达式中条件为真时的结果 if 判断的条件 else 条件为假时的结果

```python
a = int(input("please enter the first integer:"))
b = int(input("please enter the second integer:"))
if a == b:
    print("Equal")
elif a > b:
    print("The greater int is:",a)  
else:
    print("The greater int is:",b)
###三目表达式
h = a if a >= b else b
print("The greater int is:", h )
###写一个算法（流程图和python程序）：输入三个数，输出其最大者
a = int(input("please enter the first integer:"))
b = int(input("please enter the second integer:"))
c = int(input("please enter the third integer:"))
###三目表达式的第一种写法
h = a if (a>b) else b
i = h if (h >c) else c
print(i)
###另一种写法
j = (a if (a>b) else b) if ((a if (a>b) else b)>c) else c
print(j)
```

#### 容器

​       容器是用于盛放元素的，由于盛有许多的元素，容器都是可以迭代遍历的：最常用的容器包括【元组】、【列表】、【字典】、【集合】等；字符串是有序字符集，本质上也是容器。

我们在对比和讨论容器的特性时，最常考虑的因素有：

1. 是否有序
2. 是否可重复
3. 如何访问其中的元素
4. 是否可以编辑
5. 如何遍历

#### 可迭代对象

​        如果给定一个list、tuple、dictionary、str等，我们可以通过`for`循环来遍历这类对象，这种遍历我们称为**迭代（Iteration）**；而通过迭代读取的数据供人们使用的对象称之为**可迭代对象（Iterable）**。

​        如何判断一个对象式可迭代对象呢？方法是通过collections模块的Iterable类型判断：

```python
from collections import Iterable
print(isinstance('abc',Iterable))  #True:str is iterable
print(isinstance([1,2,3],Iterable)) #True:list...
print(isinstance({'dede':123},Iterable)) #True, dic...
```

​    实现对list或tuple的下标循环

```python
a = ['c','d','e']
###第一种方法
for i in range(len(a)):
    print(i,a[i])
###第二种方法:使用python的内置函数enumerate可以将list变成index-value对。
for i, value in enumerate(a):
    print(i,value)
###当一个list中的value含有两个变量时：
b = [(1,2),(3,4),(5,6)]
for x ,y in b:
    print(x,y)
###与dic不同点在于如下所示：
d={'python':1,'php':2,'java':3}
for k , v in d.items():
    print(k,v)
```

#### 生成器

​        首先了解一下列表生成式（List Comprehensions），是python内置的非常简单却强大的可以用来创建lsit的生成式。如：

```python
###廖雪峰python###
d = list(range(1,6))
print(d)
#[1, 2, 3, 4, 5]
###如果生成[1*1,...5*5]
a = []
for i in list(range(1,6)):
     a.append(i*i)
print(a)
###另一种方法
print([i * i for i in range(1,6)])
###筛选偶数
print([i * i for i in range(1,6) if i % 2 == 0 ])
```

​        通过列表生成式，可以直接创建一个列表，但是创建的列表过大会占用很大的存储空间，开发者通过将列表元素按照某种算法推算出来，可以在后续的循环过程中不断生成，这样就不必生成完整的list，而节省大量的空间，故而在python中这种一边循环一遍计算的机制称为**生成器：generator**。

```python
###要创建一个generator，有很多种方法。第一种方法是把一个列表生成式的[]改成()，就创建了一###个generator：
L1 = (i*i for i in range(6))
print(L1)
#[0, 1, 2, 3, 4, 5]
g = (i*i for i in range(6))
print(g)
#<generator object <genexpr> at 0x0000026836F6C9A8>
print(next(g))
#0
print(next(g))
#1
###这表明g保存的是算法，每次调用next(g)，就可以计算出g的下一个元素的值。
###使用for循环调用next(g)
for n in g:
    print(n)
#0
#1
#4
#9
#16
#25
```

#### 迭代器

​        可以被`next()`函数调用并不断返回下一个值的对象称为**迭代器**：`Iterator`。生成器都是`Iterator`对象，但`list`、`dict`、`str`虽然是`Iterable`，却不是`Iterator`。把`list`、`dict`、`str`等`Iterable`变成`Iterator`可以使用`iter()`函数：

```python
from collections import Iterator   
print(isinstance(iter([]),Iterator))
#True
print(isinstance(iter('abc'),Iterator))
#True
```

因为python的`Iterator`对象表示的是一个数据流，可以将这个数据流看做一个有序序列，但我们却不能提前知道序列的长度，只能通过`next()`函数实现按需计算下一个数据，故而`Iterator`的计算是惰性的，只有在需要返回下一个数据时它才会计算

#### Homework

```python
###“参考”各位大神的答案###
import random
start = 1
while start != 2:
    while start == 1:
        ran_n = random.sample(range(10),3) #生成0~9之间的3个不相等的数
        print(ran_n)
        a = input("请输入一个0~9之间的数字：")
        if a.isdigit():
            b = int(a)
            if b >9 or b <0:
                print("您输入的数字不在0~9之间，请重新输入")
            else:
                break
        else:
            print("请重新输入一个0~9之间的数字：")
            continue
    if b == ran_n[0]:
        print("荣获第一名")
    elif b == ran_n[1]:
        print("荣获第二名")
    elif b == ran_n[2]:
        print("荣获第三名")
    else:
        print("您未得奖")
    start = int(input("输入1重新开始游戏，输入2则结束游戏："))
    if start == 1:
        continue
    else:
        break
        
#[1, 9, 8]

#请输入一个0~9之间的数字：10
#您输入的数字不在0~9之间，请重新输入
#[0, 9, 7]

#请输入一个0~9之间的数字：3
#您未得奖

#输入1重新开始游戏，输入2则结束游戏：2
```











































































