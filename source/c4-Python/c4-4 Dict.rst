==========================
4.4 字典
==========================

在介绍完数据结构中的序列(字符串、列表和元组)后，接下来要介绍的是映射这一类数据结构。在Python中，归属于映射一类的只有字典(dict)。
这个数据结构为什么被命名为字典呢？它像普通的字典一样，根据功能的不同，其内部储存的信息被分为两类，一类是词语的名称(键，key)，
另一类是词语的含义(值，value)。而映射指的就是，通过查询字典的键，就可以得到该键所对应的值。

4.4.1 字典的创建
===================

虽然使用列表或元组，同样能储存两组数据，但是它们无法反映两组数据之间的关联。若你想建立一个具有对应关系的数据结构，
例如课程名称和成绩、姓名和联系方式等，就需要将其构造为字典的形式。下面以一个简单的例子来介绍字典的创建：

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

4.4.3 字典的基本操作
=====================

对于字典来说，其基本操作与序列数据结构的基本操作类似。

查询字典的长度：len(字典名)。

.. code-block::  C
  :linenos:

  >>> len(Scores)
  3

查看某项是否在字典中：键 in 字典名 。

.. code-block::  C
  :linenos:

  >>> 'Math' in Scores
  True

  >>> 95 in Scores
  False

在该示例程序中，我们分别使用了键('Math')和值(95)，结果表明，在字典中使用in时，只会匹配字典中的键，这也进一步体现了键唯一的重要性。

修改字典中的值：字典名[键] = 值 。

.. code-block::  C
  :linenos:

  Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores['Math'] = 100
  >>> Scores
  {'Chinese': 95, 'Math': 100, 'English': 91}

虽然在字典中没有像列表的append一样的方法来添加项，但是通过修改一个字典中不存在的键，会在字典中自动添加一个新的项来储存该键。

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

4.4.4 字典的方法
=====================

在Python中，与列表一样，字典也拥有着自己的方法。通过调用字典的方法，可以对字典进行修改、读值、清空等操作。
其中的有些方法乍一看似乎与之前的基本操作达到的效果一样，但实际上，二者是存在区别的，下面会对常用的部分字典方法进行介绍。

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

通过get方法得到的返回值与格式为“字典名[键]”的使用基本类似，但get方法在访问方面不受限制，即使访问的键在该字典中不存在，
使用get方法也不会报错，导致程序停止。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  
  >>> print(Scores.get('Science'))
  None

  >>> Scores['Science']
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  KeyError: 'Science'

当访问字典中不存在的键时，get方法将返回None对象，代表返回值为空，而“字典名[键]”则会直接发生程序报错，导致程序进程中断。
除此之外，get方法还支持自定义默认值——访问不存在的键时的返回值。

.. code-block::  C
  :linenos:

  >>> Scores.get('Science',89)
  89

  >>> Scores.get('Chinese',100)
  95

显然，如果访问的键存在，get方法只会返回字典中该键所对应的值，而不会返回人为设置的默认值。
get方法的作用只是来查询字典中键所对应的值，并不会对字典产生改动(添加、修改等)。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}
  >>> Scores.get('Science',89)
  89

  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91}

3. setdefault
----------------

setdefault方法与get方法类似，在访问字典中已存在的键时，返回键所对应的值；访问字典中不存在的键时，返回自定义的默认值，若无默认值，
则返回None。但setdefault方法的本质并不是“访问”，而是“定义”，只是在返回值的表现上与get方法类似。

setdefault方法不支持覆写操作，当键的值被定义过一次后，无论该键在原字典中是否存在，该键的值无法被修改。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}

  >>> print(Scores.setdefault('Science'))
  None
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91, 'Science': None}

  >>> print(Scores.setdefault('Science',100))
  None
  >>> Scores
  {'Chinese': 95, 'Math': 96, 'English': 91, 'Science': None}

从上例中可以看出setdefault方法与get方法的另一个不同点，setdefault方法定义一个新的键“Science”后，会在原字典中插入该键，
并将第一次定义的值赋给该键。

4. clear
----------------

clear方法用于将字典中的所有项清空。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese': 95, 'Math': 96, 'English': 91}

  >>> Scores.clear()
  >>> Scores
  {}

与del相比，clear方法会保留一个空的字典，而del是将整个字典删除，可以根据需求来选择是使用clear方法还是del。

5. 其它方法
----------------

在Python中，还有一些有关字典的方法，使用dir()函数可以查看所有的字典方法。

.. code-block::  C
  :linenos:

  >>> dir(Scores)
  ['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', 
  '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', 
  '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', 
  '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 
  'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']

其中的'clear','get','keys','setdefault','values'在上文中已经介绍完毕。现对其余方法做简要介绍：
  
  * 'copy'：返回值为一个具有相同键和值的新字典。
  * 'fromkeys'：根据给定的键，构建新的字典。
  * 'items'：配合list()函数使用可返回一个列表，项为键-值。
  * 'pop'：移除给定的键及其值，返回值为被移除的键的值。 
  * 'popitem'：随机移除字典中的键-值，返回值为被移除的键和值。
  * 'update'：用一个字典去更新另一个字典，若存在相同的键，则覆写其键的值；若不存在，则添加该项。

4.4.5 小结
===============

在本节中，我们了解了字典的映射概念、字典的创建、dict函数、字典的基本操作和方法。其中最为重要的是，字典的键的唯一性与不变性，
以及键和值始终是一一对应的，同时添加、同时删除。

在下一节中将介绍另一种数据结构——集合，它就像是没有值的字典。对集合的操作与对数学中的集合类似，其概念本质上是一致的。
