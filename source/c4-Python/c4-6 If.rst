==========================
4.6 条件判断语句if
==========================

在之前的编程学习的过程中，Python解释器会对我们输入的每一行代码进行逐行执行。而在学习了if语句后，
我们让Python解释器根据判断条件选择性地执行代码。

由于if语句的判断条件与布尔类型有关(在4.1.2小节中有介绍)，因此，在介绍if语句之前，需要先了解布尔类型的真、假值的判断。

在Python解释器中，认为None、“”、[ ]、{ }、()、False为假。经过之前几个小节的学习，我们知道“”、[ ]、{ }、()分别代表空字符串、
空列表、空字典和空元组，而对象None代表含义就是空，因此Python中所有的空都被认为是假，而其它的任何值都为真。

4.6.1 if语句的实现
===================

请编写以下程序：

.. code-block::  C
  :linenos:

  >>> x = 1

  >>> if x in [1,2,3]:
  ... print(x)
  File "<stdin>", line 2
      print(x)
      ^
  IndentationError: expected an indented block

在输入第4行时，Python解释器报错，这是为什么？是因为“print(x)”语句前没有缩进。在Python中，以缩进的形式来表示代码之间的层次关系，
它的使用方式与其它编程语言(C、C++等)中的大括号“{ }”的方式是一样的。因此，由于“print(x)”从属于条件判断语句“if x in [1,2,3]:”，
在“print(x)”前需要加上缩进(按空格或按Tab键)。

.. code-block::  C
  :linenos:

  >>> x = 1

  >>> if x in [1,2,3]:
  ...   print(x)
  ...
  1

输入完“print(x)”后，连按两下回车键就可以得到执行结果。

条件判断语句if的逻辑为：当条件判断为真时，执行后续缩进的代码，为假，则跳过后续缩进的代码。“if”和“:”中间的语句是判断条件，
该语句必定拥有一个布尔类型的返回值，用来返回真或假。

单纯的程序讲解也许不够生动，让我们借助BlueFi上的LED灯和按钮来对条件控制语句if进行介绍吧。

.. code-block::  C
  :linenos:

  import time
  from hiibot_bluefi.basedio import LED, Button

  button = Button()
  led = LED()

  while True:
      button.Update()
      led.white = 0

      if button.A:
          led.white = 1

在本节中，只需观察该程序中的第11行和第12行即可，其含义为，当按钮A被按下时，白色LED灯被点亮。
你可以拿起手中的BlueFi，输入该程序，观察一下控制的效果，这将帮助你理解if语句的用法。

4.6.2 else
=====================

在上一个例子中，要想控制LED灯在按钮A没被按下时处于熄灭状态，需在if的前面(或后面)加上“led.white = 0”语句。那么，
能否在一个if语句块中同时控制LED灯的亮灭呢？当然是可以的。

.. code-block::  C
  :linenos:

  while True:
      button.Update()
    
      if button.A:
          led.white = 1
      else:
          led.white = 0

“while True”语句块外的程序保持不变，还记得语句块层次的划分吗，在Python中是以缩进的形式实现的。

else语句后的“led.white = 0”语句，只有在if语句判断为假时，Python才会去执行该语句。整个“if-else”的实现效果为，当按钮A被按下时，
白色LED灯点亮；当按钮A松开后，白色LED灯熄灭。总之，判断条件为真时，执行if后的语句块；判断结果为假时，执行else后的语句块。

4.6.3 elif
=====================

当我们有多个LED灯需要用按钮来分别控制各个灯的亮灭时，显然，一个判断条件是无法满足我们的要求的。要使用多个判断条件时，需要用到elif语句，
在elif语句后可以增加判断条件。

.. code-block::  C
  :linenos:

  if button.A:
      led.white = 1
  elif button.B:
      led.red = 1
  else:
      led.white = 0
      led.red = 0

用按钮A和按钮B分别控制白色LED灯和红色LED灯的亮灭。只有当if和elif的判断条件都为假时，才会执行else语句后的语句块，在本例中，
else后的语句块是将白色和红色LED灯熄灭。在使用if-elif-else语句结构时，结构中可以没有else或elif，但一定要有if语句。

4.6.4 逻辑运算符(and、or、not)
======================================

与elif语句一个判断语句对应一个语句块的形式不同的是，使用逻辑运算符中的and、or可以实现在一个判断语句中有多个判断条件，
例如用按钮A和按钮B共同控制白色LED灯的亮灭情况。而not运算符用于将判断为假的返回值变为真，真则变为假。

1. and
----------------

使用and运算符时，只有当所有的判断条件都为真时，才会返回真。

.. code-block::  C
  :linenos:

  if button.A and button.B:
      led.white = 1
  else:
      led.white = 0

只有当按钮A和按钮B被同时按下时，白色LED灯才会被点亮。只按下按钮A或按钮B，LED灯不会被点亮。
当然，你还可以通过增加多个and来增加判断条件的个数。

2. or
----------------

or运算符与and运算符相同的点在于，它们都是用于判断条件有多个的情况。不同之处在于，and是所有的判断条件都为真时，才返回真，
而or则是只要有一个判断条件为真，就返回真。

.. code-block::  C
  :linenos:

  if button.A or button.B:
      led.white = 1
  else:
      led.white = 0

按下手中BlueFi上的按钮A和按钮B可以发现，无论是按下哪个按钮，亦或是将两个按钮同时按下，LED灯都会被点亮。与and相同，
通过添加多个or运算符，可以增加判断条件的个数。

3. not
----------------

not运算符与and和or都不一样，not运算符只作用于一个判断条件。

.. code-block::  C
  :linenos:

  if not button.A :
      led.white = 1
  else:
      led.white = 0

将其与4.6.2小节中的程序对比，可以看出，只是在if后多加了一个not，观察BlueFi的LED灯，你发现了什么？
在没有按下按钮A时，LED灯处于常亮状态，只有当按钮A被按下，LED灯才会熄灭，这与4.6.2小节中的现象正好相反。

4.6.5 小结
===================

在本节中，介绍了条件判断语句if中if-elif-else的结构规则以及逻辑运算符在if语句中的使用。了解了在存在多个判断条件时，
该如何正确使用if语句实现我们想要的逻辑。

在本节中，你或许会对程序中的“while True”语句感到困惑，不知道它的作用是什么。不用担心，在下一节中，
将会对while循环语句的使用作出说明。
