.. reStructureText 快速参考手册
   本文介绍reStructureText的常用语法

============================
reStructureText 快速参考手册
============================


:Author: alpha1e0
:Version: v1.0
:Date: 2017-10-1
:Copyright: Copyright ©2017 alpha1e0. All Rights Reserved. 
:Note: 转载请注明出处。

----

.. contents:: 目录
   :depth: 3

----

.. topic:: 主题

    本文介绍 **reStructureText** 常用语法

----


1 关于
=======

本文介绍 **reStructureText** 常用语法。

使用方法，参考页面左侧 "显示源码" ，对比源码和页面显示，如下图所示。

.. image:: /static/images/snapshot.png 


2 文本处理
==========

这是 **加重** 文本

这是 *倾斜* 文本

这是 ``代码`` 文本。

这是网站链接 http://docutils.sf.net/

.. note::

    对于中文，需要在控制符号前后加空格。


2 章节、段落
============

这是一个段落，只需写文本即可。

不同段落之间需要加一个空行。

也可以使使用缩进的段落 例如：

    床前明月光

    疑是地上霜

    举头望明月

    低头思故乡

章节，见各个章节即可，推荐如下 :: 

    ===============
     Section Title
    ===============

    ---------------
     Section Title
    ---------------

    Section Title
    =============

    Section Title
    -------------

    Section Title
    ~~~~~~~~~~~~~

    Section Title
    +++++++++++++

    Section Title
    .............


3 列表
========

3.1 无序列表
------------

* 列表1
    - 子列表1
    - 子列表2
* 列表2

3.2 有序列表
------------

1. 列表1
    a. 子列表a
    b. 子列表b
2. 列表2

3.3 定义列表
-------------

what
    是什么
how
    如何去做


.. note::

    子列表需要使用4空格或TAB缩进

3.4 内容列表

如下代码：

.. code:: python
    
    def get_status(process_id, inode_id):
        process_msg = get_process_msg(process_id)
        file_msg = get_inode_msg(inode_id)

        return (process_msg, file_msg)

参数信息：

:process_id: 进程id号
:inode_id: 关联文件inode id


4 链接
=======

内嵌链接 `github <http://github.com>`_

常规链接 google搜索_

.. _google搜索: https://www.google.com

章节链接，参考 `7 特殊标记`_

交叉引用，参考 [1]_


**图片**

.. image:: /static/images/example.jpg
   :scale: 80 %
   :alt: 杭州西湖

图片支持以下属性： :: 

    :height: 100px
    :width: 200 px
    :align: left|center|right


5 代码
=======

通用的代码片段 :: 

    def hello_world():
        print "hello world"

指定编程语言的代码片段，例如python代码 

.. code:: python

    def my_function():
        "just a test"
        print 8/2


>>> print 'this is a Doctest block'
this is a Doctest block

Per-line quoting can also be used on 
unindented literal blocks:: 

> Useful for quotes from email and 
> for Haskell literate programming.

6 表格
========

**reStructureText** 支持3中方式来定义表格

1. “画图”方法定义表格
2. CSV语法定义表格
3. 列表语法定义表格

7.1 “画”出来的表格
--------------------


.. table:: 十一行程表

   ========  ===================
     日期      行程
   ========  ===================
      1        家里蹲
      2        小区一日游
      3        极地海洋馆
   ========  ===================


6.2 CSV语法定义的表格
----------------------

.. csv-table:: 宠物价格表
   :header: "宠物名称", "价格", "备注"
   :widths: 15, 10, 30

   加菲猫, 1000, 非常可爱的猫咪
   哈士奇, 800, 二逼小哈欢乐多
   兔子, 200, 可爱的小兔子

支持的其他属性: :: 
    
    :widths: integer [, integer...] or "auto"
    :align: "left", "center", or "right"

6.3 列表语法定义的表格
----------------------

.. list-table:: 杭州房价
   :widths: 15 15 30
   :header-rows: 1

   * - 地区
     - 均价
     - 描述
   * - 上城区
     - 4.5
     - 真正的市中心，教育资源丰富，但交通较差
   * - 滨江区
     - 4.0
     - 国际滨，高新区
   * - 钱江世纪新城
     - 7.0
     - 杭州未来的发展方向


7 特殊标记
==========

.. note:: 备注信息

    备注内容，换行需要4空格或tab缩进

    - The note contains all indented body elements following.
    - It includes this bullet list.


.. danger:: 警告信息

    警告正文信息


.. contents:: 目录

支持以下属性： ::

    :depth: 2

.. topic:: 文章主题

    本文介绍 **reStructureText** 常用语法


.. sidebar:: 右侧备注信息
   :subtitle: 侧边栏

   这是一个侧边栏信息

应该在侧边栏定义下方编写相应的文本信心

侧边栏是显示在侧边（一般是右侧）的内容

侧边栏的信息可以作为补充描述


8 其他
=======

交叉引用，本文内容参考 [1]_


.. [1] http://docutils.sourceforge.net/docs/user/rst/quickstart.html
.. [2] http://docutils.sourceforge.net/docs/user/rst/quickref.html
.. [3] http://www.sphinx-doc.org/en/stable/rest.html


