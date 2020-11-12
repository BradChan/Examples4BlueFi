====================
4.1 数值类型及运算符
====================

让我们开始Python的学习吧，在本节中，会从基本的数值类型以及运算符出发，以几行简单的代码为大家介绍Python语言学习的基础内容。
如果有C语言的基础，相信大家能轻松理解Python语言的编程格式。

4.1.1 算术运算符
=================

对于四则运算中的+、-、×，在Python(无论是Python2.x还是Python3.x)中的计算规则与我们日常生活中的使用方法一致。

.. code-block::  C
  :linenos:

  >>> 1 + 2
  3
  >>> 1 - 2
  -1
  >>> 1 * 2
  2

其中的数字“1、2”被称为操作数，“+、-、×”被称为算术运算符。

而对于除法，则有整除和普通的除法两种，并且在Python2.x和Python3.x中，除号“/”的运算结果也不完全相同。

在Python3.x中，其除法运算满足下列的规律：

.. code-block::  C
  :linenos:

  >>> 1 / 2   
  0.5

  >>> 2 / 2
  1.0
  >>> 2.0 / 2.0
  1.0
  >>> 2.0 / 2
  1.0

  >>> 1 / 3
  0.3333333333333333

从上面的除法结果中发现了什么？无论操作数的类型是整数还是浮点数，Python3.x都会返回浮点数结果。

而在Python2.x中，进行除法“/”运算时，如果两个操作数都为整数，计算结果只保留整数部分，只有当两个操作数中至少有一个浮点数时，
才会返回浮点数类型的精确结果。

.. code-block::  C
  :linenos:

  >>> 1 / 2   
  0

  >>> 1.0 / 2
  0.5
  >>> 1.0 / 2.0
  0.5
  >>> 1 / 2.0
  0.5

  >>> 1 / 3
  0.3333333333333333

在Python2.x中可以通过导入“division” 模块来保持与Python 3.x一致的除法运算。

.. code-block::  C
  :linenos:

  >>> from __future__ import division
  >>> 1 / 2
  0.5

对于整除“//”，Python2.x与Python3.x一样，保留运算结果中的整数部分，如果操作数中有浮点数类型的数值，则计算结果为浮点数类型，小数部分为0。

.. code-block::  C
  :linenos:

  >>> 5 // 2
  2

  >>> 5.0 // 2
  2.0
  >>> 5 // 2.0
  2.0
  >>> 5.0 // 2.0
  2.0

  >>> 1.6 // 0.3
  5.0

在介绍完基本的四则运算后，还有两个相当重要的计算符号——取余“%”和幂“**”。

.. code-block::  C
  :linenos:

  >>> 5 % 2
  1
  >>> 5.0 % 2
  1.0
  
  >>> 2 ** 4
  16
  >>> 2.0 ** 4
  16.0

取余操作在编程项目中经常被使用，比如想得到x上各个位(个位、十位、百位等)的数值，可以通过对x进行取余、整除的方式获得；
又或者是定时操作，当前时长对定时时长取余，以判断结果是否为零作为判断条件。

4.1.2 布尔类型
===============

在Python中共有两种布尔类型(bool)的值，分别为True(真)和False(假)，它们的值分别等价于1和0，且能进行数值计算。
布尔类型常常充当运算符结果的返回值，如比较运算符、成员运算符等，用来判断运算结果的真假，
因此在If、For、While等语句中广泛应用了布尔类型。

.. code-block::  C
  :linenos:

  >>> True + 1
  2
  >>> True + 1.2
  2.2

  >>> False + 1
  1
  >>> False + 1.2
  1.2

在使用True和False进行数值计算时，需注意单词的大小写，否则Python解释器无法识别该常量，将发生以下的情况：

.. code-block::  C
  :linenos:

  >>> true + 1
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  NameError: name 'true' is not defined

4.1.3 比较运算符
=================

布尔类型常常被用于If、For、While等判断或循环语句中作为判断或循环中断的标志位，其中，难免伴随着数值比较的过程，
这就要用到比较运算符“<、>、==、>=、……”。

.. code-block::  C
  :linenos:

  >>> 1 > 2
  False
  >>> 1 < 2
  True
  >>> 1 == 2
  False
  >>> 1 >= 2
  False
  >>> 1 <= 2
  True

可以看到，比较运算符的返回值为布尔类型，这在If、For、While等语句中很有用处。

4.1.4 逻辑运算符
==========================

介绍完了算数运算符和比较运算符后，还有一种运算符叫做逻辑运算符——and、or、not，它用来判断操作数是否为零。

.. code-block::  C
  :linenos:

  >>> True and False
  False
  >>> True or False
  True

  >>> not True
  False
  >>> not False
  True

在使用逻辑运算符时，操作数与运算符之间需用空格隔开，否则Python解释器无法正确识别该语句。
在and判断中，两个操作数中有一个为假，则返回值为False；在or中，有一个为真，则返回真；not是将当前的值对应的布尔值取反。

逻辑运算符的操作数可以用整数或浮点数代替么？当然可以。

.. code-block::  C
  :linenos:

  >>> 1 and 2
  2
  >>> 2.0 and 1
  1
  >>> 1 and 0
  0

  >>> 1 or 2
  1
  >>> 2.0 or 1
  2.0
  >>> 1 or 0
  1

  >>> not 1
  False
  >>> not -1
  False
  >>> not 2.0
  False
  >>> not 0
  True

仔细观察程序，可以发现：

 * and：从左到右，若所有值均为真，则返回后一个值，有一个假的值，则返回第一个假的值；

 * or：从左到右，返回遇到的第一个判断为真的值；

 * not：所有的非零数值的返回值为False，而0则返回True。

显然，在逻辑运算符的判断中，Python解释器将所有的非零数值都当作是True，把0当作是False。

4.1.5 整数
=============

由于在Python3.x与在Python2.x中关于整数类型的分类有所不同，在此，对整数部分内容进行单独讲解。
在Python3.x中，无论整数数值的大小，整数只有一种类型——长整数，而在Python2.x中，整数的类型被分为int(32位整数)和long int(长整数)。
长整数不受位数的限制，可以扩展到可用内存的最大值。

.. code-block::  C
  :linenos:

  >>> 10000000000    #Python3.x版本
  10000000000 

  >>> 10000000000    #Python2.2以后的版本
  10000000000L       #长整数型数字后缀加“L”

我们可以发现，在Python2.x中以后缀L来区分整数和长整数，而在Python3.x中则取消了这种区分。这里需要注意的是，在Python2.2之前的版本中，
不支持整数与长整数的自动切换。

.. code-block::  C
  :linenos:

  >>> 10000000000    #Python2.2以前的版本不会对整数类型进行自动转换
  OverFlowError:integer literal too large

  >>> 10000000000L   #需手动在大数后添加L
  10000000000L     

4.1.6 字符串
==============

在本章的开始部分，使用了print函数来打印“Hello World!”语句。那么，对于Python解释器来说，“Hello World!”是什么类型的数据呢？字符串类型。
在Python中，我们可以使用双引号("")或单引号('')来定义字符串。

.. code-block::  C
  :linenos:

  >>> "Hello world!"
  'Hello world!'
  >>> 'Hello world!'
  'Hello world!'

其输出的结果都是一样的，那为什么需要两种定义方式呢？请看下例。

.. code-block::  C
  :linenos:

  >>> "I'm John"
  "I'm John"
  >>> 'I'm John'
    File "<stdin>", line 1
      'I'm John'
         ^
  SyntaxError: invalid syntax

Python解释器成功将第一个语句"I'm John"打印了出来，而无法打印第二个语句'I'm John'。这是因为双引号与单引号是两两对应的关系，
在第二个语句中,Python读取到'I'后,认为已读取完成一个字符串，无法识别之后的字符，从而产生错误。

相信你已经明白了为何要用两种定义方式来定义字符串。其实，除了用双引号与单引号共同使用来区分字符串的方式外，还有一种使用反斜杠“\”
来对双引号或单引号进行转义，让Python解释器理解中间的引号是字符串中的一个字符。

.. code-block::  C
  :linenos:

  >>> 'I\'m John'
  "I'm John"

尽管反斜杠不如双引号与单引号共同使用来的直观，但在同时使用了双引号和单引号的长语句中，我们不得不使用反斜杠来进行转义。

如何避免该长语句的出现呢？Python提供字符串的拼接操作。

.. code-block::  C
  :linenos:

  >>> "Hello " + "world!"
  'Hello world!'
  >>> "Hello " "world!"
  'Hello world!'

无论是使用“+”连接字符串还是连续写下两个字符串，Python都会将其自动拼接为一个字符串，甚至支持用乘法来重复打印字符串。

.. code-block::  C
  :linenos:

  >>> "Hello! " * 3
  'Hello! Hello! Hello! '

通过之前的程序，相信大家已经知道了创建字符串的基本操作，接下来介绍一些处理字符串的常用操作。

.. code-block::  C
  :linenos:

  >>> "This is a string"[0]
  'T'
  >>> "This is a string"[0:1]
  'T'
  >>> "This is a string"[0:4]
  'This'

在Python中，字符串可以被当作是一种字符列表，通过类似于列表的切片操作，单独打印字符串中被选择的字符。

在实际的编程过程中，很少会直接输出一个固定的语句，我们经常会希望让输出语句中的变量会随着程序进程的变化而变化。
在Python2.6以前版本中，使用%来实现该操作。

.. code-block::  C
  :linenos:

  >>> x = 'apple'
  >>> y = 'lemon'
  >>> "The items in the basket are %s and %s." % (x,y)
  'The items in the basket are apple and lemon.'

其中的x、y值为变量，可以根据需要任意修改，但要注意的是，x、y的数据类型要跟字符串中的%类型相对应。例如，在本例中，x、y是字符串类型的数据，
字符串中就为%s。因此，在Python2.6版本之后，新增了format函数来代替%进行格式化字符串。

.. code-block::  C
  :linenos:

  >>> x = 'apple'
  >>> y = 'lemon'
  >>> "The items in the basket are {0} and {0}.".format(x , y)
  'The items in the basket are apple and lemon.'
  >>> "The items in the basket are {1} and {0}.".format(x , y)
  'The items in the basket are lemon and apple.'
  "The items in the basket are {0} and {0}.".format(x , y)
  'The items in the basket are apple and apple.'

与%相比，format函数具有以下优点：

 * 无需关心输入参数的数据类型。
 * 输出多个参数的顺序可以随意调节。
 * 可重复输出同一参数。

除了format函数外，Python还内置有非常多的处理字符串的函数，例如，find,返回字符串中的某个单词或字符位于字符串的位置；replace，
返回被替代后的字符串等等。在此，不对这些函数做过多的介绍。

4.1.7 变量
==============

变量，是除了整数、浮点数、字符串等数据类型外，需要理解的又一个数据概念。我们能在程序的各个位置看到变量的存在，无论是输入、输出，还是中间的过程量。
变量在被使用之前，需要被赋值，可以将整数、浮点数、字符串等数据类型赋给变量。在Python中，赋值的操作并不复杂，
且无需像C语言中一样事先声明变量的数据类型。

.. code-block::  C
  :linenos:

  >>> x = 1
  >>> x
  1

  >>> x = "Hello"
  >>> x
  'Hello'

而没有事先赋值的变量，会引起Python报错。

.. code-block::  C
  :linenos:

  >>> y
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  NameError: name 'y' is not defined

在定义变量时，需注意变量的命名规则，变量只能由字母、数字和下划线组成，且不能以数字开头。

在Python中还支持链式赋值和同时为多个变量进行赋值：

.. code-block::  C
  :linenos:

  >>> a = b = c = 1
  >>> print(a , b , c)
  1 1 1

  >>> x , y , z = 1 , 2 , 3
  >>> print(x , y , z)
  1 2 3

甚至还可以不通过中间项直接进行数值交换：

.. code-block::  C
  :linenos:

  >>> x = 1
  >>> y = 2
  >>> x , y = y , x
  >>> print(x , y)
  2 1

从变量的灵活定义和使用中，可以看出Python是一门易读、简洁的编程语言。

4.1.8 身份运算符
======================

身份运算符“is”的返回值为布尔类型，在某些使用场合下，它的用法与比较运算符“==”相同，但二者之间存在本质上的区别。请看下例：

.. code-block::  C
  :linenos:

  >>> x = y = (1,2)
  >>> z = (1,2)

  >>> x == y
  True
  >>> x == z
  True

  >>> x is y
  True
  >>> x is z
  False
  >>> x is not z
  True

可以看出，“is”运算符判断的是两项是否为同一个对象，而“==”则以两项的数据是否相等为判断依据。

4.1.9 成员运算符
======================

“in”是成员运算符，通常用于判断数据是否位于序列(字符串、元组、列表)之中，返回值为布尔类型。

.. code-block::  C
  :linenos:

  >>> x = 1

  >>> x in [1,2,3,4]
  True

  >>> x in [2,3]
  False

  >>> x not in [2,3]
  True

以上示例是以列表为例，判断成员x的值(1)是否在列表内。

4.1.10 小结
==============

本节从定义和使用这两方面出发，对Python中存在的各种数值类型和运算符进行介绍。

数值类型方面介绍了布尔类型数据在判断语句中的使用、整数和长整数在Python2.x和Python3.x之间的区别、
字符串的定义及处理和变量的命名定义。

在运算符方面，我们知道了在Python中常用的有算数运算符、比较运算符、逻辑运算符、身份运算符和成员运算符，通过这几种运算符，
配合各种数值类型的数据，可以实现数字的计算、数值的比较和逻辑的真假判断。

在介绍完基本的数值类型、运算符和变量的定义后，后面4个小节将介绍Python的数据结构，数据结构可以统称为容器。
序列（如列表、元组和字符串）、映射（如字典）以及集合（set）是三类主要的容器，只有掌握了数据结构，才能对程序的结构进行优化。
