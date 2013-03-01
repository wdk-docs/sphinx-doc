.. _c-domain:

C域
------------

The C domain (name **c**) is suited for documentation of C API.

.. rst:directive:: .. c:function:: type name(signature)

   Describes a C function. The signature should be given as in C, e.g.::

      .. c:function:: PyObject* PyType_GenericAlloc(PyTypeObject *type, Py_ssize_t nitems)

   This is also used to describe function-like preprocessor macros.  The names
   of the arguments should be given so they may be used in the description.

   Note that you don't have to backslash-escape asterisks in the signature, as
   it is not parsed by the reST inliner.

.. rst:directive:: .. c:member:: type name

   Describes a C struct member. Example signature::

      .. c:member:: PyObject* PyTypeObject.tp_bases

   The text of the description should include the range of values allowed, how
   the value should be interpreted, and whether the value can be changed.
   References to structure members in text should use the ``member`` role.

.. rst:directive:: .. c:macro:: name

   Describes a "simple" C macro.  Simple macros are macros which are used for
   code expansion, but which do not take arguments so cannot be described as
   functions.  This is not to be used for simple constant definitions.  Examples
   of its use in the Python documentation include :c:macro:`PyObject_HEAD` and
   :c:macro:`Py_BEGIN_ALLOW_THREADS`.

.. rst:directive:: .. c:type:: name

   Describes a C type (whether defined by a typedef or struct). The signature
   should just be the type name.

.. rst:directive:: .. c:var:: type name

   Describes a global C variable.  The signature should include the type, such
   as::

      .. c:var:: PyObject* PyClass_Type


.. _c-roles:

交叉引用C架构
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following roles create cross-references to C-language constructs if they are
defined in the documentation:

.. rst:role:: c:data

   Reference a C-language variable.

.. rst:role:: c:func

   Reference a C-language function. Should include trailing parentheses.

.. rst:role:: c:macro

   Reference a "simple" C macro, as defined above.

.. rst:role:: c:type

   Reference a C-language type.
