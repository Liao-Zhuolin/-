* Python当然也有不能干的事情，比如写操作系统，这个只能用C语言写；写手机应用，只能用Swift/Objective-C（针对iPhone）和Java（针对Android）；写3D游戏，最好用C或C++。

* 因为Python是解释型语言，你的代码在执行时会一行一行地翻译成CPU能理解的机器码，这个翻译过程非常耗时，所以很慢。而C程序是运行前直接编译成CPU能执行的机器码，所以非常快。

* 第二个缺点就是代码不能加密。如果要发布你的Python程序，实际上就是发布源代码，这一点跟C语言不同，C语言不用发布源代码，只需要把编译后的机器码（也就是你在Windows上常见的xxx.exe文件）发布出去。

* 如果遇到SyntaxError，表示输入的Python代码有语法错误，最常见的一种语法错误是使用了中文标点。

* 在Python交互式模式下，可以直接输入代码，然后执行，并立刻得到结果。在命令行模式下，可以直接运行.py文件。

* 能不能像.exe文件那样直接运行.py文件呢？在Windows上是不行的，但是，在Mac和Linux上是可以的，方法是在.py文件的第一行加上一个特殊的注释：
```
#!/usr/bin/env python3
print('hello, world')
$ chmod a+x hello.py
```
* input的输入是字符串的形式，要加上强制转换才能转换为数字的形式
* 如果字符串里面有很多字符都需要转义，就需要加很多\，为了简化，Python还允许用r''表示''内部的字符串默认不转义
```
>>> print('\\\t\\')
\       \
>>> print(r'\\\t\\')
\\\t\\
```
* 空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。
* 可以把一个变量a赋值给另一个变量b，这个操作实际上是把变量b指向变量a所指向的数据，例如下面的代码：
```
a = 'ABC'
b = a
a = 'XYZ'
print(b)
```
* 对于单个字符的编码，Python提供了ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符：
```
>>> ord('A')
65>>> ord('中')
20013>>> chr(66)
'B'>>> chr(25991)
'文'
```
* 由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
* 第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；
第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。
如果你不太确定应该用什么，%s永远起作用，它会把任何数据类型转换为字符串：
```
>>> 'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True'
```
* 列表要删除指定位置的元素，用pop(i)方法，其中i是索引位置：
* 另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改
* 只有1个元素的tuple定义时必须加一个逗号,，来消除歧义：
```
>>> t = (1,)
>>> t
(1,)
```
* input()返回的数据类型是str，str不能直接和整数比较，必须先把str转换成整数。
* Python提供一个range()函数，可以生成一个整数序列，再通过list()函数可以转换为list。比如range(5)生成的序列是从0开始小于5的整数：
* 通过dict提供的get()方法，如果key不存在，可以返回None，或者自己指定的value：
```
>>> d.get('Thomas')
>>> d.get('Thomas', -1)
-1
```
* 用set（可以去除重复的元素）
* 虽然字符串有个replace()方法，也确实变出了'Abc'，但变量a最后仍是'abc'，应该怎么理解呢？
```
>>> a = 'abc'>>> a.replace('a', 'A')
'Abc'>>> a
'abc'
```
* 要始终牢记的是，a是变量，而'abc'才是字符串对象！有些时候，我们经常说，对象a的内容是'abc'，但其实是指，a本身是一个变量，它指向的对象的内容才是'abc'：
* 当我们调用a.replace('a', 'A')时，实际上调用方法replace是作用在字符串对象'abc'上的，而这个方法虽然名字叫replace，但却没有改变字符串'abc'的内容。相反，replace方法创建了一个新字符串'Abc'并返回，如果我们用变量b指向该新字符串，就容易理解了，变量a仍指向原有的字符* 串'abc'，但变量b却指向新字符串'Abc'了：
* 函数名其实就是指向一个函数对象的引用，完全可以把函数名赋给一个变量，相当于给这个函数起了一个“别名”：
```
>>> a = abs # 变量a指向abs函数
>>> a(-1) # 所以也可以通过a调用abs函数1
```
* Python的函数返回多值其实就是返回一个tuple
定义默认参数要牢记一点：默认参数必须指向不变对象！
定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个\*号。在函数内部，参数numbers接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数：
```
def calc(\*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```
* Python允许你在list或tuple前面加一个\*号，把list或tuple的元素变成可变参数传进去：
```
>>> nums = [1, 2, 3]
>>> calc(\*nums)
14
```
* 在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
* 在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。
* 使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。可以试试fact(1000)：
```
>>> fact(1000)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 4, in fact
  ...
  File "<stdin>", line 4, in fact
RuntimeError: maximum recursion depth exceeded in comparison
```
* 汉诺塔
```
def move(n,a,b,c):   #n为圆盘数，a代表初始位圆柱，b代表过渡位圆柱，c代表目标位圆柱
     if n==1:
        print(a,'-->',c)
     else:
        move(n-1,a,c,b)   #将初始位的n-1个圆盘移动到过渡位，此时初始位为a，上一级函数的过渡位b即为本级的目标位，上级的目标位c为本级的过渡位
        print(a,'-->',c)
        move(n-1,b,a,c)   #将过渡位的n-1个圆盘移动到目标位，此时初始位为b，上一级函数的目标位c即为本级的目标位，上级的初始位a为本级的过渡位
n = eval(input())
move = (n,'A','B','C')
```

* L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。
* 可以通过切片轻松取出某一段数列。比如前10个数：
>>> L[:10]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

* 后10个数：
>>> L[-10:]
[90, 91, 92, 93, 94, 95, 96, 97, 98, 99]

* 所有数，每5个取一个：
>>> L[::5]
[0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]

* 甚至什么都不写，只写[:]就可以原样复制一个list：
>>> L[:]
[0, 1, 2, 3, ..., 99]
* Python strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。
#!/usr/bin/python # -\*- coding: UTF-8 -\*- 
str = "00000003210Runoob01230000000"; 
print str.strip( '0' ); 
\# 去除首尾字符 0 
str2 = " Runoob "; 
\# 去除首尾空格 
print str2.strip();

* 默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()。
* Python内置的enumerate函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身：
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C

* 上面的for循环里，同时引用了两个变量，在Python里是很常见的，比如下面的代码：
>>> for x, y in [(1, 1), (2, 4), (3, 9)]:
...     print(x, y)
...
1 12 43 9

* 列表生成式则可以用一行语句代替循环生成上面的list：
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

* 把一个list中所有的字符串变成小写：
>>> L = ['Hello', 'World', 'IBM', 'Apple']
>>> [s.lower() for s in L]
['hello', 'world', 'ibm', 'apple']

* 在一个列表生成式中，for前面的if ... else是表达式，而for后面的if是过滤条件，不能带else。
内建的isinstance函数可以判断一个变量是不是字符串：
>>> x = 'abc'>>> y = 123>>> isinstance(x, str)
True>>> isinstance(y, str)
False

* 在Python中，这种一边循环一边计算的机制，称为生成器：generator。
第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>

* 如果要一个一个打印出来，可以通过next()函数获得generator的下一个返回值：
* 正确的方法是使用for循环，因为generator也是可迭代对象：
* 赋值同时进行，可用于交换两个变量的值
a=3
b=5
a,b=b,a

* 如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator函数，调用一个generator函数将返回一个generator： 普通函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

* 凡是可作用于for循环的对象都是Iterable类型；
凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；
* 集合数据类型如list、dict、str等是Iterable但不是Iterator，不过可以通过iter()函数获得一个Iterator对象。
Python的for循环本质上就是通过不断调用next()函数实现的
* 函数是Python内建支持的一种封装，我们通过把大段代码拆成函数，通过一层一层的函数调用，就可以把复杂任务分解成简单的任务，这种分解可以称之为面向过程的程序设计。函数就是面向过程的程序设计的基本单元。
* 函数式编程的一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！
* 函数本身也可以赋值给变量，即：变量可以指向函数。
一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数
* map()函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回。

>>> def f(x):...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]

* map()作为高阶函数，事实上它把运算规则抽象了，因此，我们不但可以计算简单的f(x)=x2，还可以计算任意复杂的函数，比如，把这个list所有数字转为字符串：
>>> list(map(str, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
['1', '2', '3', '4', '5', '6', '7', '8', '9']

* reduce把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

>>> from functools import reduce
>>> def add(x, y):...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25

* 但是如果要把序列[1, 3, 5, 7, 9]变换成整数13579，reduce就可以派上用场：
>>> from functools import reduce
>>> def fn(x, y):...     return x * 10 + y
...
>>> reduce(fn, [1, 3, 5, 7, 9])
13579

* lambda函数
list1 = [1, 2, 3, 4, 5]
list2 = map(lambda x: x**2, list1)
list(list2)

* filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。 例如，在一个list中，删掉偶数，只保留奇数，可以这么写：
def is_odd(n):
    return n % 2 == 1
list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
\# 结果: [1, 5, 9, 15]

* Python内置的sorted()函数就可以对list进行排序：
>>> sorted([36, 5, -12, 9, -21])
[-21, -12, 5, 9, 36]

sorted()函数也是一个高阶函数，它还可以接收一个key函数来实现自定义的排序，例如按绝对值大小排序：
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]

* 要进行反向排序，不必改动key函数，可以传入第三个参数reverse=True：
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
['Zoo', 'Credit', 'bob', 'about']

* 高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回
* 返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量。
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs


f1, f2, f3 = count()
>>> f1()
9
>>> f2()
9
>>> f3()
9

* 一个函数可以返回一个计算结果，也可以返回一个函数。
返回一个函数时，牢记该函数并未执行，返回函数中不要引用任何可能会变化的变量。
在Python中，对匿名函数提供了有限支持。还是以map()函数为例，计算f(x)=x2时，除了定义一个f(x)的函数外，还可以直接传入匿名函数：

>>> list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9]))
[1, 4, 9, 16, 25, 36, 49, 64, 81]

* 匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数：
>>> f = lambda x: x * x
>>> f
<function <lambda> at 0x101c6ef28>
>>> f(5)
25

* 函数对象有一个__name__属性，可以拿到函数的名字：
>>> now.__name__
'now'>>> f.__name__
'now'

* 在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）， 本质上，decorator就是一个返回函数的高阶函数
借助Python的@语法，把decorator置于函数的定义处：
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(\*args, \*\*kw)
    return wrapper

@logdef now():
    print('2015-3-25')

* 调用now()函数，不仅会运行now()函数本身，还会在运行now()函数前打印一行日志：
>>> now()
call now():
2015-3-25

* 把@log放到now()函数的定义处，相当于执行了语句： now = log(now)
* decorator可以增强函数的功能，定义起来虽然有点复杂，但使用起来非常灵活和方便。
* functools.partial就是帮助我们创建一个偏函数的，不需要我们自己定义int2()，可以直接使用下面的代码创建一个新的函数int2：
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64>>> int2('1010101')
85

* 简单总结functools.partial的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单。
* 当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单。
* 在Python中，一个.py文件就称之为一个模块（Module）
假设我们的abc和xyz这两个模块名字与其他模块冲突了，于是我们可以通过包来组织模块，避免冲突。方法是选择一个顶层包名，比如mycompany，按照如下目录存放：
mycompany
├─ _\_init_\_.py
├─ abc.py
└─ xyz.py
* 引入了包以后，只要顶层的包名不与别人冲突，那所有模块都不会与别人冲突。现在，abc.py模块的名字就变成了mycompany.abc，类似的，xyz.py的模块名变成了mycompany.xyz。
* 每一个包目录下面都会有一个__init__.py的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录，而不是一个包。__init__.py可以是空文件，也可以有Python代码，因为__init__.py本身就是一个模块，而它的模块名就是mycompany。
* 自己创建模块时要注意命名，不能和Python自带的模块名称冲突。例如，系统自带了sys模块，自己的模块就不可命名为sys.py，否则将无法导入系统自带的sys模块。
模块名不要和系统模块名冲突，最好先查看系统是否已存在该模块，检查方法是在Python交互环境执行import abc，若成功则说明系统存在此模块。
* sys模块有一个argv变量，用list存储了命令行的所有参数。argv至少有一个元素，因为第一个参数永远是该.py文件的名称，例如：运行python3 hello.py获得的sys.argv就是['hello.py']；运行python3 hello.py Michael获得的sys.argv就是['hello.py', 'Michael']。
* 当我们在命令行运行hello模块文件时，Python解释器把一个特殊变量__name__置为__main__，而如果在其他地方导入该hello模块时，if判断将失败，因此，这种if测试可以让一个模块通过命令行运行时执行一些额外的代码，最常见的就是运行测试。
* 类似__xxx__这样的变量是特殊变量，可以被直接引用，但是有特殊用途，比如上面的__author__，__name__就是特殊变量，hello模块定义的文档注释也可以用特殊变量__doc__访问，我们自己的变量一般不要用这种变量名；
* 类似_xxx和__xxx这样的函数或变量就是非公开的（private），不应该被直接引用，比如_abc，__abc等；
* Mac或Linux上有可能并存Python 3.x和Python 2.x，因此对应的pip命令是pip3。
* 默认情况下，Python解释器会搜索当前目录、所有已安装的内置模块和第三方模块，搜索路径存放在sys模块的path变量中：
>>> import sys
>>> sys.path
['','/Library/Frameworks/Python.framework/Versions/3.6/lib/python36.zip', '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6', ..., '/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages']


* 修改sys.path，添加要搜索的目录：
>>> import sys
>>> sys.path.append('/Users/michael/my_py_scripts')

* 面向对象编程——Object Oriented Programming，简称OOP，是一种程序设计思想。OOP把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。
面向过程把函数继续切分为子函数，即把大块函数通过切割成小块函数来降低系统的复杂度。
而面向对象的程序设计把计算机程序视为一组对象的集合，而每个对象都可以接收其他对象发过来的消息，并处理这些消息，计算机程序的执行就是一系列消息在各个对象之间传递。
* 在Python中，所有数据类型都可以视为对象，当然也可以自定义对象。自定义的对象数据类型就是面向对象中的类（Class）的概念。
* 如果采用面向对象的程序设计思想，我们首选思考的不是程序的执行流程，而是Student这种数据类型应该被视为一个对象，这个对象拥有name和score这两个属性（Property）。如果要打印一个学生的成绩，首先必须创建出这个学生对应的对象，然后，给对象发一个print_score消息，让对象自己把自己的数据打印出来。
class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.score = score
    def print_score(self):
        print('%s: %s' % (self.name, self.score))

* 给对象发消息实际上就是调用对象对应的关联函数，我们称之为对象的方法（Method）。
* 数据封装、继承和多态是面向对象的三大特点
* class后面紧接着是类名，即Student，类名通常是大写开头的单词，紧接着是(object)，表示该类是从哪个类继承下来的，继承的概念我们后面再讲，通常，如果没有合适的继承类，就使用object类，这是所有类最终都会继承的类。
创建实例是通过类名+()实现的
* 通过定义一个特殊的__init__方法，在创建实例的时候，就把name，score等属性绑上去：
* 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线__，在Python中，实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问，所以，我们把Student类改一改：
class Student(object):
    def __init__(self, name, score):
        self.__name = name
        self.__score = score
    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))

* 在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用__name__、__score__这样的变量名。
* 在OOP程序设计中，当我们定义一个class的时候，可以从某个现有的class继承，新的class称为子类（Subclass），而被继承的class称为基类、父类或超类（Base class、Super class）。
* 当子类和父类都存在相同的run()方法时，我们说，子类的run()覆盖了父类的run()，在代码运行的时候，总是会调用子类的run()。这样，我们就获得了继承的另一个好处：多态。
* 在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行：
* 如果要获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法：
>>> dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']

* 在Python中，如果你调用len()函数试图获取一个对象的长度，实际上，在len()函数内部，它自动去调用该对象的__len__()方法，所以，下面的代码是等价的：

>>> len('ABC')
3>>> 'ABC'.__len__()
3
* 仅仅把属性和方法列出来是不够的，配合getattr()、setattr()以及hasattr()，我们可以直接操作一个对象的状态：

>>> class MyObject(object):...
     def __init__(self):...
         self.x = 9...
     def power(self):...
         return self.x * self.x
...
>>> obj = MyObject()
>>> hasattr(obj, 'x') # 有属性'x'吗？
True
>>> obj.x
9
>>> hasattr(obj, 'y') # 有属性'y'吗？
False
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> hasattr(obj, 'y') # 有属性'y'吗？
True
>>> getattr(obj, 'y') # 获取属性'y'19>>> obj.y # 获取属性'y'19

* 实例属性属于各个实例所有，互不干扰；
* 类属性属于类所有，所有实例共享一个属性；
* 不要对实例属性和类属性使用相同的名字，否则将产生难以发现的错误。
class Student(object):
    count = 0
    def __init__(self, name):
        self.name = name
        Student.count += 1

* 为了达到限制的目的，Python允许在定义class的时候，定义一个特殊的__slots__变量，来限制该class实例能添加的属性：
* 通过多重继承，一个子类就可以同时获得多个父类的所有功能。
* @unique装饰器可以帮助我们检查保证没有重复值。
metaclass是Python中非常具有魔术性的对象，它可以改变类创建时的行为。
* finally如果有，则一定会被执行（可以没有finally语句）
凡是用print()来辅助查看的地方，都可以用断言（assert）来替代：
def foo(s):
    n = int(s)
    assert n != 0, 'n is zero!'
    return 10 / n
def main():
    foo('0')


* 不过，启动Python解释器时可以用-O参数来关闭assert：
注意：断言的开关“-O”是英文大写字母O，不是数字0。
Input Stream就是数据从外面（磁盘、网络）流进内存，Output Stream就是数据从内存流到外面去。
* 使用异步IO来编写程序性能会远远高于同步IO，但是异步IO的缺点是编程模型复杂。
* 同步和异步的区别就在于是否等待IO执行的结果。
* 如果是服务员跑过来找到你，这是回调模式，如果服务员发短信通知你，你就得不停地检查手机，这是轮询模式。总之，异步IO的复杂度远远高于同步IO。
* 每一种编程语言都会把操作系统提供的低级C接口封装起来方便使用
* 如果文件打开成功，接下来，调用read()方法可以一次读取文件的全部内容，Python把内容读到内存，用一个str对象表示：
* 最后一步是调用close()方法关闭文件。文件使用完毕后必须关闭，因为文件对象会占用操作系统的资源，并且操作系统同一时间能打开的文件数量也是有限的：
* Python引入了with语句来自动帮我们调用close()方法：
with open('/path/to/file', 'r') as f:
    print(f.read())

* 调用readline()可以每次读取一行内容，调用readlines()一次读取所有内容并按行返回list。
* 要读取二进制文件，比如图片、视频等等，用'rb'模式打开文件即可：
>>> f = open('/Users/michael/gbk.txt', 'r', encoding='gbk')
>>> f.read()
'测试'



* 写文件和读文件是一样的，唯一区别是调用open()函数时，传入标识符'w'或者'wb'表示写文本文件或写二进制文件：
* StringIO顾名思义就是在内存中读写str。

>>> from io import StringIO
>>> f = StringIO()
>>> f.write('hello')
5>>> f.write(' ')
1>>> f.write('world!')
6>>> print(f.getvalue())
hello world!



* getvalue()方法用于获得写入后的str。
* StringIO和BytesIO是在内存中操作str和bytes的方法，使得和读写文件具有一致的接口。
* Python内置的os模块也可以直接调用操作系统提供的接口函数。
* 如果是posix，说明系统是Linux、Unix或Mac OS X，如果是nt，就是Windows系统。

>>> import os
>>> os.name # 操作系统类型'posix'



* 在操作系统中定义的环境变量，全部保存在os.environ这个变量中，可以直接查看：

>>> os.environ
environ({'VERSIONER_PYTHON_PREFER_32_BIT': 'no', 'TERM_PROGRAM_VERSION': '326', 'LOGNAME': 'michael', 'USER': 'michael', 'PATH': '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/opt/X11/bin:/usr/local/mysql/bin', ...})



* 要获取某个环境变量的值，可以调用os.environ.get('key')：
>>> os.environ.get('PATH')
'/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/opt/X11/bin:/usr/local/mysql/bin'>>> os.environ.get('x', 'default')
'default'
\# 查看当前目录的绝对路径:>>> os.path.abspath('.')
'/Users/michael'# 在某个目录下创建一个新目录，首先把新目录的完整路径表示出来:>>> os.path.join('/Users/michael', 'testdir')
'/Users/michael/testdir'# 然后创建一个目录:>>> os.mkdir('/Users/michael/testdir')
\# 删掉一个目录:>>> os.rmdir('/Users/michael/testdir')

* 文件操作使用下面的函数。假定当前目录下有一个test.txt文件：

\# 对文件重命名:>>> os.rename('test.txt', 'test.py')
\# 删掉文件:>>> os.remove('test.py')

* 列出当前目录下的所有目录，只需要一行代码：
>>> [x for x in os.listdir('.') if os.path.isdir(x)]
['.lein', '.local', '.m2', '.npm', '.ssh', '.Trash', '.vim', 'Applications', 'Desktop', ...]
>>> [x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1]=='.py']
['apis.py', 'config.py', 'models.py', 'pymonitor.py', 'test_db.py', 'urls.py', 'wsgiapp.py']



* Python的os模块封装了操作系统的目录和文件操作，要注意这些函数有的在os模块中，有的在os.path模块中。
* 把变量从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling， 序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上。
* Python提供了pickle模块来实现序列化。
* 如果我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便。
* 真正的并行执行多任务只能在多核CPU上实现，但是，由于任务数量远远多于CPU的核心数量，所以，操作系统也会自动把很多任务轮流调度到每个核心上执行。
Python既支持多进程，又支持多线程
* 线程是最小的执行单元，而进程由至少一个线程组成。如何调度进程和线程，完全由操作系统决定，程序自己不能决定什么时候执行，执行多长时间。
* 多进程和多线程的程序涉及到同步、数据共享的问题，编写起来更复杂。
* 普通的函数调用，调用一次，返回一次，但是fork()调用一次，返回两次，因为操作系统自动把当前进程（称为父进程）复制了一份（称为子进程），然后，分别在父进程和子进程内返回。
* 子进程永远返回0，而父进程返回子进程的ID。
import os
print('Process (%s) start...' % os.getpid())
\# Only works on Unix/Linux/Mac:
pid = os.fork()
if pid == 0:
    print('I am child process (%s) and my parent is %s.' % (os.getpid(), os.getppid()))
else:
    print('I (%s) just created a child process (%s).' % (os.getpid(), pid))



* 创建子进程时，只需要传入一个执行函数和函数的参数，创建一个Process实例，用start()方法启动，这样创建进程比fork()还要简单。
* join()方法可以等待子进程结束后再继续往下运行，通常用于进程间的同步。
from multiprocessing import Process
import os


\# 子进程要执行的代码
def run_proc(name):
    print('Run child process %s (%s)...' % (name, os.getpid()))


if __name__=='__main__':
    print('Parent process %s.' % os.getpid())
    p = Process(target=run_proc, args=('test',))
    print('Child process will start.')
    p.start()
    p.join()
    print('Child process end.')

* 如果要启动大量的子进程，可以用进程池的方式批量创建子进程：
* Process之间肯定是需要通信的，操作系统提供了很多机制来实现进程间的通信。Python的multiprocessing模块包装了底层的机制，提供了Queue、Pipes等多种方式来交换数据。
* 进程是由若干线程组成的，一个进程至少有一个线程。
启动一个线程就是把一个函数传入并创建Thread实例，然后调用start()开始执行：
* 由于任何进程默认就会启动一个线程，我们把该线程称为主线程，主线程又可以启动新的线程，
* 多线程和多进程最大的不同在于，多进程中，同一个变量，各自有一份拷贝存在于每个进程中，互不影响，而多线程中，所有变量都由所有线程共享，所以，任何一个变量都可以被任何一个线程修改，因此，线程之间共享数据最大的危险在于多个线程同时改一个变量，把内容给改乱了。
多线程编程，模型复杂，容易发生冲突，必须用锁加以隔离，同时，又要小心死锁的发生。
* 一个ThreadLocal变量虽然是全局变量，但每个线程都只能读写自己线程的独立副本，互不干扰。ThreadLocal解决了参数在一个线程中各个函数之间互相传递的问题。
多线程模式致命的缺点就是任何一个线程挂掉都可能直接造成整个进程崩溃，因为所有线程共享进程的内存。
* 假设你不幸正在准备中考，每天晚上需要做语文、数学、英语、物理、化学这5科的作业，每项作业耗时1小时。 如果你先花1小时做语文作业，做完了，再花1小时做数学作业，这样，依次全部做完，一共花5小时，这种方式称为单任务模型，或者批处理任务模型。 假设你打算切换到多任务模型，可以先做1分钟语文，再切换到数学作业，做1分钟，再切换到英语，以此类推，只要切换速度足够快，这种方式就和单核CPU执行多任务是一样的了，以幼儿园小朋友的眼光来看，你就正在同时写5科作业。 但是，切换作业是有代价的，比如从语文切到数学，要先收拾桌子上的语文书本、钢笔（这叫保存现场），然后，打开数学课本、找出圆规直尺（这叫准备新环境），才能开始做数学作业。操作系统在切换进程或者线程时也是一样的，它需要先保存当前执行的现场环境（CPU寄存器状态、内存页等），然后，把新任务的执行环境准备好（恢复上次的寄存器状态，切换内存页等），才能开始执行。这个切换过程虽然很快，但是也需要耗费时间。如果有几千个任务同时进行，操作系统可能就主要忙着切换任务，根本没有多少时间去执行任务了，这种情况最常见的就是硬盘狂响，点窗口无反应，系统处于假死状态。
* 所以，多任务一旦多到一个限度，就会消耗掉系统所有的资源，结果效率急剧下降，所有任务都做不好。
* Python这样的脚本语言运行效率很低，完全不适合计算密集型任务。对于计算密集型任务，最好用C语言编写。
* 正则表达式是一种用来匹配字符串的强有力的武器。它的设计思想是用一种描述性的语言来给字符串定义一个规则，凡是符合规则的字符串，我们就认为它“匹配”了，否则，该字符串就是不合法的。
* 要匹配变长的字符，在正则表达式中，用\*表示任意个字符（包括0个），用+表示至少一个字符，用?表示0个或1个字符，用{n}表示n个字符，用{n,m}表示n-m个字符：
由于'-'是特殊字符，在正则表达式中，要用'\'转义
[0-9a-zA-Z\_]可以匹配一个数字、字母或者下划线；
[0-9a-zA-Z\_]+可以匹配至少由一个数字、字母或者下划线组成的字符串，比如'a100'，'0_Z'，'Py3000'等等；
* [a-zA-Z\_][0-9a-zA-Z\_]\*可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是Python合法的变量；
* [a-zA-Z\_][0-9a-zA-Z\_]{0, 19}更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。
A|B可以匹配A或B，所以(P|p)ython可以匹配'Python'或者'python'。
* ^表示行的开头，^\d表示必须以数字开头。
* $表示行的结束，\d$表示必须以数字结束。
* 可能注意到了，py也可以匹配'python'，但是加上^py$就变成了整行匹配，就只能匹配'py'了。
* Python提供re模块，包含所有正则表达式的功能。由于Python的字符串本身也用\转义，所以要特别注意：
* 使用Python的r前缀，就不用考虑转义的问题了：
s = r'ABC\-001' 
\# Python的字符串# 对应的正则表达式字符串不变：
\# 'ABC\-001'
>>> import re
>>> re.match(r'^\d{3}\-\d{3,8}$', '010-12345')
<_sre.SRE_Match object; span=(0, 9), match='010-12345'>
>>> re.match(r'^\d{3}\-\d{3,8}$', '010 12345')
>>>

* atch()方法判断是否匹配，如果匹配成功，返回一个Match对象，否则返回None。常见的判断方法就是：
test = '用户输入的字符串'if re.match(r'正则表达式', test):
    print('ok')
else:
    print('failed')

* 正常的切分代码 无法识别连续的空格，用正则表达式试试：
>>> re.split(r'\s+', 'a b   c')
['a', 'b', 'c']
>>> re.split(r'[\s\,\;]+', 'a,b;; c  d')
['a', 'b', 'c', 'd']

* 注意到group(0)永远是与整个正则表达式相匹配的字符串，group(1)、group(2)……表示第1、2、……个子串。
>>> m = re.match(r'^(\d{3})-(\d{3,8})$', '010-12345')
>>> m
<_sre.SRE_Match object; span=(0, 9), match='010-12345'>
>>> m.group(0)
'010-12345'>>> m.group(1)
'010'>>> m.group(2)
'12345'

* 最后需要特别指出的是，正则匹配默认是贪婪匹配，也就是匹配尽可能多的字符。举例如下，匹配出数字后面的0：
>>> re.match(r'^(\d+)(0*)$', '102300').groups()
('102300', '')

* 由于\d+采用贪婪匹配，直接把后面的0全部匹配了，结果0*只能匹配空字符串了。
必须让\d+采用非贪婪匹配（也就是尽可能少匹配），才能把后面的0匹配出来，加个?就可以让\d+采用非贪婪匹配：
>>> re.match(r'^(\d+?)(0*)$', '102300').groups()
('1023', '00')


* 当我们在Python中使用正则表达式时，re模块内部会干两件事情：
* 编译正则表达式，如果正则表达式的字符串本身不合法，会报错；
* 用编译后的正则表达式去匹配字符串。
* 如果一个正则表达式要重复使用几千次，出于效率的考虑，我们可以预编译该正则表达式，接下来重复使用时就不需要编译这个步骤了，直接匹配：
>>> import re
\# 编译:>>> re_telephone = re.compile(r'^(\d{3})-(\d{3,8})$')
\# 使用：>>> re_telephone.match('010-12345').groups()
('010', '12345')
>>> re_telephone.match('010-8086').groups()
('010', '8086')


* Python之所以自称“batteries included”，就是因为内置了许多非常有用的模块，无需额外安装和配置，即可直接使用。
* datetime表示的时间需要时区信息才能确定一个特定的时间，否则只能视为本地时间。
* 如果要存储datetime，最佳方法是将其转换为timestamp再存储，因为timestamp的值与时区完全无关。
* namedtuple是一个函数，它用来创建一个自定义的tuple对象，并且规定了tuple元素的个数，并可以用属性而不是索引来引用tuple的某个元素。
* deque是为了高效实现插入和删除操作的双向列表，适合用于队列和栈：
>>> from collections import deque
>>> q = deque(['a', 'b', 'c'])
>>> q.append('x')
>>> q.appendleft('y')
>>> q
deque(['y', 'a', 'b', 'c', 'x'])

* collections模块提供了一些有用的集合类，可以根据需要选用。
* Base64是一种任意二进制到文本字符串的编码方法，常用于在URL、Cookie、网页中传输少量二进制数据。
摘要算法又称哈希算法、散列算法。它通过一个函数，把任意长度的数据转换为一个长度固定的数据串（通常用16进制的字符串表示）。
* 摘要算法在很多地方都有广泛的应用。要注意摘要算法不是加密算法，不能用于加密（因为无法通过摘要反推明文），只能用于防篡改，但是它的单向计算特性决定了可以在不存储明文口令的情况下验证用户口令。
* Python的内建模块itertools提供了非常有用的用于操作迭代对象的函数。
* 基本上，所有的第三方模块都会在PyPI - the Python Package Index上注册，只要找到对应的模块名字，即可用pip安装。
* PIL提供了操作图像的强大功能，可以通过简单的代码完成复杂的图像处理。
* PIL的ImageDraw提供了一系列绘图方法，让我们可以直接绘图。比如要生成字母验证码图片：
from PIL import Image, ImageDraw, ImageFont, ImageFilter
import random
\# 随机字母:def rndChar():
return chr(random.randint(65, 90))
\# 随机颜色1:def rndColor():
return (random.randint(64, 255), random.randint(64, 255), random.randint(64, 255))
\# 随机颜色2:def rndColor2():
return (random.randint(32, 127), random.randint(32, 127), random.randint(32, 127))
\# 240 x 60:
width = 60 * 4
height = 60
image = Image.new('RGB', (width, height), (255, 255, 255))
\# 创建Font对象:
font = ImageFont.truetype('Arial.ttf', 36)
\# 创建Draw对象:
draw = ImageDraw.Draw(image)
\# 填充每个像素:for x in range(width):
for y in range(height):
draw.point((x, y), fill=rndColor())
\# 输出文字:for t in range(4):
draw.text((60 * t + 10, 10), rndChar(), font=font, fill=rndColor2())
\# 模糊:
image = image.filter(ImageFilter.BLUR)
image.save('code.jpg', 'jpeg')

* 用requests获取URL资源
* 当我们拿到一个bytes时，就可以对其检测编码。用chardet检测编码，只需要一行代码：
>>> chardet.detect(b'Hello, world!')
{'encoding': 'ascii', 'confidence': 1.0, 'language': ''}

* 检测出的编码是ascii，注意到还有个confidence字段，表示检测的概率是1.0（即100%）。
* 我们来试试检测GBK编码的中文：
>>> data = '离离原上草，一岁一枯荣'.encode('gbk')
>>> chardet.detect(data)
{'encoding': 'GB2312', 'confidence': 0.7407407407407407, 'language': 'Chinese'}

* psutil = process and system utilities 它不仅可以通过一两行代码实现系统监控，还可以跨平台使用，支持Linux／UNIX／OSX／Windows等，是系统管理员和运维小伙伴不可或缺的必备模块。
* virtualenv为应用提供了隔离的Python运行环境，解决了不同应用间多版本的冲突问题。
* Python内置的Tkinter可以满足基本的GUI程序的要求，如果是非常复杂的GUI程序，建议用操作系统原生支持的语言和库来编写。
* 绘图完成后，记得调用done()函数，让窗口进入消息循环，等待被关闭。否则，由于Python进程会立刻结束，将导致窗口被立刻关闭。
* 因为互联网协议包含了上百种协议标准，但是最重要的两个协议是TCP和IP协议，所以，大家把互联网的协议简称TCP/IP协议。
* IP地址实际上是一个32位整数（称为IPv4），以字符串表示的IP地址如192.168.0.1实际上是把32位整数按8位分组后的数字表示，目的是便于阅读。
* IPv6地址实际上是一个128位整数，它是目前使用的IPv4的升级版，以字符串表示类似于2001:0db8:85a3:0042:1000:8a2e:0370:7334。
* 端口号小于1024的是Internet标准服务的端口，端口号大于1024的，可以任意使用。
* 用TCP协议进行Socket编程在Python中十分简单，对于客户端，要主动连接服务器的IP和指定端口，对于服务器，要首先监听指定端口，然后，对每一个新的连接，创建一个线程或进程来处理。通常，服务器程序会无限运行下去。
同一个端口，被一个Socket绑定了以后，就不能被别的Socket绑定了。
* TCP是建立可靠连接，并且通信双方都可以以流的形式发送数据。相对TCP，UDP则是面向无连接的协议。
使用UDP协议时，不需要建立连接，只需要知道对方的IP地址和端口号，就可以直接发数据包。但是，能不能到达就不知道了。
* UDP的使用与TCP类似，但是不需要建立连接。此外，服务器绑定UDP端口和TCP端口互不冲突，也就是说，UDP的9999端口与TCP的9999端口可以各自绑定。
发邮件时，MUA和MTA使用的协议就是SMTP：Simple Mail Transfer Protocol，后面的MTA到另一个MTA也是用SMTP协议。
* 收邮件时，MUA和MDA使用的协议有两种：POP：Post Office Protocol，目前版本是3，俗称POP3；IMAP：Internet Message Access Protocol，目前版本是4，优点是不但能取邮件，还可以直接操作MDA上存储的邮件，比如从收件箱移到垃圾箱，等等。
* Python对SMTP支持有smtplib和email两个模块，email负责构造邮件，smtplib负责发送邮件。
所以，收取邮件分两步：
第一步：用poplib把邮件的原始文本下载到本地；
第二部：用email解析原始文本，还原为邮件对象。
* 用Python的poplib模块收取邮件分两步：第一步是用POP3协议把邮件获取到本地，第二步是用email模块把原始邮件解析为Message对象，然后，用适当的形式把邮件内容展示给用户即可。
* MySQL是Web世界中使用最广泛的数据库服务器。SQLite的特点是轻量级、可嵌入，但不能承受高并发访问，适合桌面和移动应用。而MySQL是为服务器端设计的数据库，能承受高并发访问，同时占用的内存也远远大于SQLite。
* 软件开始主要运行在桌面上，而数据库这样的软件运行在服务器端，这种Client/Server模式简称CS架构。
随着互联网的兴起，人们发现，CS架构不适合Web，最大的原因是Web应用程序的修改和升级非常迅速，而CS架构需要每个客户端逐个升级桌面App，因此，Browser/Server模式开始流行，简称BS架构。
* Web开发也经历了好几个阶段：
* 静态Web页面：由文本编辑器直接编辑并生成静态的HTML页面，如果要修改Web页面的内容，就需要再次编辑HTML源文件，早期的互联网Web页面就是静态的；
* CGI：由于静态Web页面无法与用户交互，比如用户填写了一个注册表单，静态Web页面就无法处理。要处理用户发送的动态数据，出现了Common Gateway Interface，简称CGI，用C/C++编写。
* ASP/JSP/PHP：由于Web应用特点是修改频繁，用C/C++这样的低级语言非常不适合Web开发，而脚本语言由于开发效率高，与HTML结合紧密，因此，迅速取代了CGI模式。ASP是微软推出的用VBScript脚本编程的Web开发技术，而JSP用Java来编写脚本，PHP本身则是开源的脚本语言。
* MVC：为了解决直接用脚本语言嵌入HTML导致的可维护性差的问题，Web应用也引入了Model-View-Controller的模式，来简化Web开发。ASP发展为ASP.Net，JSP和PHP也有一大堆MVC框架。
* Python的诞生历史比Web还要早，由于Python是一种解释型的脚本语言，开发效率高，所以非常适合用来做Web开发。
* 在Web应用中，服务器把网页传给浏览器，实际上就是把网页的HTML代码发送给浏览器，让浏览器显示出来。而浏览器和服务器之间的传输协议是HTTP，所以：
* HTML是一种用来定义网页的文本，会HTML，就可以编写网页；
* HTTP是在网络上传输HTML的协议，用于浏览器和服务器的通信。
* 如果要学习Web开发，首先要对HTML、CSS和JavaScript作一定的了解。HTML定义了页面的内容，CSS来控制页面元素的样式，而JavaScript负责页面的交互逻辑。
* 无论多么复杂的Web应用程序，入口都是一个WSGI处理函数。HTTP请求的所有输入信息都可以通过environ获得，HTTP响应的输出都可以通过start_response()加上函数返回值作为Body。
* 同步IO模型的代码是无法实现异步IO模型的。
* 异步IO模型需要一个消息循环，在消息循环中，主线程不断地重复“读取消息-处理消息”这一过程：
loop = get_event_loop()
while True:
event = loop.get_event()
process_event(event)


* 协程，又称微线程，纤程。英文名Coroutine。
最大的优势就是协程极高的执行效率。因为子程序切换不是线程切换，而是由程序自身控制，因此，没有线程切换的开销，和多线程比，线程数量越多，协程的性能优势就越明显。
* Python对协程的支持是通过generator实现的。
* asyncio是Python 3.4版本引入的标准库，直接内置了对异步IO的支持。

