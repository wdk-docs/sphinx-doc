.. php-domain:

PHP域
======

关于
-----

一个为 ''sphinx >= 1.0'' 提供PHP语言支持的域

:作者: Mark Story
:文档: `sphinxcontrib-phpdomain package documentation <http://packages.python.org/sphinxcontrib-phpdomain>`_
:主页: http://bitbucket.org/markstory/sphinx-contrib
:下载: http://pypi.python.org/pypi/sphinxcontrib-phpdomain
:许可: BSD
:平台: 任何平台

PHP域支持以下对象:

* 全局变量(global)
* 全局函数(function)
* 常量(constant)
* 名称空间(namespace)

  * 函数(Function)
  * 类(Class)

* 类(Class)

  * 类常量(Class constant)
  * 实例方法(Instance methods)
  * 静态方法(Static methods)
  * 属性(Properties)

.. note::

   这个域这样表达方法和属性名称::

      Class::method_name
      Class::$attribute_name

   在PHP中使用 ``\`` 语法访问命名空间中的类/函数::

        Package\Subpackage\Class


安装
-----

本地安装:
^^^^^^^^^^

.. code-block:: bash

 #sudo pip install sphinxcontrib-phpdomain --upgrade
 #cd docs/
 #vim conf.py

.. code-block:: python

 #添加扩展
 extensions = [
    ...
    'sphinxcontrib.phpdomain',
 ]
 #设置默认域
 primary_domain = 'php'

ReadTheDocs安装
^^^^^^^^^^^^^^^^

下载

+----------------------------------------------------+--------+------------+-------------+------+
| File                                               | Type   | Py Version | Uploaded on | Size |
+====================================================+========+============+=============+======+
| `sphinxcontrib-phpdomain-0.1.4.tar.gz`_ ( `md5`_ ) | Source |            | 2012-11-03  | 8KB  |
+----------------------------------------------------+--------+------------+-------------+------+

.. _sphinxcontrib-phpdomain-0.1.4.tar.gz: https://pypi.python.org/packages/source/s/sphinxcontrib-phpdomain/sphinxcontrib-phpdomain-0.1.4.tar.gz#md5=03ce0f0569db0217f7471c2f7e952841

.. _md5: https://pypi.python.org/pypi?:action=show_md5&digest=03ce0f0569db0217f7471c2f7e952841

.. code-block:: bash

 #cd docs/
 #mkdir _exts
 #cp path/sphinxcontrib-phpdomain-0.1.4/sphinxcontrib/phpdomain.py ./_exts
 #vim conf.py

.. code-block:: python

 #引入os
 import sys, os

 #设置扩展路径
 sys.path.append(os.path.abspath('_exts'))

 #添加扩展
 extensions = [
    ...
    'phpdomain',
 ]

 #设置默认域
 primary_domain = 'php'

实例
-----

源码如下:

.. code-block:: rest

  .. php:class:: DateTime

    Datetime class

    .. php:method:: setDate($year, $month, $day)

        Set the date.

        :param int $year: The year.
        :param int $month: The month.
        :param int $day: The day.
        :returns: Either false on failure, or the datetime object for method chaining.


    .. php:method:: setTime($hour, $minute[, $second])

        Set the time.

        :param int $hour: The hour
        :param int $minute: The minute
        :param int $second: The second
        :returns: Either false on failure, or the datetime object for method chaining.

    .. php:const:: ATOM

        Y-m-d\TH:i:sP

返回结果:

.. php:class:: DateTime

  Datetime class

  .. php:method:: setDate($year, $month, $day)

      Set the date.

      :param int $year: The year.
      :param int $month: The month.
      :param int $day: The day.
      :returns: Either false on failure, or the DateTime object for method chaining.


  .. php:method:: setTime($hour, $minute[, $second])

      Set the time.

      :param int $hour: The hour
      :param int $minute: The minute
      :param int $second: The second
      :returns: Either false on failure, or the DateTime object for method chaining.

  .. php:const:: ATOM

      Y-m-d\TH:i:sP
      
交叉引用:

.. code-block:: rest

   你可以使用  :php:meth:`DateTime::setDate` 修改 ``DateTime`` 的日期。

返回结果:

你可以使用  :php:meth:`DateTime::setDate` 修改 ``DateTime`` 的日期。

指令
-----

PHP域提供以下指令，大部分指令跟Python类似。

每个指令填充索引，或命名空间索引。

.. rst:directive:: .. php:namespace:: name

   该指令声明一个新的PHP名称空间。  It accepts nested
   namespaces by separating namespaces with ``\\``.  It does not generate
   any content like :rst:dir:`php:class` does.  It will however, generate 
   an entry in the namespace/module index.
   
   它有 ``synopsis`` 和 ``deprecated`` 选项, 类似 :rst:dir:`py:module`
  
.. rst:directive:: .. php:global:: name

   该指令声明一个PHP全局变量.

.. rst:directive:: .. php:function:: name(signature)

   Defines a new global/namespaced function outside of a class.  You can use 
   many of the same field lists as the python domain.  However, ``raises`` 
   is replaced with ``throws``

.. rst:directive:: .. php:const:: name

   该指令声明一个PHP全局常量, you can also used it nested 
   inside a class directive to create class constants.
   
.. rst:directive:: .. php:exception:: name

   该指令在当前名称空间中声明一个新的异常. The 
   signature can include constructor arguments.

.. rst:directive:: .. php:interface:: name

   描述接口.  Methods and constants belonging to the interface 
   should follow or be nested inside this directive.

.. rst:directive:: .. php:trait:: name

   描述一个特征.  Methods beloning to the trait should follow or be nested
   inside this directive.

.. rst:directive:: .. php:class:: name

   描述一个类.  Methods, attributes, and constants belonging to the class
   should be inside this directive's body:

.. code-block:: rest

        .. php:class:: MyClass
            Class description
           .. php:method:: method($argument)
           Method description

Attributes, methods and constants don't need to be nested.  They can also just follow the class declaration:

.. code-block:: rest

        .. php:class:: MyClass
            Text about the class
        .. php:method:: methodName()
            Text about the method

.. seealso:: .. php:method:: name
             .. php:attr:: name
             .. php:const:: name

.. rst:directive:: .. php:method:: name(signature)

   描述一个类的方法, its arguments, return value, and exceptions:

.. code-block:: rest

        .. php:method:: instanceMethod($one, $two)

            :param string $one: The first parameter.
            :param string $two: The second parameter.
            :returns: An array of stuff.
            :throws: InvalidArgumentException

            This is an instance method.

.. rst:directive:: .. php:staticmethod:: ClassName::methodName(signature)

    描述一个静态方法, its arguments, return value and exceptions,
    see :rst:dir:`php:method` for options.

.. rst:directive:: .. php:attr:: name

   描述一个类的属性/特质.

交叉引用
---------

以下角色，引用PHP的对象，如果找到匹配指令将生成链接:

.. rst:role:: php:ns

   引用命名空间. 嵌套名称空间需要使用ReST语法的两个 ``\\`` 分开::
   
      .. php:ns:`LibraryName\\SubPackage` will work correctly.

.. rst:role:: php:func

   引用函数，无论是在一个名称空间或不在. 如果函数是在一个名称空间,一定要包括名称空间, 除非你是目前在相同的名称空间.

.. rst:role:: php:global

   引用带 ``$`` 前缀的全局变量.
   
.. rst:role:: php:const

   引用全局常量，或者类常量。  类常量应该在类中::
   
        DateTime has an :php:const:`DateTime::ATOM` constant.

.. rst:role:: php:class

   引用类; 带有名称空间的名称可以使用。 如果你有一个名称空间,你应该使用以下风格::
   
     :php:class:`LibraryName\\ClassName`

.. rst:role:: php:meth

   引用class/interface/trait方法. 这个角色支持两种方法::
   
     :php:meth:`DateTime::setDate`
     :php:meth:`Classname::staticMethod`

.. rst:role:: php:attr

   引用对象属性::
   
      :php:attr:`ClassName::$propertyName`

.. rst:role:: php:exc

   引用异常. 带有名称空间的名称可以使用。

.. rst:role:: php:interface

   引用接口. 带有名称空间的名称可以使用。

.. rst:role:: php:trait

   引用特质。带有名称空间的名称可以使用。
