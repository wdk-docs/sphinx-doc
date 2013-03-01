.. php-domain:

PHP域
---------------

The PHP domain provides the following directives. 
Most directives are similar to Python's.

关于
^^^^^^^

一个为 ''sphinx >= 1.0'' 提供PHP语言支持的域

项目地址：

:PyPI: http://pypi.python.org/pypi/sphinxcontrib-phpdomain
:详细文档: http://packages.python.org/sphinxcontrib-phpdomain

PHP域支持一下对象:

* Global variable
* Global function
* Constant
* Namespace

  * Function
  * Class

* Class

  * Class constant
  * Instance methods
  * Static methods
  * Properties

.. note::

   这个域这样表达方法和属性名称::

      Class::method_name
      Class::$attribute_name

   You address classes/functions in namespaces using \\ syntax as you would in PHP::

        Package\Subpackage\Class


安装
^^^^^^

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

实例
^^^^^^^

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
^^^^^^^^^^^^^^^^

每个指令填充索引，或命名空间索引。

.. rst:directive:: .. php:namespace:: name

   这个指令声明一个新的PHP名称空间。  It accepts nested
   namespaces by separating namespaces with ``\``.  It does not generate
   any content like :rst:dir:`php:class` does.  It will however, generate 
   an entry in the namespace/module index.
   
   它有 ``synopsis`` 和 ``deprecated`` 选项, 类似 :rst:dir:`py:module`
  
.. rst:directive:: .. php:global:: name

   This directive declares a new PHP global variable.

.. rst:directive:: .. php:function:: name(signature)

   Defines a new global/namespaced function outside of a class.  You can use 
   many of the same field lists as the python domain.  However, ``raises`` 
   is replaced with ``throws``

.. rst:directive:: .. php:const:: name

   This directive declares a new PHP constant, you can also used it nested 
   inside a class directive to create class constants.
   
.. rst:directive:: .. php:exception:: name

   This directive declares a new Exception in the current namespace. The 
   signature can include constructor arguments.

.. rst:directive:: .. php:interface:: name

   Describe an interface.  Methods and constants belonging to the interface 
   should follow or be nested inside this directive.

.. rst:directive:: .. php:trait:: name

   Describe a trait.  Methods beloning to the trait should follow or be nested
   inside this directive.

.. rst:directive:: .. php:class:: name

   Describes a class.  Methods, attributes, and constants belonging to the class
   should be inside this directive's body::

        .. php:class:: MyClass
        
            Class description
        
           .. php:method:: method($argument)
        
           Method description


   Attributes, methods and constants don't need to be nested.  They can also just 
   follow the class declaration::

        .. php:class:: MyClass
        
            Text about the class
        
        .. php:method:: methodName()
        
            Text about the method
        

   .. seealso:: .. php:method:: name
                .. php:attr:: name
                .. php:const:: name

.. rst:directive:: .. php:method:: name(signature)

   Describe a class method, its arguments, return value, and exceptions::
   
        .. php:method:: instanceMethod($one, $two)
        
            :param string $one: The first parameter.
            :param string $two: The second parameter.
            :returns: An array of stuff.
            :throws: InvalidArgumentException
        
           This is an instance method.

.. rst:directive:: .. php:staticmethod:: ClassName::methodName(signature)

    Describe a static method, its arguments, return value and exceptions,
    see :rst:dir:`php:method` for options.

.. rst:directive:: .. php:attr:: name

   Describe an property/attribute on a class.

交叉引用
^^^^^^^^^^^^^^^^^^^^^^^^^

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
