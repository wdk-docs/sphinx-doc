.. _standard-domain:

标准域
-------------------

The so-called "standard" domain collects all markup that doesn't warrant a
domain of its own.  Its directives and roles are not prefixed with a domain
name.

The standard domain is also where custom object descriptions, added using the
:func:`~sphinx.application.Sphinx.add_object_type` API, are placed.

There is a set of directives allowing documenting command-line programs:

.. rst:directive:: .. option:: name args, name args, ...

   Describes a command line option or switch.  Option argument names should be
   enclosed in angle brackets.  Example::

      .. option:: -m <module>, --module <module>

         Run a module as a script.

   The directive will create a cross-reference target named after the *first*
   option, referencable by :rst:role:`option` (in the example case, you'd use
   something like ``:option:`-m```).

.. rst:directive:: .. envvar:: name

   Describes an environment variable that the documented code or program uses or
   defines.  Referencable by :rst:role:`envvar`.

.. rst:directive:: .. program:: name

   Like :rst:dir:`py:currentmodule`, this directive produces no output.  Instead, it
   serves to notify Sphinx that all following :rst:dir:`option` directives
   document options for the program called *name*.

   If you use :rst:dir:`program`, you have to qualify the references in your
   :rst:role:`option` roles by the program name, so if you have the following
   situation ::

      .. program:: rm

      .. option:: -r

         Work recursively.

      .. program:: svn

      .. option:: -r revision

         Specify the revision to work upon.

   then ``:option:`rm -r``` would refer to the first option, while
   ``:option:`svn -r``` would refer to the second one.

   The program name may contain spaces (in case you want to document subcommands
   like ``svn add`` and ``svn commit`` separately).

   .. versionadded:: 0.5


There is also a very generic object description directive, which is not tied to
any domain:

.. rst:directive:: .. describe:: text
               .. object:: text

   This directive produces the same formatting as the specific ones provided by
   domains, but does not create index entries or cross-referencing targets.
   Example::

      .. describe:: PAPER

         You can set this variable to select a paper size.
