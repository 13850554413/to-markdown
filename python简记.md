---
title: python内建函数列表 #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: python, 笔记 #分类
tags: [python,笔记] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: python内建函数列表
---

# python内建函数列表

**数学运算类**
```python
abs(x)                      求绝对值
complex([real[, imag]]) 	创建一个复数
divmod(a, b) 	            分别取商和余数
float([x]) 	                将一个字符串或数转换为浮点数。如果无参数将返回0.0
int([x[, base]])  	        将一个字符转换为int类型，base表示进制
long([x[, base]])  	        将一个字符转换为long类型
pow(x, y[, z])  	        返回x的y次幂
range([start], stop[, step])
                            产生一个序列，默认从0开始
round(x[, n])  	            四舍五入
sum(iterable[, start])  	对集合求和
oct(x) 	                    将一个数字转化为8进制
hex(x) 	                    将整数x转换为16进制字符串
chr(i) 	                    返回整数i对应的ASCII字符
bin(x) 	                    将整数x转换为二进制字符串
bool([x]) 	                将x转换为Boolean类型k
```

**集合操作类**
```python
basestring() 	            str和unicode的超类不能直接调用，可以用作isinstance判断
format(value [, format_spec])
                            格式化输出字符串格式化的参数顺序从0开始，如“I am {0},I like {1}”
unichr(i) 	                返回给定int类型的unicode
enumerate(sequence [, start = 0])
                            返回一个可枚举的对象,该对象的next()方法将返回一个tuple
iter(o[, sentinel]) 	    生成一个对象的迭代器，第二个参数表示分隔符
max(iterable[, args...][key])
                            返回集合中的最大值
min(iterable[, args...][key])
                            返回集合中的最小值
dict([arg]) 	            创建数据字典
list([iterable])  	        将一个集合类转换为另外一个集合类
set() 	                    set对象实例化
frozenset([iterable]) 	    产生一个不可变的set
str([object])  	            转换为string类型
sorted(iterable[, cmp[, key[, reverse]]])  	队集合排序
tuple([iterable])  	        生成一个tuple类型
xrange([start], stop[, step])
                            xrange()函数与range()类似，但xrnage()并不创建列表，而是返回一
                            个xrange对象，它的行为与列表相似，但是只在需要时才计算列表值，当列
                            表很大时，这个特性能为我们节省内存
```

**逻辑判断**
```python
all(iterable)               iterable为True或迭代起为空返回True
any(iterable)               如果iterable任一元素为真返回True如果迭代器为空返回False
cmp(x, y) 	                如果x < y ,返回负数；x == y, 返回0；x > y,返回正数

**反射**

callable(object)            检查对象object是否可调用
compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1)
                            将source编译为代码或者AST对象。代码对象能够通过exec语句来执行或者eval()进行求值。
                            1、参数source：字符串或者AST（Abstract Syntax Trees）对象。
                            2、参数 filename：代码文件名称，如果不是从文件读取代码则传递一些可辨认的值。
                            3、参数model：指定编译代码的种类。可以指定为 ‘exec’,’eval’,’single’。
                            4、参数flag和dont_inherit：这两个参数暂不介绍
 dir([object])              如果有实参，它会尝试返回该对象的有效属性列表。
                            1、不带参数时，返回当前范围内的变量、方法和定义的类型列表；
                            2、带参数时，返回参数的属性、方法列表。
                            3、如果参数包含方法__dir__()，该方法将被调用。当参数为实例时。
                            4、如果参数不包含__dir__()，该方法将最大限度地收集参数信息
delattr(object, name)       删除object对象名为name的属性
eval(expression, globals=None, locals=None)
                            计算表达式expression的值
exec(object[, globals[, locals]])
                            这个函数支持动态执行 Python 代码。object 必须是字符串或者代码对象。
                            如果是字符串，那么该字符串将被解析为一系列 Python 语句并执行（除非发生语法错误）
filter(function, iterable)  构造一个序列，等价于[ item for item in iterable if function(item)]
                            1、参数function：返回值为True或False的函数，可以为None
                            2、参数iterable：序列或可迭代对象
getattr(object, name[, default])
                            获取一个类的属性
globals()                   返回表示当前全局符号表的字典
hasattr(object, name)       判断对象object是否包含名为name的特性
hash(object)                返回该对象的哈希值（如果它有的话）
id(object)                  返回对象的“标识值”
isinstance(object, classinfo)
                            判断object是否是class的实例
issubclass(class, classinfo)
                            判断是否是子类
len(s)  	                返回集合长度
locals()  	                返回当前的变量列表
map(function, iterable, ...)
                            遍历每个元素，执行function操作
memoryview(obj)  	        返回一个内存镜像类型的对象
next(iterator[, default])  	类似于iterator.next()
property([fget[, fset[, fdel[, doc]]]])
                            属性访问的包装类，设置后可以通过c.x=value等来访问setter和getter
reduce(function, iterable[, initializer])
                            合并操作，从第一个开始是前两个参数，然后是前两个的结果与第三个合并进行处理，以此类推
reload(module)  	        重新加载模块
setattr(object, name, value)
                            设置属性值
repr(object)  	            将一个对象变幻为可打印的格式
slice（） 	　              返回一个表示由range(start, stop, step)所指定索引集的slice对象
staticmethod 	            声明静态方法，是个注解
super(type[, object-or-type])
                            引用父类
type(object) 	            返回该object的类型
vars([object])  	        返回对象的变量，若无参数与dict()方法类似
bytearray([source [, encoding [, errors]]])
                            返回一个byte数组
                            1、如果source为整数，则返回一个长度为source的初始化数组；
                            2、如果source为字符串，则按照指定的encoding将字符串转换为字节序列；
                            3、如果source为可迭代类型，则元素必须为[0 ,255]中的整数；
                            4、如果source为与buffer接口一致的对象，则此对象也可以被用于初始化bytearray.
zip(*iterables)             创建一个聚合了来自每个
```

**IO操作**
```python
file(filename [, mode [, bufsize]])
                            file类型的构造函数，作用为打开一个文件，如果文件不存在且mode为写或追加时，
                            文件将被创建。添加‘b’到mode参数中，将对文件以二进制形式操作。添加‘+’到mode
                            参数中，将允许对文件同时进行读写操作
                            1、参数filename：文件名称。
                            2、参数mode：'r'（读）、'w'（写）、'a'（追加）。
                            3、参数bufsize：如果为0表示不进行缓冲，如果为1表示进行行缓冲，如果是一个大于1的数表示缓冲区的大小 。
input([prompt])  	        获取用户输入,推荐使用raw_input，因为该函数将不会捕获用户的错误输入
open(name[, mode[, buffering]])
                            打开文件与file有什么不同？推荐使用open
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
                            将objects打印到file指定的文本流，以sep分隔并在末尾加上end。
                            sep, end, file 和 flush 如果存在，它们必须以关键字参数的形式给出
raw_input([prompt])  	    设置输入，输入都是作为字符串处理
```

**其他**

help()--帮助信息

[参照python3.7.4中文官方说明](https://docs.python.org/zh-cn/3.7/library/functions.html#hash)

**__init__.py文件**

这个文件的作用是把文件夹变成一个python模块，通常是空的但是我们还可以为他增加一些其他功能．
当我们导入一个包的时候实际上是导入了它的__init__.py文件，这样就可以在里面批量导入我们所需要的模块而不用一个个导入．
```python
# __init__.py
__all__ = ['os', 'sys', 're', 'urllib']

# a.py
from package import *
```
这时就会把注册在__init__.py文件中__all__列表中的模块和包导入到当前文件中来.

**python 返回函数的理解**

返回函数的理解，返回函数返回的不是函数执行的结果而是内定函数的对象，它的作用就是
不会立即执行而是等到调用的时候才执行优点是可以延迟计算

**文件操作**

```python
with open('name','r+') as f:
    f.seek(0)   # 当有内容要读取并替换部分内容的时候可以把指针或句柄移到开头truncate()清空
    f.truncate()
```
