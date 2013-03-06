.. _glossary:

术语
====

.. glossary::

   创建器
      A class (inheriting from :class:`~sphinx.builders.Builder`) that takes
      parsed documents and performs an action on them.  Normally, builders
      translate the documents to an output format, but it is also possible to
      use the builder builders that e.g. check for broken links in the
      documentation, or build coverage information.

      See :ref:`builders` for an overview over Sphinx' built-in builders.

   配置目录
      The directory containing :file:`conf.py`.  By default, this is the same as
      the :term:`资源目录`, but can be set differently with the **-c**
      command-line option.

   指令
      A reStructuredText markup element that allows marking a block of content
      with special meaning.  Directives are supplied not only by docutils, but
      Sphinx and custom extensions can add their own.  The basic directive
      syntax looks like this:

      .. sourcecode:: rst

         .. directivename:: argument ...
            :option: value

            Content of the directive.

      See :ref:`directives` for more information.

   文档名
      Since reST source files can have different extensions (some people like
      ``.txt``, some like ``.rst`` -- the extension can be configured with
      :confval:`source_suffix`) and different OSes have different path separators,
      Sphinx abstracts them: :dfn:`document names` are always relative to the
      :term:`资源目录`, the extension is stripped, and path separators
      are converted to slashes.  All values, parameters and such referring to
      "documents" expect such document names.

      Examples for document names are ``index``, ``library/zipfile``, or
      ``reference/datamodel/types``.  Note that there is no leading or trailing
      slash.

   域
      A domain is a collection of markup (reStructuredText :term:`指令`\ s
      and :term:`角色`\ s) to describe and link to :term:`项目`\ s belonging
      together, e.g. elements of a programming language.  Directive and role
      names in a domain have names like ``domain:name``, e.g. ``py:function``.

      Having domains means that there are no naming problems when one set of
      documentation wants to refer to e.g. C++ and Python classes.  It also
      means that extensions that support the documentation of whole new
      languages are much easier to write.  For more information about domains,
      see the chapter :ref:`domains`.

   环境
      A structure where information about all documents under the root is saved,
      and used for cross-referencing.  The environment is pickled after the
      parsing stage, so that successive runs only need to read and parse new and
      changed documents.

   主控文档
      此文档包含根文档,以及 :rst:dir:`toctree` 指令.

   项目
      object,The basic building block of Sphinx documentation.  Every "object
      directive" (e.g. :rst:dir:`function` or :rst:dir:`object`) creates such a block;
      and most objects can be cross-referenced to.

   角色
      reStructuredText 标记元素,可以标记一段文本. 如同指令,角色是可扩展的. 基本语法类似:
      ``:rolename:`content```.  参考 :ref:`inlinemarkup`.

   资源目录
      此目录及子目录应该包含所有 Sphnix 工程需要的文件. (即:source directory)
