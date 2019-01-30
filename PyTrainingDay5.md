#### 正则表达式

​        字符串是编程时涉及到的最多的一种数据结构(字符序列），正则表达式在对字符串进行处理的方面具有非常强大的能力。

比如判断一个字符串是否是合法的Email的方法是：

1. 创建一个匹配Email的正则表达式；
2. 用该正则表达式去匹配用户的输入来判断是否合法。

在正则表达式中，如果直接给出字符，就是精确匹配，如`\d`可以匹配一个数字，`\w`可以匹配一个字母或数字，所以：

- `'00\d'`可以匹配`'007'`，但无法匹配`'00A'`；
- `'\d\d\d'`可以匹配`'010'`；
- `'\w\w\d'`可以匹配`'py3'`；

`.`可以匹配任意字符，所以：

- `'py.'`可以匹配`'pyc'`、`'pyo'`、`'py!'`等等。

用`*`表示任意个字符（包括0个），用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符

#### re模块

Python 自1.5版本起增加了re 模块，它提供 Perl 风格的正则表达式模式；re 模块使 Python 语言拥有全部的正则表达式功能。 

**re模块**包含了所有的正则表达式的功能

python的字符串本身也用`\`转义，所以需特别注意：

```python
s = 'ABC\\-001' 
#对应的正则表达式字符串为：'ABC\-001'
```

可用python的`r`前缀，就不用考虑转义的问题：

```python
s = r'ABC\-001'
#对应的正则表达式字符串为：'ABC\-001'
```

正则表达式的函数语法

```python
re.match(pattern,string,flags = 0)
```

函数参数说明：

| 参数    |                             描述                             |
| ------- | :----------------------------------------------------------: |
| pattern |                       匹配的正则表达式                       |
| string  |                       要匹配的字符串。                       |
| flags   | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。参见：[正则表达式修饰符 - 可选标志](http://www.runoob.com/python/python-reg-expressions.html#flags) |

匹配成功re.match方法返回一个匹配的对象，否则返回None。

我们可以使用group(num) 或  groups() 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述                                                         |
| :----------: | ------------------------------------------------------------ |
| group(num=0) | 匹配的整个表达式的字符串，group() 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
|   groups()   | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。     |

判断正则表达式是否匹配：

```python
import re
print( re.match(r'^\d{3}\-\d{3,8}$', '010-12345'))
#<re.Match object; span=(0, 9), match='010-12345'>
print( re.match(r'^\d{3}\-\d{3,8}$', '010 12345'))
#none
```

**切分字符串**：

```python
###使用固定的字符进行切分代码：
import re
print('a b  c'.split(' '))
#['a', 'b', '', 'c']
print(re.split(r'\s+','a b  c'))
#['a', 'b', 'c']
###假如[]表示多个字符内的多个中的一个匹配即可
print(re.split(r'[\s\,]+', 'a,b, c  d'))
#['a', 'b', 'c', 'd']
print(re.split(r'[\s\,\;]+', 'a,b;; c  d'))
#['a', 'b', 'c', 'd']
```

**分组**：

```python
import re
m = re.match(r'(\d{3})-(\d{3,8})$', '010-12345')
print(m)
#<re.Match object; span=(0, 9), match='010-12345'>
#注意到group(0)永远是原始字符串，group(1)、group(2)……表示第1、2、……个子串。
print(m.group(0))
#010-12345
print(m.group(1))
#010
print(m.group(2))
#12345
```

**编译**：

当我们在Python中使用正则表达式时，re模块内部会干两件事情：

1. 编译正则表达式，如果正则表达式的字符串本身不合法，会报错；
2. 用编译后的正则表达式去匹配字符串。

如果一个正则表达式要重复使用几千次，出于效率的考虑，我们可以预编译该正则表达式，接下来重复使用时就不需要编译这个步骤了，直接匹配：

```python
import re
re_telephone = re.compile(r'^(\d{3})-(\d{3,8})$') #^表示是以(\d{3})开头的字符
print(re_telephone.match('010-12345').groups())
#('010', '12345')
print(re_telephone.match('010-8086').groups())
#('010', '8086')
```

**详细的[正则表达式模式](http://www.runoob.com/python/python-reg-expressions.html)。**

#### os模块

```python
import os
print(os.listdir())  ##获取当前文件夹的文件
print(os.getcwd())   ##获取当前工作目录
os.chdir(path)       ##改变工作目录
###http://www.runoob.com/python/os-file-methods.html
```

#### datetime模块

Reference：

1. https://www.cnblogs.com/cindy-cindy/p/6720196.html
2. http://www.runoob.com/python/python-date-time.html

- Python 程序能用很多方式处理日期和时间，转换日期格式是一个常见的功能。
- Python 提供了一个 time 和 calendar 模块可以用于格式化日期和时间。
- 时间间隔是以秒为单位的浮点小数。
- 每个时间戳都以自从1970年1月1日午夜（历元）经过了多长时间来表示。
- Python 的 time 模块下有很多函数可以转换常见日期格式。如函数time.time()用于获取当前时间戳, 如下实例:

```python
#引入时间模块
import time
T_now = time.time()
print("当前时间戳为：",T_now)
#当前时间为： 1548851313.3565192
```

很多python函数用一个元组组装起来的9组数字处理时间：

| 序号 | 字段         | 值                                   |
| ---- | ------------ | ------------------------------------ |
| 0    | 4位数年      | 2008                                 |
| 1    | 月           | 1 到 12                              |
| 2    | 日           | 1到31                                |
| 3    | 小时         | 0到23                                |
| 4    | 分钟         | 0到59                                |
| 5    | 秒           | 0到61 (60或61 是闰秒)                |
| 6    | 一周的第几日 | 0到6 (0是周一)                       |
| 7    | 一年的第几日 | 1到366 (儒略历)                      |
| 8    | 夏令时       | -1, 0, 1, -1是决定是否为夏令时的旗帜 |

上述也就是struct_time元组。这种结构具有如下属性：

| 序号 | 属性     | 值                                   |
| ---- | -------- | ------------------------------------ |
| 0    | tm_year  | 2008                                 |
| 1    | tm_mon   | 1 到 12                              |
| 2    | tm_mday  | 1 到 31                              |
| 3    | tm_hour  | 0 到 23                              |
| 4    | tm_min   | 0 到 59                              |
| 5    | tm_sec   | 0 到 61 (60或61 是闰秒)              |
| 6    | tm_wday  | 0到6 (0是周一)                       |
| 7    | tm_yday  | 1 到 366(儒略历)                     |
| 8    | tm_isdst | -1, 0, 1, -1是决定是否为夏令时的旗帜 |

```python
#时间戳单位最适于做日期运算。但是1970年之前的日期就无法以此表示了。太遥远的日期也不行，UNIX和Windows只支持到2038年。 
#从返回浮点数的时间戳方式向时间元组转换，只要将浮点数传递给如localtime之类的函数。
import time
localtime = time.localtime(time.time())
print("本地时间为：",localtime)
#本地时间为： time.struct_time(tm_year=2019, tm_mon=1, tm_mday=30, tm_hour=20, tm_min=43, tm_sec=46, tm_wday=2, tm_yday=30, tm_isdst=0)
```

**获取格式化的时间**：

```python
N_time = time.asctime(time.localtime(time.time()))
print("本地时间为：",N_time)
#本地时间为： Wed Jan 30 20:43:46 2019
```

**获取格式化日期**：

```python
print(time.strftime('%Y-%m-%d %H:%M:%S',time.localtime()))
print(time.strftime('%a %b %d %H:%M:%S %Y',time.localtime()))
a = 'Wed Jan 30 20:42:13 2019'
print(time.mktime(time.strptime(a,'%a %b %d %H:%M:%S %Y')))
#2019-01-30 20:43:46
#Wed Jan 30 20:43:46 2019
#1548852133.0
```

python中时间日期格式化符号：

- %y 两位数的年份表示（00-99）
- %Y 四位数的年份表示（000-9999）
- %m 月份（01-12）
- %d 月内中的一天（0-31）
- %H 24小时制小时数（0-23）
- %I 12小时制小时数（01-12）
- %M 分钟数（00=59）
- %S 秒（00-59）
- %a 本地简化星期名称
- %A 本地完整星期名称
- %b 本地简化的月份名称
- %B 本地完整的月份名称
- %c 本地相应的日期表示和时间表示
- %j 年内的一天（001-366）
- %p 本地A.M.或P.M.的等价符
- %U 一年中的星期数（00-53）星期天为星期的开始
- %w 星期（0-6），星期天为星期的开始
- %W 一年中的星期数（00-53）星期一为星期的开始
- %x 本地相应的日期表示
- %X 本地相应的时间表示
- %Z 当前时区的名称
- %% %号本身

**Time 模块**

Time 模块包含了以下内置函数，既有时间处理的，也有转换时间格式的：

| 序号 | 函数及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [time.altzone](http://www.runoob.com/python/att-time-altzone.html) 返回格林威治西部的夏令时地区的偏移秒数。如果该地区在格林威治东部会返回负值（如西欧，包括英国）。对夏令时启用地区才能使用。 |
| 2    | [time.asctime([tupletime\])](http://www.runoob.com/python/att-time-asctime.html) 接受时间元组并返回一个可读的形式为"Tue Dec 11 18:07:14 2008"（2008年12月11日 周二18时07分14秒）的24个字符的字符串。 |
| 3    | [time.clock( )](http://www.runoob.com/python/att-time-clock.html) 用以浮点数计算的秒数返回当前的CPU时间。用来衡量不同程序的耗时，比time.time()更有用。 |
| 4    | [time.ctime([secs\])](http://www.runoob.com/python/att-time-ctime.html) 作用相当于asctime(localtime(secs))，未给参数相当于asctime() |
| 5    | [time.gmtime([secs\])](http://www.runoob.com/python/att-time-gmtime.html) 接收时间戳（1970纪元后经过的浮点秒数）并返回格林威治天文时间下的时间元组t。注：t.tm_isdst始终为0 |
| 6    | [time.localtime([secs\])](http://www.runoob.com/python/att-time-localtime.html) 接收时间戳（1970纪元后经过的浮点秒数）并返回当地时间下的时间元组t（t.tm_isdst可取0或1，取决于当地当时是不是夏令时）。 |
| 7    | [time.mktime(tupletime)](http://www.runoob.com/python/att-time-mktime.html) 接受时间元组并返回时间戳（1970纪元后经过的浮点秒数）。 |
| 8    | [time.sleep(secs)](http://www.runoob.com/python/att-time-sleep.html) 推迟调用线程的运行，secs指秒数。 |
| 9    | [time.strftime(fmt[,tupletime\])](http://www.runoob.com/python/att-time-strftime.html) 接收以时间元组，并返回以可读字符串表示的当地时间，格式由fmt决定。 |
| 10   | [time.strptime(str,fmt='%a %b %d %H:%M:%S %Y')](http://www.runoob.com/python/att-time-strptime.html) 根据fmt的格式把一个时间字符串解析为时间元组。 |
| 11   | [time.time( )](http://www.runoob.com/python/att-time-time.html) 返回当前时间的时间戳（1970纪元后经过的浮点秒数）。 |
| 12   | [time.tzset()](http://www.runoob.com/python/att-time-tzset.html) 根据环境变量TZ重新初始化时间相关设置。 |

Time模块包含了以下2个非常重要的属性：

| 序号 | 属性及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | **time.timezone** 属性time.timezone是当地时区（未启动夏令时）距离格林威治的偏移秒数（>0，美洲;<=0大部分欧洲，亚洲，非洲）。 |
| 2    | **time.tzname** 属性time.tzname包含一对根据情况的不同而不同的字符串，分别是带夏令时的本地时区名称，和不带的。 |

**timedelta类**：

datetime.datetime.timedelta用于计算两个日期之间的差值，例如：

```python
import datetime
a = datetime.datetime.now()
print(a)
b = datetime.datetime.now()
print(b)
print(b-a)
#2019-01-30 20:53:57.476346
#2019-01-30 20:53:57.476346
#0:00:00
time1 = datetime.datetime(2019,1,2)
time2 = datetime.datetime(2019,1,30)
print((time2-time1).days,'days')
print((time2-time1).total_seconds())
#28 days
#2419200.0
```

#### http请求

Reference: 

1. [廖雪峰python](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001432688314740a0aed473a39f47b09c8c7274c9ab6aee000)
2. https://blog.csdn.net/hacker2025/article/details/73252600
3. https://www.jianshu.com/p/9a9dd097d282
4. https://blog.csdn.net/lecorn/article/details/82146260

​        Python3处理HTTP请求的包：http.client，urllib，urllib3，requests
其中，**http **比较 low-level，一般不直接使用；**urllib**更 high-level一点，属于标准库。urllib3跟urllib类似，拥有一些重要特性而且易于使用，但是属于扩展库，需要安装；**requests** 基于urllib3 ，也不是标准库，但是使用非常方便，个人感觉，如果非要用标准库，就使用urllib。如果没有限制，就用requests

​         **本次介绍python的内置包urllib**：

python内置了urllib包来处理http请求，主要是以下几个模块：

|        名称        |        功能         |
| :----------------: | :-----------------: |
|    urllib.error    |    处理异常模块     |
|    urllib.parse    |     解析url模块     |
|   urllib.request   |     请求url模块     |
|  urllib.response   |      响应模块       |
| urllib.robotparser | 解析 robots.txt文件 |

主要方法：

```python
######打开url或者对象
urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False, context=None)
```

 **Get请求**

```python
import urllib
# import urllib2 # python3中没有 urllib2 用urllib.request替代
# get请求
resu = urllib.request.urlopen('https://www.baidu.com/', data=None, timeout=10)
data = resu.read().decode()
#打开文件
fo = open('firsttime.txt','a+',encoding = 'utf-8') # 打开文件 这里网络数据流的编码需要和写入的文件编码一致
fo.write(data)   # 写入文件
fo.close()       # 关闭文件
```

如果get的请求携带参数需要通过url方式传值（ **不懂**）

```python
import urllib
import json

def getExpressInfo(num):
    """
    通过快递单号获取快递详情方法
    :param num: Numbers 快递单号
    :return: mixed      快递详细
    """
    # get请求
    url = 'http://www.kuaidi100.com/autonumber/autoComNum?text=' + num # get请求通过url传值
    basicInfo = urllib.request.urlopen(url, data=None, timeout=10) # python3应该可以通过检测data是否携带参数来判断是get请求还是post请求
    data = json.loads(basicInfo.read().decode()) #解析返回对象获取

    comInfo = data['auto'][0]['comCode'] # 获取快递公司信息

    # 通过公司名称和快递单号请求快速100的API
    url2 = 'http://api.kuaidi100.com/api?id=be2205c7c55b54eb&com=' + comInfo + '&nu=' + num
    result = urllib.request.urlopen(url2, data=None, timeout=10)
    expressInfo = result.read().decode()

    print(expressInfo)
    #返回快递信息
    return(expressInfo)


num = '280688688407' # 快递单号

#调用快递信息方法
getExpressInfo(num)
#{"status":"2","message":"快递公司网络异常，请稍后查询."}
###？？？？？？？？
```
**post请求**

```python
###登陆成功

Status: 200 OK
.......
Data: {"retcode":20000000,"msg":"","data":
......
icket%253DST-MzE5OTAyOTk3Mg%25253D%25253D-1548856462-yf-147B6C5AD22F5B71B13724DC9B6B327D-1","uid":"3199029972"}}
```

urllib提供的功能就是利用程序去执行各种HTTP请求。

#### Homework

   1. 请用户输入一个时间，输出选项所对应的现在时间，告诉用户这两个时间相隔的天数，小时数，分钟数和秒数。

```python
###非常蠢的办法
import datetime
t_str = input("请用户输入一个时间：")
time1 = datetime.datetime.strptime(t_str, '%Y-%m-%d %H:%M:%S')
time2 = datetime.datetime.now()
print("现在的时间:",time2)
Time_distance = (time2-time1).seconds
print("这两个时间相隔的秒数",Time_distance)
day_s = Time_distance//(24*60*60)
hour_s = (Time_distance-day_s*24*60*60)//(60*60)
minute_s = (Time_distance-day_s*24*60*60-hour_s*60*60)//60
second_s = Time_distance-day_s*24*60*60-hour_s*60*60-minute_s*60
print('您输入的时间距离现在：%s天%s小时%s分钟%s秒' %(day_s,hour_s,minute_s,second_s))
#请用户输入一个时间：2019-01-30 20:53:57
#现在的时间: 2019-01-30 23:08:22.727469
#这两个时间相隔的秒数 8065
#您输入的时间距离现在：0天2小时14分钟25秒
```

2. 请用户输入电话及邮箱，判断用户输入是否合法

```python
##抄的https://blog.csdn.net/yitingh/article/details/86708929
import re
def main():
    tel = input("请输入电话:")
    ret = re.match(r"^1[35678]\d{9}$", tel)
    if ret:
         print("匹配成功")
    else:
         print("匹配失败")
if __name__ == "__main__":
     main()
#输入邮箱
import re
email=input("请输入你的邮箱：")
if len(email) > 7:
    if re.match("^.+\\@(\\[?)[a-zA-Z0-9\\-\\.]+\\.([a-zA-Z]{2,3}|[0-9]{1,3})(\\]?)$", email) != None:
        print("你的邮箱符合要求")
    else:
         print("你输入的邮箱不正确！")
else:

    print("你输入的邮箱不正确！")
###抄袭的第二个：https://blog.csdn.net/weixin_44026955/article/details/86704079
import re


pattern1_1 = re.compile(r'^\d{11}$')
pattern1_2 = re.compile(r'(^\d{3,4})(\W|_)*(\d{7,8})$')
pattern1_3 = re.compile(r'^\d{4,6}')
while True:
    num = input('请输入您的电话号码：')
    if len(num) == 11 and re.match(pattern1_1,num):
        print('格式正确！您输入的手机号为：{}'.format(num))
        break
    elif re.match(pattern1_2,num):
        print('格式正确！您输入的固定电话为：{}'.format(num))
        break
    elif re.match(pattern1_3,num):
        print('格式正确！您输入的短号为：{}'.format(num))
        break
    else:
        print('号码输入有错，请重新输入。')
        continue


pattern2 = re.compile(r'^[A-Za-z0-9_-]+@[A-Za-z0-9_-]+\.com$')
while True: 
    mail = input('请输入您的电子邮箱地址,形如 xxxxxxx@xxx.com：')
    if re.match(pattern2,mail):
        print('格式正确！您输入的邮箱是:{}'.format(mail))
        break
    else:
        print('邮箱输入有错，请重新输入。')
        continue
```

3. 对http://www.baidu.com 进行请求，并用正则化匹配图片内容。将百度图标爬取下来保存至本地

```python
###抄得，不知道原理
###https://github.com/onlyyou1996/python/blob/master/day5.py
import re
import ssl
import urllib.request
response = urllib.request.urlopen("http://www.baidu.com")
response = response.read()
response = response.decode('utf-8') #python3
reg = r'src="(.+?\.png)"'    #正则表达式，得到图片地址
imgre = re.compile(reg)      #re.compile() 可以把正则表达式编译成一个正则表达式对象.   
imglist = re.findall(imgre,response)      #re.findall() 方法读取response 中包含 imgre（正则表达式）的数据
x = 0
for imgurl in imglist:
    imgurl='https:'+imgurl
    urllib.request.urlretrieve(imgurl,'D:\%s.png' % x)  
x += 1
###可以绘制出来，但是'D:\%s.png'最好改为'%s.png'
plt.imshow(Image.open('0.png'))
plt.show()
```

![1548862347623](C:\Users\18019\AppData\Roaming\Typora\typora-user-images\1548862347623.png)