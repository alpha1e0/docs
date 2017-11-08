.. markdown 快速参考手册
   本文介绍markdown的常用语法

=============================
E001 - markdown 快速参考手册
=============================


:Version: v1.0
:Date: 2017-10-1
:Note: 转载请注明出处。

----

.. contents:: 目录
   :depth: 3

----


1 标题
=======

标题用 # 号开头即可，1个 # 号是一级标题，2个 ## 号是二级标题，依次类推 ::

    # 这是一级标题
    ## 这是二级标题
    ### 这是三级标题


2 引用
========

使用 > 符号表示引用 ::

    > 这是个引用 

    > 一级引用
    >> 二级引用（pandoc语法支持）


3 区块代码
===========

区块代码直接使用缩进即可实现 ::

        grep -r "test" ./*


4 段落
==========

这是段落1

这是段落2，中间隔一个空行就可以了

正常文字

斜体文字 ::

    *斜体加重1*

加粗文字 ::

    **斜体加重2**

高亮文字 ::

    `高亮文字`


5 列表
========

无序列表 ::

    * 项目1
    * 项目2
    * 项目3

有序列表 ::

    1. the first one
    2. the second one


6 代码
=======

使用如下方式指定代码格式 ::

    ```{.python .numberLines startFrom="100"}
    def foo():
        print "hello world"
    ```

反引号包含的内容表示HTML代码 ::

    `<h2>2号标题</h2>`


7 链接
========

行内链接 ::

    Google搜索: [Google一下](www.google.com)

    My email is: [email](mailto:shiyan@h3c.com)

图片链接 ::

    ![双鱼座](/aa/bb/Pictures/avatar/双鱼座.jpg "双鱼座")

参考链接 ::

    I get 10 times more traffic from [Google][1] than from
    [Yahoo][2] or [MSN][3].

    [1]: http://google.com/ "Google"
    [2]: http://search.yahoo.com/ "Yahoo Search"
    [3]: http://search.msn.com/ "MSN Search"


8 其他
========

分割线 ::

    ---