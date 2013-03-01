.. _python-domain:

Python域
-----------------

The Python domain (name **py**) provides the following directives for module
declarations:

.. rst:directive:: .. py:module:: name

   This directive marks the beginning of the description of a module (or package
   submodule, in which case the name should be fully qualified, including the
   package name).  It does not create content (like e.g. :rst:dir:`py:class` does).

   This directive will also cause an entry in the global module index.

   The ``platform`` option, if present, is a comma-separated list of the
   platforms on which the module is available (if it is available on all
   platforms, the option should be omitted).  The keys are short identifiers;
   examples that are in use include "IRIX", "Mac", "Windows", and "Unix".  It is
   important to use a key which has already been used when applicable.

   The ``synopsis`` option should consist of one sentence describing the
   module's purpose -- it is currently only used in the Global Module Index.

   The ``deprecated`` option can be given (with no value) to mark a module as
   deprecated; it will be designated as such in various locations then.


.. rst:directive:: .. py:currentmodule:: name

   This directive tells Sphinx that the classes, functions etc. documented from
   here are in the given module (like :rst:dir:`py:module`), but it will not
   create index entries, an entry in the Global Module Index, or a link target
   for :rst:role:`py:mod`.  This is helpful in situations where documentation
   for things in a module is spread over multiple files or sections -- one
   location has the :rst:dir:`py:module` directive, the others only
   :rst:dir:`py:currentmodule`.


The following directives are provided for module and class contents:

.. rst:directive:: .. py:data:: name

   Describes global data in a module, including both variables and values used
   as "defined constants."  Class and object attributes are not documented
   using this environment.

.. rst:directive:: .. py:exception:: name

   Describes an exception class.  The signature can, but need not include
   parentheses with constructor arguments.

.. rst:directive:: .. py:function:: name(signature)

   Describes a module-level function.  The signature should include the
   parameters, enclosing optional parameters in brackets.  Default values can be
   given if it enhances clarity; see :ref:`signatures`.  For example::

      .. py:function:: Timer.repeat([repeat=3[, number=1000000]])

   Object methods are not documented using this directive. Bound object methods
   placed in the module namespace as part of the public interface of the module
   are documented using this, as they are equivalent to normal functions for
   most purposes.

   The description should include information about the parameters required and
   how they are used (especially whether mutable objects passed as parameters
   are modified), side effects, and possible exceptions.  A small example may be
   provided.

.. rst:directive:: .. py:class:: name[(signature)]

   Describes a class.  The signature can include parentheses with parameters
   which will be shown as the constructor arguments.  See also
   :ref:`signatures`.

   Methods and attributes belonging to the class should be placed in this
   directive's body.  If they are placed outside, the supplied name should
   contain the class name so that cross-references still work.  Example::

      .. py:class:: Foo
         .. py:method:: quux()

      -- or --

      .. py:class:: Bar

      .. py:method:: Bar.quux()

   The first way is the preferred one.

.. rst:directive:: .. py:attribute:: name

   Describes an object data attribute.  The description should include
   information about the type of the data to be expected and whether it may be
   changed directly.

.. rst:directive:: .. py:method:: name(signature)

   Describes an object method.  The parameters should not include the ``self``
   parameter.  The description should include similar information to that
   described for ``function``.  See also :ref:`signatures`.

.. rst:directive:: .. py:staticmethod:: name(signature)

   Like :rst:dir:`py:method`, but indicates that the method is a static method.

   .. versionadded:: 0.4

.. rst:directive:: .. py:classmethod:: name(signature)

   Like :rst:dir:`py:method`, but indicates that the method is a class method.

   .. versionadded:: 0.6

.. rst:directive:: .. py:decorator:: name
                   .. py:decorator:: name(signature)

   Describes a decorator function.  The signature should *not* represent the
   signature of the actual function, but the usage as a decorator.  For example,
   given the functions

   .. code-block:: python

      def removename(func):
          func.__name__ = ''
          return func

      def setnewname(name):
          def decorator(func):
              func.__name__ = name
              return func
          return decorator

   the descriptions should look like this::

      .. py:decorator:: removename

         Remove name of the decorated function.

      .. py:decorator:: setnewname(name)

         Set name of the decorated function to *name*.

   There is no ``py:deco`` role to link to a decorator that is marked up with
   this directive; rather, use the :rst:role:`py:func` role.

.. rst:directive:: .. py:decoratormethod:: name
                   .. py:decoratormethod:: name(signature)

   Same as :rst:dir:`py:decorator`, but for decorators that are methods.

   Refer to a decorator method using the :rst:role:`py:meth` role.


.. _signatures:

Python签名
~~~~~~~~~~~~~~~~~

Signatures of functions, methods and class constructors can be given like they
would be written in Python, with the exception that optional parameters can be
indicated by brackets::

   .. py:function:: compile(source[, filename[, symbol]])

It is customary to put the opening bracket before the comma.  In addition to
this "nested" bracket style, a "flat" style can also be used, due to the fact
that most optional parameters can be given independently::

   .. py:function:: compile(source[, filename, symbol])

Default values for optional arguments can be given (but if they contain commas,
they will confuse the signature parser).  Python 3-style argument annotations
can also be given as well as return type annotations::

   .. py:function:: compile(source : string[, filename, symbol]) -> ast object


信息字段列表
~~~~~~~~~~~~~~~~

.. versionadded:: 0.4

Inside Python object description directives, reST field lists with these fields
are recognized and formatted nicely:

* ``param``, ``parameter``, ``arg``, ``argument``, ``key``, ``keyword``:
  Description of a parameter.
* ``type``: Type of a parameter.
* ``raises``, ``raise``, ``except``, ``exception``: That (and when) a specific
  exception is raised.
* ``var``, ``ivar``, ``cvar``: Description of a variable.
* ``returns``, ``return``: Description of the return value.
* ``rtype``: Return type.

The field names must consist of one of these keywords and an argument (except
for ``returns`` and ``rtype``, which do not need an argument).  This is best
explained by an example::

   .. py:function:: format_exception(etype, value, tb[, limit=None])

      Format the exception with a traceback.

      :param etype: exception type
      :param value: exception value
      :param tb: traceback object
      :param limit: maximum number of stack frames to show
      :type limit: integer or None
      :rtype: list of strings

This will render like this:

   .. py:function:: format_exception(etype, value, tb[, limit=None])
      :noindex:

      Format the exception with a traceback.

      :param etype: exception type
      :param value: exception value
      :param tb: traceback object
      :param limit: maximum number of stack frames to show
      :type limit: integer or None
      :rtype: list of strings

It is also possible to combine parameter type and description, if the type is a
single word, like this::

   :param integer limit: maximum number of stack frames to show


.. _python-roles:

交叉引用Python对象
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following roles refer to objects in modules and are possibly hyperlinked if
a matching identifier is found:

.. rst:role:: py:mod

   Reference a module; a dotted name may be used.  This should also be used for
   package names.

.. rst:role:: py:func

   Reference a Python function; dotted names may be used.  The role text needs
   not include trailing parentheses to enhance readability; they will be added
   automatically by Sphinx if the :confval:`add_function_parentheses` config
   value is true (the default).

.. rst:role:: py:data

   Reference a module-level variable.

.. rst:role:: py:const

   Reference a "defined" constant.  This may be a C-language ``#define`` or a
   Python variable that is not intended to be changed.

.. rst:role:: py:class

   Reference a class; a dotted name may be used.

.. rst:role:: py:meth

   Reference a method of an object.  The role text can include the type name and
   the method name; if it occurs within the description of a type, the type name
   can be omitted.  A dotted name may be used.

.. rst:role:: py:attr

   Reference a data attribute of an object.

.. rst:role:: py:exc

   Reference an exception.  A dotted name may be used.

.. rst:role:: py:obj

   Reference an object of unspecified type.  Useful e.g. as the
   :confval:`default_role`.

   .. versionadded:: 0.4

The name enclosed in this markup can include a module name and/or a class name.
For example, ``:py:func:`filter``` could refer to a function named ``filter`` in
the current module, or the built-in function of that name.  In contrast,
``:py:func:`foo.filter``` clearly refers to the ``filter`` function in the
``foo`` module.

Normally, names in these roles are searched first without any further
qualification, then with the current module name prepended, then with the
current module and class name (if any) prepended.  If you prefix the name with a
dot, this order is reversed.  For example, in the documentation of Python's
:mod:`codecs` module, ``:py:func:`open``` always refers to the built-in
function, while ``:py:func:`.open``` refers to :func:`codecs.open`.

A similar heuristic is used to determine whether the name is an attribute of the
currently documented class.

Also, if the name is prefixed with a dot, and no exact match is found, the
target is taken as a suffix and all object names with that suffix are
searched.  For example, ``:py:meth:`.TarFile.close``` references the
``tarfile.TarFile.close()`` function, even if the current module is not
``tarfile``.  Since this can get ambiguous, if there is more than one possible
match, you will get a warning from Sphinx.

Note that you can combine the ``~`` and ``.`` prefixes:
``:py:meth:`~.TarFile.close``` will reference the ``tarfile.TarFile.close()``
method, but the visible link caption will only be ``close()``.

