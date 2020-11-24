==========================
4.12 模块
==========================

随着程序内所需功能的增加，程序的长度也会越来越长，程序会变得难以维护，这时，我们就会想将其拆分成几个文件，以方便维护。
又或者是想在不同的主程序中调用同一个函数，希望使用尽可能短的代码完成这一工作。为了实现这些功能，Python中引入了模块这一概念。

在Python中，以.py为后缀的文件都可以看作是一个模块，将一个庞大的编程项目拆分为一个个的模块，不同的模块实现不同的功能，方便阅读和维护。
模块内部的函数可以被其它的模块或主程序调用，因此，在项目编程的过程中，我们可以直接在现有模块的基础上进行编程，无需从头创建模块。

4.12.1 模块的分类
===================

模块可以根据来源的不同分为三类：Python内置模块、开源模块、自定义模块。

1. Python内置模块
-------------------

在Python解释器安装时，它的内部就已存在了一些内置的模块，常用的有：

    * time：获取当前时间、延时等
    * math：数学运算，如cos、sin、atan等
    * turtle：画笔工具

在Python解释器中输入“help('modules')”可以查看Python内的所有内置模块的名称。

2. 开源模块
----------------

在Python安装时，会自动安装pip工具。输入cmd进入电脑的命令提示符窗口，使用“pip install 模块名”可以从网上下载该模块。

3. 自定义模块
----------------

自定义模块时，只需将文件名的后缀保存为.py格式，即可作为一个模块被其它模块或主程序调用。

下面使用MU编辑器创建一个文件名为contrast.py的模块：

.. code-block::  C
  :linenos:

  module_name = "contrast"

  def min(x,y):
      if x < y:
          return x
      else:
          return y
        
  def max(x,y):
      if x > y:
          return x
      else:
          return y

该模块内部有两个函数——max和min,一个全局变量“module_name”，主要的功能是获取两个传入参数中的最大值或最小值。

4.12.2 导入模块
=====================

在Python中使用import导入模块或模块中的函数，根据导入情况的不同，可以分为以下3种编写格式：

1. import 模块名
---------------------

在code.py主程序中调用contrast.py模块：

.. code-block::  C
  :linenos:

  import contrast

  print(contrast.module_name)
  print(contrast.max(1,2))
  print(contrast.min(5,1))

要想调用模块内的函数或变量，需在前面加上“模块名.”。

点击保存，观察串口窗口的输出结果：

.. code-block::  C
  :linenos:

  contrast
  2
  1

实现的效果与预期的效果一致。

2. from 模块名 import 函数或变量
---------------------------------

如果你只想调用模块内的某几个变量和函数，可以使用“from 模块名 import 函数或变量”的格式来调用它们：

.. code-block::  C
  :linenos:

  from contrast import max

  print(max(1,2))

输出结果为：

.. code-block::  C
  :linenos:

  2
  
此时，在变量或函数名前不需要再加上“模块名.”。由于本例中只导入了contrast.py模块中的max函数，因此，只能使用max函数，
min函数和module_name变量无法调用，我们可以尝试着调用一下它们：

.. code-block::  C
  :linenos:

  from contrast import max

  print(contrast.module_name)
  print(min(1,2))

输出结果为：

.. code-block::  C
  :linenos:

  Traceback (most recent call last):
      File "code.py", line 3, in <module>
  NameError: name 'module_name' is not defined

3. from 模块名 import *
---------------------------------

这种方法与第二种类似，它以*代表模块内的所有变量和函数。

.. code-block::  C
  :linenos:

  from contrast import *

  print(module_name)
  print(max(1,2))
  print(min(5,1))

模块内的所有变量和函数都可以直接调用，输出结果如下：

.. code-block::  C
  :linenos:

  contrast
  2
  1

在使用这种结构导入模块时需要注意，它不会导入“_var”格式命名的变量或函数，这一点在之前的“类中的下划线”这一小节中有提到。
除此之外，它还有一个缺陷，如果在一个主程序中导入了多个模块，且各个模块之间存在函数名或变量名重名的情况，
Python解释器调用的函数或变量或许就不是我们所希望的那个，这会引起难以排除的错误。因此，请尽量不要使用这种结构来导入模块。

4.12.3 小结
====================

本节中介绍了模块在Python编程中的重要性、模块的分类以及如何导入模块这三部分内容，正确地使用模块可以大大地减少我们在完成一个编程项目上的时间。
并且由于Python是一门开源的编程语言，因此，它具有丰富的模块可供我们选择。“人生苦短，我用Python”这句话正是对Python这门编程语言最好的解释。

到本节为止，你已经掌握了Python的基本知识，相信你肯定可以读懂后续章节中有关Python编程的绝大部分内容，
这也是为什么在介绍第五章“使用Python控制BlueFi”之前，需要先介绍第四章“Python编程语言”的原因。

在后续的章节中，将围绕BlueFi对它上面的各种输入输出元件做各种有趣的编程实验。在这个过程中，我们将逐渐掌握如何正确地使用BlueFi，
直到自己能独立开发有趣的创意项目。



