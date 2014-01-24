.. highlight:: rst

第一次使用
=======================

本文旨在给出一个教程样的概览,以便大家快速明了 Sphnix 如何使用, 点击绿色箭头的 “详细” 链接将进入对应操作的高级手册.


设置文档源
------------------------------------

包含所有文档原始文本的目录称作: :term:`资源目录`.  此目录也包含 Sphnix 配置文件 :file:`conf.py`, Sphnix 根据此文件的声明查阅和生成文档. [#]_

Sphnix 内置了一个脚本  :program:`sphinx-quickstart` 可以自动生成默认的 :file:`conf.py` 只需调用之 ::

   $ sphinx-quickstart

并回答几个问题. (注意,对 “autodoc” 回答 Yes.)

同时还有个叫 :program:`sphinx-apidoc` 自动"API文档"生成器， 参考 :ref:`invocation-apidoc` .


定义文档结构
---------------------------

假设你已经执行了 :program:`sphinx-quickstart`. 已经创建包含 :file:`conf.py` 的资源目录和主控文件 :file:`index.rst` (如果你接受默认).   :term:`主控文档` 的主函数是担任欢迎页面, 并包含了"table of contents tree"的根(or *toctree*).  这是Sphinx添加到reStructuredText主要事情之一, 连接多个文件到一层文档的方法.

.. sidebar:: reStructuredText 指令

   ``toctree`` 是一个 reStructuredText :dfn:`指令`, 一个非常好用的标签块.  指令包含参数选项和内容.

   *参数* are given directly after the double colon following the
   directive's name.  Each directive decides whether it can have arguments, and
   how many.

   *选项* are given after the arguments, in form of a "field list".  The
   ``maxdepth`` is such an option for the ``toctree`` directive.

   *内容* follows the options or arguments after a blank line.  Each
   directive decides whether to allow content, and what to do with it.

   A common gotcha with directives is that **the first line of the content must
   be indented to the same level as the options are**.


toctree指令开头是空的,如下::

   .. toctree::
      :maxdepth: 2

在指令*内容*中添加文档列表::

   .. toctree::
      :maxdepth: 2

      intro
      tutorial
      ...

直接书写 :term:`文档名`\ s ，不用写扩展，使用斜线来分割目录.

|more| 更多 :ref:`toctree 指令 <toctree-directive>`.

You can now create the files you listed in the toctree and add content, and
their section titles will be inserted (up to the "maxdepth" level) at the place
where the toctree directive is placed.  Also, Sphinx now knows about the order
and hierarchy of your documents.  (They may contain ``toctree`` directives
themselves, which means you can create deeply nested hierarchies if necessary.)


添加内容
--------------

In Sphinx source files, you can use most features of standard reStructuredText.
There are also several features added by Sphinx.  For example, you can add
cross-file references in a portable way (which works for all output types) using
the :rst:role:`ref` role.

For an example, if you are viewing the HTML version you can look at the source
for this document -- use the "Show Source" link in the sidebar.

|more| See :ref:`rst-primer` for a more in-depth introduction to
reStructuredText and :ref:`sphinxmarkup` for a full list of markup added by
Sphinx.


创建
-----------------

添加文件和内容之后就可以创建docs了。使用程序 :program:`sphinx-build` , 如下::

   $ sphinx-build -b html sourcedir builddir

*sourcedir* 是 :term:`资源目录`, *builddir* 存放创建文档的地方. :option:`-b`
选项是选择一个创建器; 本例是创建html文件.

|more| 查看更多 :ref:`invocation` for all options that :program:`sphinx-build`
supports.

然而, :program:`sphinx-quickstart` 创建了 :file:`Makefile` 和
:file:`make.bat` 可以很容易的创建life:  如下 ::

   $ make html

to build HTML docs in the build directory you chose.  Execute ``make`` without
an argument to see which targets are available.

.. admonition:: How do I generate PDF documents?

   ``make latexpdf`` runs the :mod:`LaTeX builder
   <sphinx.builders.latex.LaTeXBuilder>` and readily invokes the pdfTeX
   toolchain for you.


文档项目
-------------------

One of Sphinx' main objectives is easy documentation of :dfn:`objects` (in a
very general sense) in any :dfn:`domain`.  A domain is a collection of object
types that belong together, complete with markup to create and reference
descriptions of these objects.

The most prominent domain is the Python domain.  To e.g. document the Python
built-in function ``enumerate()``, you would add this to one of your source
files::

   .. py:function:: enumerate(sequence[, start=0])

      Return an iterator that yields tuples of an index and an item of the
      *sequence*. (And so on.)

This is rendered like this:

.. py:function:: enumerate(sequence[, start=0])

   Return an iterator that yields tuples of an index and an item of the
   *sequence*. (And so on.)

The argument of the directive is the :dfn:`signature` of the object you
describe, the content is the documentation for it.  Multiple signatures can be
given, each in its own line.

The Python domain also happens to be the default domain, so you don't need to
prefix the markup with the domain name::

   .. function:: enumerate(sequence[, start=0])

      ...

does the same job if you keep the default setting for the default domain.

There are several more directives for documenting other types of Python objects,
for example :rst:dir:`py:class` or :rst:dir:`py:method`.  There is also a
cross-referencing :dfn:`role` for each of these object types.  This markup will
create a link to the documentation of ``enumerate()``::

   The :py:func:`enumerate` function can be used for ...

And here is the proof: A link to :func:`enumerate`.

Again, the ``py:`` can be left out if the Python domain is the default one.  It
doesn't matter which file contains the actual documentation for ``enumerate()``;
Sphinx will find it and create a link to it.

Each domain will have special rules for how the signatures can look like, and
make the formatted output look pretty, or add specific features like links to
parameter types, e.g. in the C/C++ domains.

|more| See :ref:`domains` for all the available domains and their
directives/roles.


基本配置
-------------------

Earlier we mentioned that the :file:`conf.py` file controls how Sphinx processes
your documents.  In that file, which is executed as a Python source file, you
assign configuration values.  For advanced users: since it is executed by
Sphinx, you can do non-trivial tasks in it, like extending :data:`sys.path` or
importing a module to find out the version your are documenting.

The config values that you probably want to change are already put into the
:file:`conf.py` by :program:`sphinx-quickstart` and initially commented out
(with standard Python syntax: a ``#`` comments the rest of the line).  To change
the default value, remove the hash sign and modify the value.  To customize a
config value that is not automatically added by :program:`sphinx-quickstart`,
just add an additional assignment.

Keep in mind that the file uses Python syntax for strings, numbers, lists and so
on.  The file is saved in UTF-8 by default, as indicated by the encoding
declaration in the first line.  If you use non-ASCII characters in any string
value, you need to use Python Unicode strings (like ``project = u'Exposé'``).

|more| See :ref:`build-config` for documentation of all available config values.


Autodoc
-------

When documenting Python code, it is common to put a lot of documentation in the
source files, in documentation strings.  Sphinx supports the inclusion of
docstrings from your modules with an :dfn:`extension` (an extension is a Python
module that provides additional features for Sphinx projects) called "autodoc".

In order to use autodoc, you need to activate it in :file:`conf.py` by putting
the string ``'sphinx.ext.autodoc'`` into the list assigned to the
:confval:`extensions` config value.  Then, you have a few additional directives
at your disposal.

For example, to document the function ``io.open()``, reading its
signature and docstring from the source file, you'd write this::

   .. autofunction:: io.open

You can also document whole classes or even modules automatically, using member
options for the auto directives, like ::

   .. automodule:: io
      :members:

autodoc needs to import your modules in order to extract the docstrings.
Therefore, you must add the appropriate path to :py:data:`sys.path` in your
:file:`conf.py`.

|more| See :mod:`sphinx.ext.autodoc` for the complete description of the
features of autodoc.


涵盖的课题
-------------------------

- Other extensions (math, intersphinx, viewcode, doctest)
- Static files
- Selecting a theme
- Templating
- Using extensions
- Writing extensions


.. rubric:: Footnotes

.. [#] This is the usual lay-out.  However, :file:`conf.py` can also live in
       another directory, the :term:`配置目录`.  See
       :ref:`invocation`.

.. |more| image:: more.png
          :align: middle
          :alt: more info
