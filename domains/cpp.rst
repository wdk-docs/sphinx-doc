.. _cpp-domain:

C++域
--------------

The C++ domain (name **cpp**) supports documenting C++ projects.

The following directives are available:

.. rst:directive:: .. cpp:class:: signatures
               .. cpp:function:: signatures
               .. cpp:member:: signatures
               .. cpp:type:: signatures

   Describe a C++ object.  Full signature specification is supported -- give the
   signature as you would in the declaration.  Here some examples::

      .. cpp:function:: bool namespaced::theclass::method(int arg1, std::string arg2)

         Describes a method with parameters and types.

      .. cpp:function:: bool namespaced::theclass::method(arg1, arg2)

         Describes a method without types.

      .. cpp:function:: const T &array<T>::operator[]() const

         Describes the constant indexing operator of a templated array.

      .. cpp:function:: operator bool() const

         Describe a casting operator here.

      .. cpp:function:: constexpr void foo(std::string &bar[2]) noexcept

         Describe a constexpr function here.

      .. cpp:member:: std::string theclass::name

      .. cpp:member:: std::string theclass::name[N][M]

      .. cpp:type:: theclass::const_iterator

   Will be rendered like this:

      .. cpp:function:: bool namespaced::theclass::method(int arg1, std::string arg2)

         Describes a method with parameters and types.

      .. cpp:function:: bool namespaced::theclass::method(arg1, arg2)

         Describes a method without types.

      .. cpp:function:: const T &array<T>::operator[]() const

         Describes the constant indexing operator of a templated array.

      .. cpp:function:: operator bool() const

         Describe a casting operator here.

      .. cpp:function:: constexpr void foo(std::string &bar[2]) noexcept

         Describe a constexpr function here.

      .. cpp:member:: std::string theclass::name

      .. cpp:member:: std::string theclass::name[N][M]

      .. cpp:type:: theclass::const_iterator

.. rst:directive:: .. cpp:namespace:: namespace

   Select the current C++ namespace for the following objects.


.. _cpp-roles:

These roles link to the given object types:

.. rst:role:: cpp:class
          cpp:func
          cpp:member
          cpp:type

   Reference a C++ object.  You can give the full signature (and need to, for
   overloaded functions.)

   .. note::

      Sphinx' syntax to give references a custom title can interfere with
      linking to template classes, if nothing follows the closing angle
      bracket, i.e. if the link looks like this: ``:cpp:class:`MyClass<T>```.
      This is interpreted as a link to ``T`` with a title of ``MyClass``.
      In this case, please escape the opening angle bracket with a backslash,
      like this: ``:cpp:class:`MyClass\<T>```.

.. admonition:: Note on References

   It is currently impossible to link to a specific version of an
   overloaded method.  Currently the C++ domain is the first domain
   that has basic support for overloaded methods and until there is more
   data for comparison we don't want to select a bad syntax to reference a
   specific overload.  Currently Sphinx will link to the first overloaded
   version of the method / function.
