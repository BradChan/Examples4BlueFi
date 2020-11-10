==========================
4.4 字典
==========================

在介绍完数据结构中的序列(字符串、列表和元组)后，接下来要介绍的是映射这一类数据结构。在Python中，归属于映射一类的只有字典(dict)。
这个数据结构为什么被命名为字典呢？它像普通的字典一样，根据功能的不同，其内部储存的信息被分为两类，一类是词语的名称(键，key)，
另一类是词语的含义(值，value)。而映射指的就是，通过查询字典的键，就可以得到该键所对应的值。

4.4.1 字典的创建
===================

虽然使用列表或元组，同样能储存两组数据，但无法反映两组数据之间的关联。若你想建立一个具有对应关系的数据结构，
例如课程名称和成绩、姓名和联系方式等，就需要将其构造为字典的形式。下面以一个简单的例子来介绍字典的创建。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91}
  
  >>> Scores['English']
  91

该示例程序创建了一个名为“Scores”的字典，其中的各项都具有两个元素——键(key)和值(value)，且各项之间以“,”隔开，各项中的键与值以“:”隔开。
以第一项为例，该项的键为“Chinese”，值为“95”。使用“字典名[键]”就可以查询字典中该键所对应的值，这也体现出了字典是一种映射类型的数据结构。

在创建字典时，需要注意的是字典的键只能由不可更改的数据类型命名，如数字、字符串、元组等，列表由于其可被修改，因此不能作为字典的键使用。
而且字典的键是唯一的，不可重复的，类比于现实中的字典就不难理解。若字典中的键存在重复，会发生什么？

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91, 'Math': 100}
  >>> Scores
  {'Chinese': 95, 'Math': 100, 'English': 91}
  
观察该示例，可以发现如果在一个字典的建立过程中，出现了两个相同的键(在本例中是'Math')，只会保留最后定义的键的值(100)。

4.4.2 dict函数
================

与列表(list函数)和元组(tuple函数)相同，字典也拥有相应函数来将具有(键，值)这样格式的元组或列表转化为字典。

.. code-block::  C
  :linenos:

  #列表->字典
  >>> Scores = [('Chinese',95),('Math',96),('English',91)]
  >>> Scores = dict(Scores)
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91}

  #元组->字典
  >>> Scores = (('Chinese',95),('Math',96),('English',91))
  >>> Scores = dict(Scores)
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91}

除此之外，dict函数还可以通过关键字参数来创建字典。

.. code-block::  C
  :linenos:

  >>> Scores = dict(Chinese = 95, Math = 96, English = 91)
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91}

4.2.3 字典的基本操作
=====================

对于字典来说，其基本操作与序列数据结构的基本操作类似。

查询字典的长度：len(字典名)。

.. code-block::  C
  :linenos:

  >>> len(Scores)
  3

查看某项是否在字典中：某项 in 字典名 。

.. code-block::  C
  :linenos:

  >>> 'Math' in Scores
  True

  >>> 95 in Scores
  False

在该示例程序中，我们分别使用了键('Math')和值(95)，结果表明，在字典中使用in时，只会匹配字典中的键，这也进一步体现了键唯一性的重要作用。

修改字典中的值：字典名[键] = 值 。

.. code-block::  C
  :linenos:

  Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores['Math'] = 100
  >>> Scores
  {'Chinese': 95, 'Math': 100, 'English': 91}

虽然在字典中没有像列表一样的append方法来添加项，但是通过修改一个字典中不存在的键，会在字典中自动添加一个新的项来储存该键。

.. code-block::  C
  :linenos:

  Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores['Science'] = 92
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91, 'Science': 92}

删除字典中的项或字典：del 字典名[键] 或 del 字典名 。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> del Scores['Math']
  >>> Scores
  {'Chinese': 95, 'English': 91}

  >>> del Scores
  >>> Scores
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  NameError: name 'Scores' is not defined

4.2.4 字典的方法
=====================

在Python中，与列表一样，字典也拥有着自己的方法。通过调用字典的方法，可以对字典进行修改、读值、清空等操作。
其中的有些方法乍一看似乎与之前的基本操作达到的效果一样，但实际上，是存在区别的，下面会对常用的部分字典方法进行介绍。

1. keys和values
-----------------

keys方法用来读取字典内所有的键。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores.keys()
  dict_keys(['Chinese', 'Math', 'English'])

与keys方法相对应的是values方法，用来获取字典中所有的值。

.. code-block::  C
  :linenos:

  >>> Scores.values()
  dict_values([95, 96, 91])

调用keys方法和values方法都会返回一个可迭代对象，可以使用 list() 来转换为列表。

.. code-block::  C
  :linenos:

  >>> list(Scores.keys())
  ['Chinese', 'Math', 'English']

  >>> list(Scores.values())
  [95, 96, 91]

如果你使用的是Python2.x，那么keys方法和values方法会直接返回一个列表。

.. code-block::  C
  :linenos:

  >>> Scores.keys()
  ['Chinese', 'Math', 'English']

  >>> Scores.values()
  [95, 96, 91]

2. get
----------------

3. setdefault
----------------

4. clear
----------------