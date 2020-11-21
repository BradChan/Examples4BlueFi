==========================
4.11 类
==========================

类，是Python中一个重要的概念，它集合了前面所提到的数据类型(数字、字符串、列表、字典等)和函数，它是一个比函数更大、更抽象的数据容器。

Python是一门面向对象的编程语言，在Python中，一切都是对象。对象的特点是什么呢？身份、类型和值。

.. code-block::  C
  :linenos:

  >>> x = 1

  #值
  >>> x
  1

  #身份
  >>> id(x)
  140735913531040

  #类型
  >>> type(x)
  <class 'int'>

使用Python的内置函数id()和type()可以得到对象的身份和类型。

类与对象的联系又是什么呢？类是从客观世界中的事物抽象出来的一些特点，而对象是类实例化后的实体，即客观世界中符合类描述的实物。
通俗的讲就是，如果有一个东西，看起来像个鸭子，走起路来像个鸭子，叫起来也像个鸭子，那么它一定就是个鸭子！
前半句可以看作是类，它是在对鸭子这个对象进行描写，后半句是类的实例化，即对象，也就是鸭子。

4.11.1 类的定义
======================

与定义函数相同，类的定义也具备其特定的格式，它以class语句开头：

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         return self.lesson
  ...     def get_score(self):
  ...         return self.score

Report是该类的名称，该类中储存了课程的名称(lesson)和成绩(score)，并提供接口函数让我们去访问这两个数据。

类的定义中包含了3个主要内容——对象、属性和方法。

在类中用self来代表对象，而对象的属性值在“__init__”方法中定义，“__init__”方法是Python内置的类方法，格式固定，
在本例中定义的两个属性值为lesson和score。最后是方法，在之前的学习中，我们已经接触过了列表、元组、字典等数据结构的方法，
在该类中，我们自定义了两个方法，get_lesson()和get_score()分别用来获取对象的两个属性值。下面看看具体的实例化过程：

.. code-block::  C
  :linenos:

  >>> scores = Report("Chinese",91)

第一行中，我们定义了一个名为“scores”的对象，并将两个实参"Chinese"和91分别传给方法“__init__”中的lesson和score，
“__init__”方法会在类被实例化时首先被调用，无需手动调用。接着试试调用类内的方法：

.. code-block::  C
  :linenos:

  >>> scores.get_lesson()
  'Chinese'

  >>> scores.get_score()
  91

与之前使用方法的只是一样，用“.”将对象名称与方法隔开。类的方法是用函数定义而成，其用法与普通的函数基本上没有区别，
只是它可以将self作为形参，从而可以调用“__init__”方法中对象的各个属性值，在本例中就调用了self.lesson和self.score这两个属性值。

4.11.2 类中的下划线“_”
===========================

或许你会觉得“__init__”方法的定义格式很奇怪，首先，这是Python内置的一种特殊方法，其次，
在类中使用下划线“_”定义属性名和方法(函数)名时具有特殊的意义。

1. __var__
----------------

这种格式与“__init__”相同，前后都有两个下划线，它通常代表Python内部自带的特殊方法，除了“__init__”之外，还有“__del__”、
“__len__”、“__repr__”等等，它们都具有特定的使用方式，因此，在自定义方法名时，请不要随意将其定义为“__var__”的格式，
有可能会与Python内置的特殊方法重名。

2. _var
---------------

在命名前加一个下划线是告诉使用者，该属性或方法只在该类中使用，这只是一种约定俗成的书写格式，并不会强制禁止我们去调用它。

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     i = 0
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self._score = score

  >>> scores.lesson
  'Chinese'
  
  >>> scores._score
  91

但在使用“import 模块名 from *”从其它模块中导入所有属性和方法时，Python不会导入前面带有下划线的属性和方法，
有关模块导入的内容会在下一节中介绍。

.. code-block::  C
  :linenos:

  >>> scores._score
  NameError: "name '_score' is not defined"

但在使用“import 模块名”时，不会引发报错。

.. code-block::  C
  :linenos:

  >>> scores._score
  91

3. __var
---------------

在命名前加两个下划线造成的结果与之前的约定俗成不同，会使得Python对该名称进行重命名。既防止了类外的程序对它的误调用，
又避免了与子类中的命名冲突。

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.__score = score
  ...     def get_lesson(self):
  ...         return self.lesson
  ...     def get_score(self):
  ...         return self.__score

在该程序中定义了一个属性值“__score”,我们先试着在外部程序中调用一下他：

.. code-block::  C
  :linenos:

  >>> scores.__score
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  AttributeError: 'Report' object has no attribute '__score'

提示报错，在“Report”类中找不到“__score”属性值。可以看出，该属性的名称已经被Python重命名了，我们可以用dir函数来查看它的名称：

.. code-block::  C
  :linenos:

  >>> dir(scores)
  ['_Report__score', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', 
  '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', 
  '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 
  '__weakref__', 'get_lesson', 'get_score', 'lesson']

仔细观察可以发现“__score”被重命名为了“_Report__score”，在原有的名称前加上了类的名称。试着用“_Report__score”在外部程序中调用该属性：

.. code-block::  C
  :linenos:

  >>> scores._Report__score
  91

当然，在平常使用时请避免这种用法。

4.11.3 类的三大特性
======================

面向对象编程的语言都具有三大特性——封装、多态和继承，Python也不例外。

1. 封装
---------------

封装的概念就是隐藏对象的属性值和方法的具体实现过程，只提供给外部程序必要的调用方法，通常使用“_”和“__”来将类中的属性私有化，防止外部访问。

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self._lesson = lesson
  ...         self._score = score
  ...     def get_lesson(self):
  ...         return self._lesson
  ...     def get_score(self):
  ...         return self._score

使用类时，我们只需传入两个参数lesson和score，就可以直接调用类中的方法，而不必关心方法是怎么实现的。

.. code-block::  C
  :linenos:

  #传入参数
  >>> scores = Report("Chinese",91)   

  #调用方法
  >>> scores.get_lesson()
  'Chinese'
  >>> scores.get_score()
  91

2. 继承
-----------

在创建新的类时，并不是都需要从头开始创建，如果新的类只是某一个现有的类的修改，我们可以用继承的方法来创建它。新创建的类被称为子类，
被继承的类被成为父类(也称作超类、基类)。子类将自动继承父类中的各个方法和属性，先来看一个简单的例子：

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         return self.lesson
  ...     def get_score(self):
  ...         return self.score
  ...
  >>> class Report_sub(Report):      
  ...     pass

子类的定义格式为：

 class 子类名(父类名)：

试着用子类来访问父类中的属性和方法：

.. code-block::  C
  :linenos:

  >>> scores = Report_sub("Chinese",91)

  >>> scores.lesson
  'Chinese'
  >>> scores.get_lesson()
  'Chinese'

除了可以复制父类已有的属性和方法之外，在子类中还能对父类的属性和方法进行重写覆盖，这也是子类的一个重要特点。

首先是对父类中的属性进行重写：

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         return self.lesson
  ...     def get_score(self):
  ...         return self.score
  ...
  >>> class Report_sub(Report):
  ...     def __init__(self,name,lesson,score):
  ...         self.name = name
  ...         self.lesson = lesson
  ...         self.score = score
  ...
  >>> scores = Report_sub('Stan','Chinese',91)
  >>> scores.name
  'Stan'

当子类中使用“__init__”对父类的属性重写覆盖时，Python不会再调用父类中的“__init__”。如果一定要调用父类中的“__init__”方法，
可以使用super()函数。

.. code-block::  C
  :linenos:

  >>> class Report_sub(Report):
  ...     def __init__(self,name,lesson,score):
  ...         self.name = name
  ...         super().__init__(lesson,score)
  ...
  >>> scores = Report_sub('Stan','Chinese',91)
  >>> scores.lesson
  'Chinese'

在子类中对父类的方法进行重写：

.. code-block::  C
  :linenos:

  >>> class Report_sub(Report):
  ...     def __init__(self,name,lesson,score):
  ...         self.name = name
  ...         super().__init__(lesson,score)
  ...     def get_lesson(self):
  ...         return self.name+"'s lesson is "+self.lesson
  ...
  >>> scores = Report_sub('Stan','Chinese',91)
  >>> scores.get_lesson()
  "Stan's lesson is Chinese"

在子类中对父类的get_lesson方法进行重写，Python不会再调用父类中的get_lesson方法。
同样可以使用super()函数手动调用父类中被重写的方法。

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         print(self.lesson)
  ...     def get_score(self):
  ...         return self.score
  ...
  >>> class Report_sub(Report):
  ...     def __init__(self,name,lesson,score):
  ...         self.name = name
  ...         super().__init__(lesson,score)
  ...     def get_lesson(self):
  ...         super().get_lesson()
  ...         return self.name+"'s lesson is "+self.lesson
  ...
  >>> scores = Report_sub('Stan','Chinese',91)
  >>> scores.get_lesson()
  Chinese
  "Stan's lesson is Chinese"

第6行中的return需修改为print，否则会被子类get_lesson方法中的return覆盖。

Python中的子类还支持多重继承，一个子类可以继承多个父类，在这个子类中可以继承各个父类中的所有方法，
下面以几个例子来对多重继承的特点进行介绍：

.. code-block::  C
  :linenos:

  >>> class Report_1:
  ...     def __init__(self,lesson,score):
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         return self.lesson
  ...     def get_score(self):
  ...         return self.score
  ...
  >>> class Report_2:
  ...     def __init__(self,name,lesson,score):
  ...         self.name = name
  ...         self.lesson = lesson
  ...         self.score = score
  ...     def get_lesson(self):
  ...         return self.name+"'s lesson is "+ self.lesson
  ...     def get_score(self):
  ...         return self.lesson+"'s score is "+ str(self.score)
  ...
  >>> class Report_sub(Report_1,Report_2):
  ...     pass

Report_sub类是Report_1类和Report_2类的子类，那么Report_sub类的属性值和方法调用的是哪个父类中的属性值和方法呢？请看下面的程序。

.. code-block::  C
  :linenos:

  #对象实例化
  >>> scores = Report_sub('Stan','Chinese',91)
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  TypeError: __init__() takes 3 positional arguments but 4 were given

  >>> scores = Report_sub('Chinese',91)

  #调用属性值和方法
  >>> scores.lesson
  'Chinese'
  >>> scores.get_score()
  91
  
可以看出，对象实例化时会先调用第一个父类进行属性值的初始化，而方法的调用也是优先调用第一个父类中的方法。因此，在使用多重继承时，
如果父类中的方法名存在同名情况，请小心排列它们在子类中定义时的顺序。

3. 多态
----------

多态指的是在调用同一个方法时，随着对象的不同，方法的返回值也是多样的。在使用多态时，有两个必要的要求：

 1. 多态一定发生在子类和父类之间。
 2. 多态中存在子类对父类方法的重写。

请看下面的程序：

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,score):
  ...         self.score = score
  ...     def get_score(self):
  ...         return self.score
  ...
  >>> class Math(Report):
  ...     def get_score(self):
  ...         return "Your Math score is "+ str(self.score)
  ...
  >>> class Sports(Report):
  ...     def get_score(self):
  ...         return "Your Sports score is "+ str(self.score)

  >>> math = Math(96)
  >>> sports = Sports(90)

  >>> math.get_score()
  'Your Math score is 96'
  >>> sports.get_score()
  'Your Sports score is 90'

该程序中共涉及到了一个父类——Report，两个子类——Math和Sports，两个对象——math和sports，
从程序中的第18行到第21行可以看出，两个不同的对象调用了同一个方法，得到了不同的结果。

或许你会说，直接在父类中再定义两个方法“get_score_1和get_score_2”也可以实现这种效果。
实际上，真正体现多态好处的编程是这样的：

.. code-block::  C
  :linenos:

  >>> class Report:
  ...     def __init__(self,score):
  ...         self.score = score
  ...     def get_score(self):
  ...         print(self.score)
  ...
  >>> class Math(Report):
  ...     def get_score(self):
  ...         print("Your Math score is "+ str(self.score))
  ...
  >>> class Sports(Report):
  ...     def get_score(self):
  ...         print("Your Sports score is "+ str(self.score))
  ...
  >>> def scores(object):
  ...     object.get_score()

  >>> math = Math(96)
  >>> sports = Sports(90)

  >>> scores(math)
  Your Math score is 96
  >>> scores(sports)
  Your Sports score is 90

请看程序中的第15、16行，定义了一个名为scores的函数，只需调用scores函数就可以根据传入对象的不同，去调用相应的方法。
它还有另外一种写法：

.. code-block::  C
  :linenos:

  >>> class Scores:
  ...     def lesson(self,object):
  ...         object.get_score()
  
  >>> math = Math(96)
  >>> sports = Sports(90)
  >>> scores = Scores()

  >>> scores.lesson(math)
  Your Math score is 96
  >>> scores.lesson(sports)
  Your Sports score is 90

定义一个新的类Scores，其它的对象都通过Scores的lesson方法去访问相应的get_score方法，得到对应的结果。如果你想要添加一个新的对象，
只需在父类后添加一个新的子类即可，它同样可以被scores.lesson(对象名)调用它对应的方法，从中也反应出了多态的可扩展性和灵活性。

这种基于多态，以一个函数或一个方法来统一调用的结构也被称为“鸭子模型”。

4.11.4 小结
====================

本节中对类的定义、类中属性和方法命名的约定以及类的三种特性做了介绍，类中的内容非常多，也是Python中相当重要的一个部分，
因此，请认真理解类的概念，这将有助于理解之后的编程项目对中各种现有类的使用。

在实际的编程项目中，我们常常会直接使用现有的模块，而模块中会有各种各样的函数、变量、类等，，在下一节中就会对什么是模块、
如何导入模块中的类等方面做介绍。





