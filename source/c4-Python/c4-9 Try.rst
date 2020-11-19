==========================
4.9 异常处理语句try
==========================

在Python中，程序的运行过程被分为两种状态，正常和异常。正常状态就是程序运行没有出错的状态，在大部分情况下，程序都是处于正常状态，
当然也会有程序运行时发生意料之外的错误的情况，这被称作异常状态。当异常发生时，程序会被停止并报错，例如在4.2.2小节中，
我们试图对字符串中的字符进行修改，会得到以下的错误提示：

.. code-block::  C
  :linenos:

  >>> "1234"[0] = 2
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  TypeError: 'str' object does not support item assignment

该异常的类型为TypeError，除了该类型外，Python内置的异常类还有很多，下表中列出了部分常见的异常类型：

.. image:: ../_static/images/c4/部分异常类型.png
  :scale: 50%
  :align: center

图4-20  部分异常类型

4.9.1 捕获异常try/except
=============================

尽管异常可以提示程序中的存在的错误，但它也会导致程序停止运行。如果我们既想知道哪里发生了错误，又不想程序停止运行，该怎么办？
在Python中存在异常处理语句try/except可以用于捕获并处理异常状态，它会告诉Python当异常发生时，该执行什么程序，
下面以捕获异常类型中的TypeError为例，介绍try/except语句：

.. code-block::  C
  :linenos:

  >>> try:
  ...   "Hello World!"[0] = 1
  ... except TypeError:
  ...   print("String cannot be modified!")
  ...
  String cannot be modified!

将需要捕获异常的语句放在try语句内部的语句块中，当异常发生时，用except语句捕获该异常，并执行except语句内部的语句块。
这里需要注意的是，except后的异常名称应与try语句块产生的异常名称相同。可以看到，使用try/except语句可以对异常进行捕获，
避免了程序停止运行的情况发生。

还可以使用多个except来分别处理try语句的各个异常情况：

.. code-block::  C
  :linenos:

  >>> data = [0,'a']
  >>>
  >>> for i in data:
  ...     try:
  ...       print(1/i)
  ...     except TypeError:
  ...       print("TypeError!")
  ...     except ZeroDivisionError:
  ...       print("ZeroDivisionError!")
  ...
  ZeroDivisionError!
  TypeError!

在该程序中，定义了data列表，在列表内有两项，0和'a',依次作为第5行除法运算中的除数。显然，这两个数据无法作为除数使用，
会分别引起除数为零和数据类型错误这两个异常。

也可以将多种异常情况放在同一个except子句中，将上例程序中的两个except合为一个：

.. code-block::  C
  :linenos:

  >>> data = [0,'a']
  >>>
  >>> for i in data:
  ...     try:
  ...       print(1/i)
  ...     except (TypeError, ZeroDivisionError):
  ...       print("Error!")
  ...
  Error!
  Error!

在这里需要注意except后多个异常之间以“,”隔开，并用“( )”将它们包括在一起。

4.9.2 else
=================

在有些时候，当try内的语句块未发生异常时，我们需要执行某一语句块，与if中的else一样，在try/except后也可以添加else子句。

.. code-block::  C
  :linenos:

  >>> data = [list('Hello World!'),"Hello World!"]  #list('Hello World!') => ['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '!']

  >>> for i in data:
  ...     try:
  ...         i[0] = 2
  ...     except TypeError:
  ...         print("String cannot be modified!")
  ...     else:
  ...         print("List can be modified!")
  ...
  List can be modified!
  String cannot be modified!

在该程序中，先是新建了一个data列表，内部有两项，分别为列表list('Hello World!')和字符串"Hello World!",下面通过一个for循环依次遍历data列表，
将data列表中的两项送入try中进行检验。被检验的第一项是列表，第二项是字符串，从而得到两行输出结果。
从该程序的输出结果中可以得出，当try内的语句块产生异常时，执行except内的语句块程序，未发生异常时，执行else内的语句块程序。

4.9.3 finally
=================

最后是finally子句，它被放在try/except/else的最后，无论try中的语句是否发生异常，都会执行finally内的语句块。

.. code-block::  C
  :linenos:

  >>> data = [list('Hello World!'),"Hello World!"]
  >>>
  >>> for i in data:
  ...     try:
  ...         i[0] = 1
  ...     except TypeError:
  ...         print("String cannot be modified!")
  ...     else:
  ...         print("List can be modified!")
  ...     finally:
  ...         print("I'll always be here.")
  ...
  List can be modified!
  I'll always be here.
  String cannot be modified!
  I'll always be here.

该程序与4.9.2中的相似，只是在程序的最后加上了finally子句。
从输出结果可以看到，由于try语句执行了两次，因此finally子句内的语句块程序也被执行了两次，可以看出，
finally子句的执行与try内是否发生异常无关。

4.9.4 小结
=================

本节罗列了Python中常见的一些异常情况，并介绍了如何使用try/except/else/finally语句对异常进行捕获和处理。

下一节中将介绍如何使用函数将一个语句块抽象为一个代码，这可以减少重复编程以及提高程序的可读性。




