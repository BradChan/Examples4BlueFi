==========================
4.5 集合
==========================

最后一种数据结构为集合(set)，集合也是一种储存数据的数据类型，且格式与列表和元组类似，各项之间以“,”分开。不同之处在于，
集合由一组无序且无重复项的不可变数据组成的，从该定义中可以得出以下三点：
 * 集合内无重复的项。
 * 无法对集合使用索引。
 * 集合内各项只能是数字、字符串、元组等不可变数据类型。

4.5.1 集合的创建
=====================

集合与字典相同，都使用“{ }”来定义，只是字典中的每一项都有两个元素(键和值)，而集合中每一项只有一个元素。集合中的项可以类比于字典中的键，
它们都由不可变的数据类型命名，且不可重复。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese', 'Math', 'English','Math'}
  >>> Scores
  {'Chinese', 'English', 'Math'}

从该示例程序中可以看出，即使在定义时定义了两个相同的项，在集合中也只会保留其中的一个。在定义集合时需要注意的是，
如果要定义一个空集合，不能使用“{ }”来定义。因为“{ }”定义的是空的字典，而不是空的集合。

.. code-block::  C
  :linenos:

  #定义的是一个空的字典
  >>> Scores = {}
  >>> Scores
  {}

  #可对它进行字典的修改操作
  >>> Scores['Math'] = 100
  >>> Scores
  {'Math': 100}

那该如何定义一个空的集合呢？使用set函数。

4.5.2 set函数
===================

在Pyhton中，只能使用set函数来创建一个空的集合。

.. code-block::  C
  :linenos:

  >>> Scores = set()
  >>> Scores
  set()

使用set函数可以将字符串、列表、元组甚至字典等数据类型转化为集合，并删除其中的重复项，

.. code-block::  C
  :linenos:

  #字符串->集合
  >>> Scores = set('Chinese')
  >>> Scores
  {'n', 'i', 'C', 's', 'h', 'e'}

  #列表->集合
  >>> Scores = set(['Chinese','Math','English','Math'])
  >>> Scores
  {'Chinese', 'Math', 'English'}

  #字典->集合
  >>> Scores = set([('Chinese',95),('Math',96),('English',91),('Math',96)])
  >>> Scores
  {('Math', 96), ('English', 91), ('Chinese', 95)}

可以看到，生成的集合中没有重复的项，且项的排列是无规律的。

4.5.3 集合的基本操作
=====================

集合的基本操作与其它数据结构类似，但由于集合的无序性，任何有关排列顺序的操作都无法对集合执行，如索引、切片等。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese', 'Math', 'English'}

  #得到集合长度
  >>> len(Scores)
  3
  
  #查看'English'是否在集合Scores
  >>> 'English' in Scores
  True

  #删除集合
  >>> del Scores
  >>> Scores
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  NameError: name 'Scores' is not defined

4.5.4 集合的方法
====================

集合中存在的方法与前几个数据结构的方法大同小异，通过它们可以对集合进行添加项、移除项、复制等操作。

1. add
-----------

add方法可以向集合中添加新的项，需要注意的是，添加的项的数据类型只能是不可变的数据类型。

.. code-block::  C
  :linenos:

  >>> Scores = {'Chinese', 'Math', 'English'}

  >>> Scores = {'Chinese', 'Math', 'English'}
  >>> Scores.add('Science')
  >>> Scores
  {'Science', 'Chinese', 'Math', 'English'}

若添加的项为列表，则会引起Python解释器报错：

.. code-block::  C
  :linenos:

  >>> Scores.add(['Science', 'Sports'])
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  TypeError: unhashable type: 'list'

2. pop、remove、discard
-------------------------

对于集合内项的删除，共有三种方法可供选择，分别是pop、remove和discard。三种方法都能删除集合内的项，但其实现方式和返回值都存在差异。

.. code-block::  C
  :linenos:

  #pop
  >>> Scores = {'Chinese', 95, 'Math', 96, 'English', 91}
  >>> Scores.pop()
  96

  #remove
  >>> Scores = {'Chinese',95, 'Math',96, 'English',91}
  >>> Scores.remove('Math')
  >>> Scores
  {96, 'Chinese', 'English', 91, 95}
  >>> Scores.remove('Science')
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  KeyError: 'Science'

  #discard
  >>> Scores = {'Chinese',95, 'Math',96, 'English',91}
  >>> Scores.discard('Math')
  >>> Scores
  {96, 'Chinese', 'English', 91, 95}
  >>> Scores.discard('Science')
  >>> Scores
  {96, 'Chinese', 'English', 91, 95}

观察程序，可以看出三种删除方式的实现效果：
 * pop：随机删除集合中的任意项，返回值为被删除的项。
 * remove：删除指定的项，当集合中不存在指定的项时，会引起Python解释器报错。
 * discard：同样是删除指定的项，但当集合中不存在指定的项时，不会引起Python解释器报错。

remove和discard的区别，就好比与在字典小节中的“字典名[键]”和get方法的区别，一个会引发报错，而另一个不会。

3. copy
----------------


4. update
--------------

5. clear
--------------

