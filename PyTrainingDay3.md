##### Python文件的打开方式

- r只读，r+读写，不创建新文件
- w新建只写，w+新建读写，二者都会将原有文件清零
- a附加写方式打开，不可读；a+附加读写方式打开

python使用open()这个函数来打开文件返回对象,使用write()写入对象

**open 第二参数**

| "r"  | 以只读方式打开文件                               |
| ---- | :----------------------------------------------- |
| "w"  | 以写入方法打开文件，会覆盖已储存的内容           |
| "x"  | 如果存在该文件，打开会引发异常                   |
| "a"  | 以写入模式打开文件，如果存在该文件，会在末尾添加 |
| "b"  | 以二进制模式打开文件                             |
| "t"  | 以文本模式打开文件（默认）                       |
| "+"  | 可读写模式（可添加到其他模式中去）               |
| "U"  | 通用换行符支持                                   |

**文件对象的方法**：

| close()           | 关闭文件                                                     |
| ----------------- | ------------------------------------------------------------ |
| read(size=-1)     | 从文件中读取size个字符，当未给定size或给定负值时，读取剩余的所有字符，然后作为字符返串回 |
| readline()        | 从文件中读取一整行字符串                                     |
| write(str)        | 将字符串str写入文件中                                        |
| writelines(seq)   | 向文件中写入字符串序列seq，seq应该是一个返回字符串的可迭代对象 |
| seek(offset,from) | 在文件中移动文件指针，从from（0代表文件起始位置，1，代表当前位置，2代表文件末尾）偏移offset个字节 |
| tell()            | 返回当前在文件中的位置                                       |

```python
fd = open('hw.txt','r')
print(fd.read())
#Hello,world
with open('hw.txt','r+') as fd:
    print(fd.read())
#Hello,world
fd = open('hw.txt','w+')
print(fd.read()) #清空文件
fd.write("Hello,world")
fd = open('hw.txt','r')
print(fd.read())
#Hello,world

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181102190900704.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0phY2swMDEwMTE=,size_16,color_FFFFFF,t_70)

##### Dictionary

Python内置了字典：dict的支持，使用{}花括号代表dic；在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。如：

```python
###创建dic
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
print(d['Michael'])
#95
###判断Michael是否存在于dic中
print('Michael' in d)
#True
###使用get判断
print(d.get('smiles'))
#None
###删除元素
d.pop('Bob')
print(d)
#{'Michael': 95, 'Tracy': 85}
###添加元素
d['Bob'] = '75'
print(d)
#{'Michael': 95, 'Tracy': 85, 'Bob': '75'}
###输出dic
print(str(d))
#{'Michael': 95, 'Tracy': 85, 'Bob': '75'}
###字典的长度
print(len(d))
#3
```

请务必注意，dict内部存放的顺序和key放入的顺序是没有关系的。

和list比较，dict有以下几个特点：

1. 查找和插入的速度极快，不会随着key的增加而变慢；
2. 需要占用大量的内存，内存浪费多。

而list相反：

1. 查找和插入的时间随着元素的增加而增加；
2. 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。

dict可以用在需要高速查找的很多地方，在Python代码中几乎无处不在，正确使用dict非常重要，需要牢记的第一条就是dict的key必须是**不可变对象**。

这是因为dict根据key来计算value的存储位置，如果每次计算相同的key得出的结果不同，那dict内部就完全混乱了。这个通过key计算位置的算法称为哈希算法（Hash）。

要保证hash的正确性，作为key的对象就不能变。在Python中，字符串、整数等都是不可变的，因此，可以放心地作为key。而list是可变的，就不能作为key：

```python
###廖雪峰的python教程###
key = [1, 2, 3]
d[key] = 'a list'
TypeError: unhashable type: 'list'
```

##### Set集合

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

```python
s= set([1,2,3,3,4])
print(s)
#{1, 2, 3, 4}
###添加元素
s.add(5)
print(s)
#{1, 2, 3, 4, 5}
###移除元素
s.remove(5)
#{1, 2, 3, 4}
```

set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

```python
###交集
s1 = set([1,2,3])
s2 = set([2,3,4])
ss = s1&s2
print(ss)
#{2, 3}
###并集
ss = s1 | s2
print(ss)
#{1, 2, 3, 4}
```

##### python处理excel和csv文件

在python中，对excel表格读，写，追加数据，使用以下三个模块：

1. xlrd读取excel表中的数据
2. xlwt创建一个全新的excel文件，然后对这个文件进行写入内容以及保存
3. xlutils读入一个excel文件，然后进行修改或追加，不能操作xlsx，只能操作xls（能将xlrd.Book转为xlwt.Workbook,从而得以在现有xls基础上修改数据，并创建一个新的xls，实现修改）

```python
###python读出excel文件
import xlrd
file ='python.xlsx'
data =xlrd.open_workbook(filename=file)
table = data.sheets()[0]
nrows = table.nrows
ncols = table.ncols
print("行数：%s\n列数%s" %(nrows,ncols))
#行数：9
#列数3
###获取整行整列的值，以list形式输出
row = table.row_values(0)
col = table.col_values(0)
print("row: %s\ncol: %s" %(row,col)) 

###获取单元格数据
c_A1 = table.cell_value(0,0)
c_C4 = table.cell_value(3,2)
print("A1: %s\nC4: %s" %(c_A1,c_C4))

###python导入csv文件
import csv

with open("python.csv", "r", encoding = "UTF-8-sig") as f:  
    ##使用encoding = "UTF-8-sig"的原因请看：
    ##https://www.cnblogs.com/chongzi1990/p/8694883.html
    reader = csv.reader(f)
    rows = [row for row in reader]

print(rows)
```



##### Homework

```python
fd = open('homework.txt','r', encoding='UTF-8') #打开文件
lines={}  #以dic形式保存
for line in fd.readlines():
    line = line.strip('\n')  #去除开头的和末尾的\n
    key = line.split()[0]  #第一列数据为key
    value = [line.split()[1], line.split()[2]] #第二、三；列数据为value
    lines[key] = value
print(lines)

dict2 = {}

for v in lines.values(): #遍历dic中的键值
    for j in v:          #返回的是一个list的v，故而还需遍历list
        if j in dict2:   
            dict2[j] = dict2[j]+1
        else:
            dict2[j] = 1
print(dict2)
for i, v in dict2.items():
    if v > 1:
        print("对应多个项目的是:%s,共参加了%s个项目" %(i,v))
```





































































