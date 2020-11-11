==========================
4.2 列表
==========================

列表、字符串和元组都属于数组结构中的序列这一类，其都具备序列这一数据结构该有的特点，编号可索引、切片、连接等，
而列表区别于字符串和元组的地方在于列表是可修改的，而字符串和元组不可修改。正是列表可被修改的这一特点，列表拥有了很多有用且不可替代的功能。


4.2.1 列表的创建
===================

在Python中，使用“[ ]”来定义列表。

.. code-block::  C
  :linenos:

  >>> li = [1, 2 ,3]  
  >>> li
  [1, 2, 3]

该示例程序创建了一个名为li的列表，其各项为1、2、3。

4.2.2 列表的基本操作
====================

与字符串的操作类似，列表同样可以完成索引、切片、查询项等的操作。

.. code-block::  C
  :linenos:

  >>> li = [1, 2 ,3] 

  #得到列表长度
  >>> len(li)
  3

  #查看1是否在列表li内
  >>> 1 in li
  True
  
  #索引，查找列表中指定位置的元素
  >>> li[0]
  1
  
  #对列表内元素进行切片获取
  >>> li[0:2]
  [1, 2]
  >>> li[0:3]
  [1, 2, 3]

  #连接其它列表
  >>> other_li = [4, 5, 6]
  >>> li + other_li
  [1, 2, 3, 4, 5, 6]

是不是与字符串的操作类似？但接下来的程序只能由列表来完成。

.. code-block::  C
  :linenos:
   
  #删除列表内元素
  >>> li = ['a','b','c']
  >>> del li[0]
  >>> li
  ['b', 'c']

  #修改列表内元素
  >>> li[0] = 2
  >>> li
  [2, 2, 3, 4]

在上述程序的第二个例子中，列表li的第一个元素被修改为了2，让我们看看字符串是否可以被修改。

.. code-block::  C
  :linenos:

  >>> "1234"[0] = 2
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  TypeError: 'str' object does not support item assignment

显然，根据Python解释器的返回信息，字符串不支持修改操作。

4.2.3 列表的方法
================

Python支持的列表操作远不止上述这些，但在介绍之前，我们需要先了解一个新的概念——方法，它与对象息息相关，
对象可以是列表、字符串或其他类型的对象。其格式为：
  对象.方法(入口参数)

方法的使用方式与函数类似，都是实现本身定义的功能。例如之前用到的print函数，用来将数据以字符串的形式打印到屏幕上；format函数，
将输入的数据格式化为字符串类型。Python解释器对于列表自带了几个方法用来对列表中的数据进行修改和查询。

或许你已经对枯燥的代码感到无趣，下面我会借助BlueFi的RGB灯珠来对列表的各个方法进行实物演示。在本节的学习中，
我们无需了解BlueFi每行代码的含义，只需观察列表的变化与RGB灯珠的对应关系即可，
至于其实现的原理会在第五章“使用Python控制BlueFi”中介绍。

在使用列表方法修改列表之前，先在BlueFi中新建一个有关RGB灯珠颜色的列表程序。打开MU编辑器，输入下面这段程序，将其命名为为code.py
并保存到CIRCUITPY磁盘中。

.. code-block::  C
  :linenos:

  import time
  from hiibot_bluefi.basedio import NeoPixel
  from hiibot_bluefi.screen import Screen

  screen = Screen()
  pixels = NeoPixel()
  pixels.brightness = 0.02

  colors = [(255,0,0), (0,255,0), (0,0,255)]

  pixels.drawPattern(colors)
  screen.brightness = 0

  while True:
      pass

我们只需关注第9行代码，它代表的意思是创建一个列表，列表名为“colors”，内部的各个数据为每颗灯珠的RGB值。
例如第一组数据(255,0,0)代表R=255、G=0、B=0，因此，第一颗RGB灯珠的颜色为红色。整体的显示效果如下图所示：

.. image:: ../_static/images/c4/红绿蓝.png
  :scale: 50%
  :align: center

图4-2  RGB灯珠——红、绿、蓝

共有3颗RGB灯珠被点亮，从左到右依次为红、绿、蓝。

1. append
-------------

“append”方法用于在列表的尾项添加新的列表项，其使用方式为：

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255)]
  colors.append((255,255,0))

其余程序保持不变，只需改变第9行处“colors”列表代码即可。其实现效果如下：

.. image:: ../_static/images/c4/红绿蓝黄.png
  :scale: 50%
  :align: center

图4-3  RGB灯珠——红、绿、蓝、黄

我们都知道红色加绿色会显示黄色，在上图中，第四颗灯珠被点亮为黄色，与我们的预期相符。

2. pop
-------------

“pop”方法用于移除列表中的项。

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255)]
  colors.pop()

.. image:: ../_static/images/c4/红绿.png
  :scale: 39%
  :align: center

图4-4 RGB灯珠——红、绿

pop方法默认移除列表的尾项，因此，第三颗灯珠(蓝)熄灭。使用pop可以实现列表的出栈操作，遵循着后进先出的原则。
显然，pop方法与append方法的操作结果相反，可以用append来实现堆栈操作。如果pop和append被同时调用会怎样？

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255)]
  colors.append(colors.pop())

.. image:: ../_static/images/c4/红绿蓝.png
  :scale: 39%
  :align: center

图4-5 RGB灯珠——红、绿、蓝

从RGB灯珠的结果中可以发现，调用pop方法会返回被移除的项。因此，append方法内的入口参数为被pop移除的项，最后的显示结果与原来一样。

3. insert
-------------

“insert”操作在列表的指定位置插入新的项。

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255)]
  colors.insert(1,(255,255,0))

.. image:: ../_static/images/c4/红黄绿蓝.png
  :scale: 39%
  :align: center

图4-6 RGB灯珠——红、黄、绿、蓝

第二颗灯珠变为黄色，绿色和蓝色灯珠依次后移。insert方法的入口参数有两个，第一个为插入的位置，以0为起始，因此本例中的“1”代表插入位置为列表的第二项；
第二个为插入的项，本例中为(255,255,0)，显示颜色为黄色。

4. extend
-------------

“extend”方法可以在列表的尾项后添加另一个列表中所有的项。

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255)]
  other_colors = [(255,255,0), (255,255,255)]
  colors.extend(other_colors)

.. image:: ../_static/images/c4/红绿蓝黄白.png
  :scale: 39%
  :align: center

图4-7 RGB灯珠——红、绿、蓝、黄、白

在other_colors列表中存放的两项为黄色和白色，使用extend方法将其添加到colors列表的尾部，RGB灯珠的颜色依次为红、绿、蓝、黄、白。
这似乎与之前的“+”连接操作相同，但实际上二者导致的结果是不同的，extend方法会修改被添加的列表的项(在本例中是colors列表)，而“+”操作不会修改任一列表的项，
它的返回值是新建的另一个列表。

5. remove
-------------

“remove”方法移除列表中第一个匹配的项。

.. code-block::  C
  :linenos:

  colors = [(255,0,0), (0,255,0), (0,0,255), (0,255,0)]
  colors.remove((0,255,0))

首先定义colors列表，其中的项依次代表红、绿、蓝、绿，接着用remove方法移除第一个绿灯，其效果如下：

.. image:: ../_static/images/c4/红蓝绿.png
  :scale: 39%
  :align: center

图4-8 RGB灯珠——红、蓝、绿

remove方法只是移除了一个绿灯，并将后续的项依次前移。与pop方法不同的是，remove方法没有返回值，只进行了对列表中项的修改。

6. 其它方法
--------------

对于修改列表的方法，还有很多，例如，reserve，将列表中的项反向存放；sort,对列表中的项进行排序；
index，查找某项在列表中第一个匹配的项的位置；等等。