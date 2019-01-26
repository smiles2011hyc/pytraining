#### 环境搭建anaconda环境配置

- Add Anaconda to my PATH environment variable

- 运行Spyder IDE

---

#### Python初体验

```python
#print and input初体验
print("Hello,world")     ##Hello，world
me = input("面向世界:")   ##面向世界:hello,world
print("%s %(me)")       ##Hello，world
```

---

#### Python基础讲解

1. **python变量特性和命名规则**
   - 如无特殊情况，文件一律使用 UTF-8 编码
   - 如无特殊情况, 文件头部必须加入`#-*-coding:utf-8-*-`标识 #Spyder IDE默认存在

|   变量名必须是大小写英文、数字和下划线_的组合   |
| :---------------------------------------------: |
| 等号=是赋值语句，其可以对任意数据进行反复的赋值 |
|               变量名不能包含空格                |
|     不要将变量名与python关键值或函数名重复      |

2. **注释方法**
   - 使用：# 进行注释
3. **python中":"的作用**
   - 以“:"结尾时，缩进的语句视为代码块
   - 在切片时表示步长

4. **dir()和help()的使用**
   - **dir()** 函数不带参数时，返回当前范围内的变量、方法和定义的类型列表；带参数时，返回参数的属性、方法列表。如果参数包含方法__dir__()，该方法将被调用。如果参数不包含__dir__()，该方法将最大限度地收集参数信息。
   - help():帮助用户了解模块、类型、对象、方法、属性的文档信息。

5. **import使用**
   - import:导入模块或模块中的对象、函数、类、变量

|               导入整个模块：import module_name               |
| :----------------------------------------------------------: |
| 导入模块中特定的函数：from module_name import function_name  |
| 使用as给模块指定别名：import module_name (from modele_name import function_name) as XX |
|       导入模块中的所有函数：from module_name import *        |

6. pep8介绍
   - [PEP8编码规范](https://blog.csdn.net/ratsniper/article/details/78954852)

---

#### python数值基本知识

1. 数值类型：int(整数)、float(浮点数)、bool(布尔值，True(1),False(0))、none(空值)，etc。

2. 运算符：

   2.1. 算术运算符：+、-、*、/（结果是浮点数）、//（取整）、%（取余）、**（乘方）

3. 逻辑运算符：and、or、not

4. 成员运算符： in、not in

5. 身份运算符：判断两个标识符是不是因用自一个对象

   运算符优先级：

|           符号            |         描述         |
| :-----------------------: | :------------------: |
|            **             |    指数（最高级）    |
|         * / % //          | 乘，除，取余和取整除 |
|            + -            |        加减法        |
|           >> <<           |   右移，左移运算符   |
|             &             |         and          |
| = %= /= //= -= += *= **== |      赋值运算符      |
|         is is not         |      身份运算符      |
|         in not in         |      成员运算符      |
|        not and or         |      逻辑运算符      |

6.string（字符串）

1. 定义：字符串是以单引号`'`或双引号`"`括起来的任意文本
2. 基本操作：

```python
a = "Hello"
b = "World"
print(a+b)
print(a*2)
print(a[0])
print(a[1:3])
for c in a:
    print(c)
###依次显示###
HelloWorld
HelloHello
H
el
H
e
l
l
o
```

3. 格式化输出

   在python中，采用的格式化方式是使用`%`实现：

```python
print("Hello, %s" % "world")
##输出：Hello, world
print("Hi,%s,you have $%d" %("Michael",1000))
##输出：Hi,Michael,you have $1000
```

在字符串内部，`%s`表示用字符串替换，`%d`表示用整数替换，有几个`%?`占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个`%?`，括号可以省略。

常见的占位符有：

| 占位符 | 替换内容     |
| ------ | ------------ |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

**作业：**

```python
name = input("请输入你的姓名：")
age = int(input("请输入你的年龄："))
gender = input("请输入你的性别：")
print("你的姓名:%s,你是%s出生的,你的性别:%s" %(name,2019-age,gender))
#请输入你的姓名：regularboy
#请输入你的年龄：3
#请输入你的性别：man
#你的姓名:regularboy,你是2016出生的,你的性别:man
```

