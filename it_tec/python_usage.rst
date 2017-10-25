.. python 常用


============
python 常用
============


:Version: v1.0
:Date: 2017-10-1
:Note: 转载请注明出处。

----

.. topic:: 主题

    本文介绍 **reStructureText** 常用语法，以 **python 2.x** 为主

----

.. contents:: 目录
   :depth: 3

----


1 字符串操作
==============

1.1 基础
----------

python 2.x 字符串类型：

- basestring
- str
- unicode

判断是否为字符串 :: 

    isinstance(some_string, basestring)

python 3.x 字符串统一使用unicode

1.2 常用方法
------------

.. list-table:: 字符串常用操作
   :widths: 15 15 
   :header-rows: 1

   * - 方法
     - 说明
   * - find(substr)
     - 查找字符串substr位置，失败返回-1
   * - find(substr)
     - 查找字符串substr位置，失败返回-1
   * - replace(old,new)
     - 将字符串中old替换为new
   * - isalnum()
     - 判断是否为字母或者数字组成的字符串
   * - isalpha()
     - 判断是否是字母组成的字符串
   * - isdigit()()
     - 判断是否为数字
   * - strip()/rstrip()/lstrip()
     - 去除字符串末尾或开头的特殊字符，如果指定参数，则去除指定的字符
   * - split(sp)
     - 使用sp分割字符串
   * - startswith(substr)/endswith(substr)
     - 判断字符串是否以substr开头或结束
   * - upper()/lower()
     - 字符串转换为全大写、全小写
   * - encode()/decode()
     - 字符串编解码


1.3 字符串、数字、字节转换
----------------------------

常用转换： ::

    str ==> int(str,base)  ==> int             # 字符串 转 数字
    int ==> hex/oct/bin(int) ==> str           # 数字 转 字符串
    int ==> chr(int) ==> bype(char)            # 数字 转 字节码（字符）
    byte(char) ==> ord(byte) ==> int           # 字节码（字符）转 数字
    str ==> binascii.hexlify/b2a_hex(str) ==>  # 字符串 转 16进制形式


unicode字节流转unicode对象 ::

    unicode字节流 ==> codecs.raw_unicode_escape_decode(unicode字节流) ==> unicode对象
    unicode对象 ==> codecs.raw_unicode_escape_encode(unicode对象)  ==> unicode字节流


1.4 编码、解码
---------------

python2.x 默认使用ascii字节流，使用str.decode后得到unicode，unicode进行encode得到字节流

python支持的一些编码方式（codecs）： ::

    gbk(cp936)、gb2312、hz(hz-gb/hz-gb-2312)、gb18030、big5、utf-8、utf-7、utf_16/le/be、utf_32/le/be

全部编码支持参考 https://docs.python.org/2/library/codecs.html

python编码检测：需要第三方库 **chardet** ，例如 ::

    encoding = chardet.detect(str)

获取当前操作系统环境编码 :: 

    locale.getdefaultlocale()
    locale.getpreferredencoding()
    sys.getfilesystemencoding()

获取终端编码方式 ::

    sys.stdin.encoding
    sys.stdout.encoding

获取python默认编码方式（python默认使用什么编码方式来解码非ascii字符，于str和unicode之间转换有关） ::

    sys.getdefaultencoding()

设置python默认编码方式，如无特殊必要不推荐使用这种方式，由于改动太大会造成一些库出现异常 ::

    reload(sys)
    sys.setdefaultencoding("utf-8")

设置python文件编码方式（python解释器如何处理.py源码，如果不指定则不允许出现非ascii字符） ::

    #-*-coding: utf-8 -*-


1.5 其他编码
------------

url编码 ::

    urllib.quote
    urllib.unquote

base64编码 ::

    base64.b64encode()
    base64.b64decode()

md5编码 ::

    hashlib.md5

html编码 ::

    cgi.escape(str,quote=None)  #quote为True时编码引号
    HTMLParser.HTMLParser().unescape(str)

crc编码 ::

    binascii.crc32


2 python format格式化输出
=========================

在python中有两种字符串格式化方法

- C风格的格式化方法，例如 "%s is a good %s" %("Tom", "student")
- format函数，例如 "{0} is a good {1}".format("tom", "student")

任何时候，优先使用 *format* 方式的字符串格式化，它功能丰富、更加清晰易懂

format函数，语法定义 ::

    replacement_field    ::=  "{" [field_name] ["!" conversion] [":" format_spec] "}"
    field_name           ::=  arg_name ("." attribute_name | "[" element_index "]")*
    arg_name             ::=  [identifier | integer]
    attribute_name       ::=  identifierelement_index     ::=  integer | index_stringindex_string      ::=  <any source character except "]"> +
    conversion           ::=  "r" | "s"
    format_spec          ::=  <described in the next section>    

    format_spec          ::=  [[fill]align][sign][#][0][width][,][.precision][type]
    fill                 ::=  <any character>
    align                ::=  "<" | ">" | "=" | "^"
    sign                 ::=  "+" | "-" | " "
    width                ::=  integerprecision   ::=  integertype        ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"


使用 **":"** , 指定代表元素需要的操作, 如 **":.3"** 小数点三位,  **":8"** 占8个字符空间等;

还可以添加特定的控制字符, 如:

- 'b' : 二进制. 将数字以2为基数进行输出.
- 'c' : 字符. 在打印之前将整数转换成对应的Unicode字符串.
- 'd' : 十进制整数. 将数字以10为基数进行输出.
- 'o' : 八进制. 将数字以8为基数进行输出.
- 'x' : 十六进制. 将数字以16为基数进行输出, 9以上的位数用小写字母.
- 'e' : 幂符号. 用科学计数法打印数字, 用'e'表示幂.
- 'g' : 一般格式. 将数值以fixed-point格式输出. 当数值特别大的时候, 用幂形式打印.
- 'n' : 数字. 当值为整数时和'd'相同, 值为浮点数时和'g'相同. 不同的是它会根据区域设置插入数字分隔符.
- '%' : 百分数. 将数值乘以100然后以fixed-point('f')格式打印, 值后面会有一个百分号.

例如： ::

    '{:<30}'.format('left aligned')                          # 左对齐
    '{:a<30}'.format('left aligned')                         # 左对齐，后面填充a
    '{:>30}'.format('right aligned')                         # 右对齐
    '{:^30}'.format('centered')                              # 中间对齐
    '{0:{base}{width}}'.format(num, base=base, width=width)

Template:

from string import Template
>>> s = Template('$who likes $what')
>>> s.substitute(who='tim', what='kung pao')'tim likes kung pao'

参考 `官方手册 <https://docs.python.org/2/library/string.html>`_



3 正则表达式
============

正则基本语法如下图： (参考 [1]_)

.. image:: /static/images/python_re.png

使用示例： ::

    import re
    pattern = re.complie(r"hello (\w+)")   # r前导符表示"原始"字符串，会忽略反斜杠特殊字符的作用
    match = pattern.match("hello world")
    print match.groups()

flags： ::

    re.I/re.IGNORECASE：忽略大小写
    re.m/re.MULTILINE：多行模式

[非]贪婪模式：
    python默认为贪婪模式，匹配最多，例如abbbc，ab*匹配结果abbb，ab*?匹配结果a

相关函数/对象（一下均为pattern.match，非re.match）：

`Match` 对象： ::

    用于存储匹配结果
    group(groupindex)：0为整个匹配的子串，groupindex默认为0，一次类推1，2，
    groups()：以元组形式返回匹配结果
    groupdict()：以字典形式返回结果

``match(string[, pos[, endpos]])`` 函数
     从字符串头开始匹配，如果头不匹配不会继续往下匹配

``search(string[, pos[, endpos]])`` 函数
    查找pattern，返回第一匹配

``findall(string[, pos[, endpos]])`` 函数
    返回所有匹配

``finditer(string[, pos[, endpos]])`` 函数
    返回所有匹配的Match迭代器

``sub(repl, string[, count = 0])``
    用repl替换string中所有匹配pattern的字符串，返回新字符串


4 反射
=======

基本操作：

- issubclass(classA, classB)
- isinstance(obj, classlist) #classlist可以是一个类也可以是类列表
- type(object) #返回对象类型，类型见types模块
- hasattr(obj, 'foo')
- getattr(obj, 'foo')
- setattr(obj, 'foo', foo)
- delattr(obj, 'foo')
- dir(obj)  #返回
- vars(obj)

python types模块定义了所有类型，参考 `这里 <https://docs.python.org/2/reference/datamodel.html#the-standard-type-hierarchy>`_

常用属性：

.. list-table:: 常用内建属性2
   :header-rows: 1

   * - xx
     - 模块
     - 类
     - 对象
     - 函数
     - 内建函数和方法
     - 方法
   * - __doc__
     - yes
     - yes
     - no
     - yes
     - yes
     - yes
   * - __name__
     - yes
     - yes
     - no
     - yes
     - yes
     - yes
   * - __dict__
     - yes
     - yes
     - yes
     - yes
     - no
     - no
   * - __file__
     - yes
     - no
     - no
     - no
     - no
     - no
   * - __module__
     - no
     - yes
     - no
     - yes
     - yes
     - yes


**inspect模块**

对象类型检查： ::

    is{module|class|function|method|builtin}(obj)
    isroutine(obj) #判断是否为函数、方法

获取信息：

``getmembers(object[, predicate])`` :
    这个方法是dir()的扩展版，它会将dir()找到的名字对应的属性一并返回，形如[(name, value), ...]。

``getmodule(object)`` :
    返回object的定义所在的模块对象。

``get{file|sourcefile}(object)`` :
    获取object的定义所在的模块的文件名|源代码文件名（如果没有则返回None）。用于内建的对象（内建模块、类、函数、方法）上时会抛出TypeError异常。

``get{source|sourcelines}(object)`` :
    获取object的定义的源代码，以字符串|字符串列表返回。代码无法访问时会抛出IOError异常。只能用于     module/class/function/method/code/frame/traceack对象。

``getargspec(func)`` :
    仅用于方法，获取方法声明的参数，返回元组，分别是(普通参数名的列表, *参数名, **参数名, 默认值元组)。如果没有值，将是空列表和3个None。如果是2.6以上版本，将返回一个命名元组(Named Tuple)，即除了索引外还可以使用属性名访问元组中的元素。 

inspect模块详见 `inspect官方手册 <https://docs.python.org/2/library/inspect.html#module-inspect>`_

5 其他
======

**动态加载模块** ::

    mod = __import__("exploit.test",globals(),locals(),['a'],-1)
    mod = importlib.import_module("exploit.test")


**单例模式** 

使用模块实现单例模式（模块只会被导入一次） ::

    from m.a import val
    print val
    foo此处调用其他模块，其他模块import了a
    print val

关于val是否被修改，类似于函数参数修改的问题，如果是简单变量，foo修改的时候相当于id变化了，因此两次val打印都一样
如果是数组或列表修改内容，则两次打印一样


**动态创建局部变量** ::

    locals()['a'] = "aa"
    print a

**查看软件包版本** ::

    from pkg_resources import require
    print require("requests")

**通过字符串调用函数或对象** ::

    globals()['foo']()   #locals vars也可以
    eval('foo')()   

    obj = globals()['class']()
    getattr(obj, 'foo')  ===> obj.foo

**长字符串** ::

    s = ("insert "
         "into "
         "table ")  ===> s = "insert into table"

**list迭代** ::

    enumerate(['a','b','c'])

**base64编解码** ::

    base64.b64encode/b64decode


**ctrl - c捕获**

方法一：使用signal注册默认处理 :: 

    def signalHandler(signum, frame):
        print "[+]: User force exit."
        exit()
    signal.signal(signal.SIGINT, signalHandler)

方法二：使用sys.excepthook，拦截KeyboardInterrupt ::

    def exceptionHook(etype, evalue, trackback):
        if isinstance(evalue, KeyboardInterrupt):
            print "ctrl-c"
            exit()
        else:
            sys.__excepthook__(etype, evalue, trackback)

    sys.excepthook = exceptionHook


**pip 使用** 

- pip install SomePackage            # latest version
- pip install SomePackage==1.0.4     # specific version
- pip install 'SomePackage>=1.0.4'     # minimum version
- pip install SomePackage-1.0-py2.py3-none-any.whl
- pip install --upgrade xxx   #升级包xxx
- pip uninstall package
- pip list
- pip show package
- pip search "query


**获取绝对路径**

- os.path.abspath
- os.path.realpath异同：

相同：两者都是将参数和os.getcwd拼接成一个绝对路径
不同：在linux中，如果绝对路径的文件是一个软连接，os.path.realpath返回软连接真实的地址


.. [1] http://www.cnblogs.com/huxi/archive/2010/07/04/1771073.html

