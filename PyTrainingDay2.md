##### Python基础

**1.1. list**

Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。

如：

```python
###构建list
a =["b","c","d"]
print(a)
#['b', 'c', 'd']
###获取list个数
print(len(a))
#3
###使用索引访问list
print(a[0])
#b
###追加元素到末尾
a.append('e')
print(a)
#['b', 'c', 'd', 'e']
###追加元素到指定位置
a.insert(0,'a')
print(a)
#['a', 'b', 'c', 'd', 'e']
###删除末尾元素
a.pop()
print(a)
#['a', 'b', 'c', 'd']
###删除指定位置元素
del a[1]
print(a)
#['I', 'c', 'd']
###删除指定元素I
a.remove('I')
print(a)
#['c', 'd'恒#['c', 'd'geng#['c', 'd'恒#['c', 'd']
###添加多个元素或者一个列表
a.extend(['e','f','h','g'])
print(a)
#['c', 'd', 'e', 'f', 'h', 'g']
###列表排序，默认升序
a.sort()
print(a)
#['c', 'd', 'e', 'f', 'g', 'h']
###降序排列
a.sort(reverse=True)
print(a)
#['h', 'g', 'f', 'e', 'd', 'c']
###将列表反转
a.reverse()
print(a)
#['c', 'd', 'e', 'f', 'g', 'h']
###列表
###替换指定元素
a[0]= "I"
print(a)
#['I', 'b', 'c', 'd']

```

**1.2. Tuple**

另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改。

如：

```python
a =("b","c","d")   #tuple和list的标志是前者是括号，后者是方括号
a = (1)  #此时要加逗号(,),即(1,),否则会当成运算公式的小括号
###删除整个元组
del a
```

**1.3. Tuple和list相互转换**

- list(tuple): tuple-->list
- tuple(list): lsit --> tuple

```python
li = ['a','b','c']
tu = (1,2,3)
New_li = list(tu)
print(New_li)
New_tu = tuple(li)
print(New_tu)
```

**2.1.作业**

定义一个列表，包含自己的家庭成员，并在指定位置插入给定元素，例如你的男女朋友名称等。再将男女朋友名字移除等操作。

```python
family = ["grandpa","grandma","father","mother","sister"]
family.insert(5,"girlfriend")
print(family)
#['grandpa', 'grandma', 'father', 'mother', 'sister', 'girlfriend']
del family[5]
print(family)
#['grandpa', 'grandma', 'father', 'mother', 'sister']
```



















































