.. highlight:: rest

.. _inline-markup:

行内标记
=============

Sphinx使用解释的文本角色插入语义标记到文档中。

写法如下 ``:rolename:`content```.

.. note::

   The default role (```content```) has no special meaning by default.  You are
   free to use it for anything you like, e.g. variable names; use the
   :confval:`default_role` config value to set it to a known role.

查看更多 :ref:`域 <domains>` 添加的角色.


.. _xref-syntax:

交叉引用语法
~~~~~~~~~~~~~~~~~~~~~~~~

交叉引用是由大量语义解释文本的角色所产生的。
因为, 你只需要写 ``:role:`目标```, 并且将生成一个链接到由 *role* 指定类型的名字为 *目标* 的项目。链接文本就是 *目标*。

这有一些额外的设施，但是，那使交叉引用的角色更灵活：

* 你可以提供一个明确的标题和参考目标, 想在reST中直接超链接: ``:role:`标题 <目标>``` 将引用 *目标*, 但链接文本将是 *标题*.

* 使用前缀 ``!``, 将不创建引用/超链接.

* 使用前缀 ``~``, 链接文本只会是最后一个组件. 例如, ``:py:meth:`~Queue.Queue.get``` 将引用 ``Queue.Queue.get`` 但链接文本只显示 ``get`` 。

  在HTML输出里, 链接的 ``title`` 属性 (鼠标经过时显示的提示) 将会是目标全名.


交叉引用对象
-------------------------

这些角色是由各自域描述的:

* :ref:`Python <python-roles>`
* :ref:`C <c-roles>`
* :ref:`C++ <cpp-roles>`
* :ref:`JavaScript <js-roles>`
* :ref:`ReST <rst-roles>`


.. _ref-role:

任意位置交叉引用
-------------------------------------

.. rst:role:: ref

   To support cross-referencing to arbitrary locations in any document, the
   standard reST labels are used.  For this to work label names must be unique
   throughout the entire documentation.  There are two ways in which you can
   refer to labels:

   * 在段落名前放置标签, 可以这样引用 ``:ref:`标签名```。 例如::

        .. _引用标签名:

        交叉引用段落
        --------------------------

        这里是段落文本.

        他指向段落本身, 查看 :ref:`引用标签名`.

     The ``:ref:`` role would then generate a link to the section, with the link
     title being "交叉引用段落".  This works just as well when
     section and reference are in different source files.

     Automatic labels also work with figures: given ::

        .. _my-figure:

        .. figure:: whatever

           Figure caption

     a reference ``:ref:`my-figure``` would insert a reference to the figure
     with link text "Figure caption".

     The same works for tables that are given an explicit caption using the
     :dudir:`table` directive.

   * 如果标签没有放到段落名前仍然可以引用，但你必须给链接一个明确的标题, 使用语法: ``:ref:`链接名 <标签名>```.

   Using :rst:role:`ref` is advised over standard reStructuredText links to sections
   (like ```Section title`_``) because it works across files, when section
   headings are changed, and for all builders that support cross-references.


交叉引用文件
---------------------------

.. versionadded:: 0.6

直接链接到文件:

.. rst:role:: doc

   链接到指定的文档; 以绝对或相对方式指定文件名。例如, 如果引用 ``:doc:`parrot``` 发生在文档 ``sketches/index`` 中, 将链接到 ``sketches/parrot``。 如果引用是 ``:doc:`/people``` 或者
   ``:doc:`../people```, 将链接到 ``people``。

   如果没有显式链接文本 (如: ``:doc:`Monty Python members </people>```), 链接的字幕将是文档的标题.


引用下载文件
------------------------------

.. versionadded:: 0.6

.. rst:role:: download

   This role lets you link to files within your source tree that are not reST
   documents that can be viewed, but files that can be downloaded.

   When you use this role, the referenced file is automatically marked for
   inclusion in the output when building (obviously, for HTML output only).
   All downloadable files are put into the ``_downloads`` subdirectory of the
   output directory; duplicate filenames are handled.

   An example::

      See :download:`this example script <../example.py>`.

   The given filename is usually relative to the directory the current source
   file is contained in, but if it absolute (starting with ``/``), it is taken
   as relative to the top source directory.

   The ``example.py`` file will be copied to the output directory, and a
   suitable link generated to it.


交叉引用其他兴趣项
-----------------------------------------

The following roles do possibly create a cross-reference, but do not refer to
objects:

.. rst:role:: envvar

   An environment variable.  Index entries are generated.  Also generates a link
   to the matching :rst:dir:`envvar` directive, if it exists.

.. rst:role:: token

   The name of a grammar token (used to create links between
   :rst:dir:`productionlist` directives).

.. rst:role:: keyword

   The name of a keyword in Python.  This creates a link to a reference label
   with that name, if it exists.

.. rst:role:: option

   A command-line option to an executable program.  The leading hyphen(s) must
   be included.  This generates a link to a :rst:dir:`option` directive, if it
   exists.


以下角色创建一个交叉引用到术语词汇表中:

.. rst:role:: term

   Reference to a term in the glossary.  The glossary is created using the
   ``glossary`` directive containing a definition list with terms and
   definitions.  It does not have to be in the same file as the ``term`` markup,
   for example the Python docs have one global glossary in the ``glossary.rst``
   file.

   If you use a term that's not explained in a glossary, you'll get a warning
   during build.


其他语义标签
~~~~~~~~~~~~~~~~~~~~~

以下角色没有做什么特别的东西，除了以不同的风格格式化文本:

.. rst:role:: abbr

   An abbreviation.  If the role content contains a parenthesized explanation,
   it will be treated specially: it will be shown in a tool-tip in HTML, and
   output only once in LaTeX.

   Example: ``:abbr:`LIFO (last-in, first-out)```.

   .. versionadded:: 0.6

.. rst:role:: command

   操作系统级命令, 如 ``rm``.

.. rst:role:: dfn

   Mark the defining instance of a term in the text.  (No index entries are
   generated.)

.. rst:role:: file

   The name of a file or directory.  Within the contents, you can use curly
   braces to indicate a "variable" part, for example::

      ... is installed in :file:`/usr/lib/python2.{x}/site-packages` ...

   In the built documentation, the ``x`` will be displayed differently to
   indicate that it is to be replaced by the Python minor version.

.. rst:role:: guilabel

   Labels presented as part of an interactive user interface should be marked
   using ``guilabel``.  This includes labels from text-based interfaces such as
   those created using :mod:`curses` or other text-based libraries.  Any label
   used in the interface should be marked with this role, including button
   labels, window titles, field names, menu and menu selection names, and even
   values in selection lists.

   .. versionchanged:: 1.0
      An accelerator key for the GUI label can be included using an ampersand;
      this will be stripped and displayed underlined in the output (example:
      ``:guilabel:`&Cancel```).  To include a literal ampersand, double it.

.. rst:role:: kbd

   Mark a sequence of keystrokes.  What form the key sequence takes may depend
   on platform- or application-specific conventions.  When there are no relevant
   conventions, the names of modifier keys should be spelled out, to improve
   accessibility for new users and non-native speakers.  For example, an
   *xemacs* key sequence may be marked like ``:kbd:`C-x C-f```, but without
   reference to a specific application or platform, the same sequence should be
   marked as ``:kbd:`Control-x Control-f```.

.. rst:role:: mailheader

   The name of an RFC 822-style mail header.  This markup does not imply that
   the header is being used in an email message, but can be used to refer to any
   header of the same "style."  This is also used for headers defined by the
   various MIME specifications.  The header name should be entered in the same
   way it would normally be found in practice, with the camel-casing conventions
   being preferred where there is more than one common usage. For example:
   ``:mailheader:`Content-Type```.

.. rst:role:: makevar

   The name of a :command:`make` variable.

.. rst:role:: manpage

   A reference to a Unix manual page including the section,
   e.g. ``:manpage:`ls(1)```.

.. rst:role:: menuselection

   Menu selections should be marked using the ``menuselection`` role.  This is
   used to mark a complete sequence of menu selections, including selecting
   submenus and choosing a specific operation, or any subsequence of such a
   sequence.  The names of individual selections should be separated by
   ``-->``.

   For example, to mark the selection "Start > Programs", use this markup::

      :menuselection:`Start --> Programs`

   When including a selection that includes some trailing indicator, such as the
   ellipsis some operating systems use to indicate that the command opens a
   dialog, the indicator should be omitted from the selection name.

   ``menuselection`` also supports ampersand accelerators just like
   :rst:role:`guilabel`.

.. rst:role:: mimetype

   The name of a MIME type, or a component of a MIME type (the major or minor
   portion, taken alone).

.. rst:role:: newsgroup

   新闻组的名称.

.. rst:role:: program

   The name of an executable program.  This may differ from the file name for
   the executable for some platforms.  In particular, the ``.exe`` (or other)
   extension should be omitted for Windows programs.

.. rst:role:: regexp

   正则表达式。引号不包括在内。

.. rst:role:: samp

   A piece of literal text, such as code.  Within the contents, you can use
   curly braces to indicate a "variable" part, as in :rst:role:`file`.  For
   example, in ``:samp:`print 1+{variable}```, the part ``variable`` would be
   emphasized.

   If you don't need the "variable part" indication, use the standard
   ````code```` instead.

生成索引目录角色 :rst:role:`index` 。

以下角色生成外部链接:

.. rst:role:: pep

   A reference to a Python Enhancement Proposal.  This generates appropriate
   index entries. The text "PEP *number*\ " is generated; in the HTML output,
   this text is a hyperlink to an online copy of the specified PEP.  You can
   link to a specific section by saying ``:pep:`number#anchor```.

.. rst:role:: rfc

   A reference to an Internet Request for Comments.  This generates appropriate
   index entries. The text "RFC *number*\ " is generated; in the HTML output,
   this text is a hyperlink to an online copy of the specified RFC.  You can
   link to a specific section by saying ``:rfc:`number#anchor```.


Note that there are no special roles for including hyperlinks as you can use
the standard reST markup for that purpose.


.. _default-substitutions:

替换
~~~~

The documentation system provides three substitutions that are defined by default.
They are set in the build configuration file.

.. describe:: |release|

   Replaced by the project release the documentation refers to.  This is meant
   to be the full version string including alpha/beta/release candidate tags,
   e.g. ``2.5.2b3``.  Set by :confval:`release`.

.. describe:: |version|

   Replaced by the project version the documentation refers to. This is meant to
   consist only of the major and minor version parts, e.g. ``2.5``, even for
   version 2.5.1.  Set by :confval:`version`.

.. describe:: |today|

   Replaced by either today's date (the date on which the document is read), or
   the date set in the build configuration file.  Normally has the format
   ``April 14, 2007``.  Set by :confval:`today_fmt` and :confval:`today`.
