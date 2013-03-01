.. _basic-domain-markup:

基础标签
------------

Most domains provide a number of :dfn:`object description directives`, used to
describe specific objects provided by modules.  Each directive requires one or
more signatures to provide basic information about what is being described, and
the content should be the description.  The basic version makes entries in the
general index; if no index entry is desired, you can give the directive option
flag ``:noindex:``.  An example using a Python domain directive::

   .. py:function:: spam(eggs)
                    ham(eggs)

      Spam or ham the foo.

This describes the two Python functions ``spam`` and ``ham``.  (Note that when
signatures become too long, you can break them if you add a backslash to lines
that are continued in the next line.  Example::

   .. py:function:: filterwarnings(action, message='', category=Warning, \
                                   module='', lineno=0, append=False)
      :noindex:

(This example also shows how to use the ``:noindex:`` flag.)

The domains also provide roles that link back to these object descriptions.  For
example, to link to one of the functions described in the example above, you
could say ::

   The function :py:func:`spam` does a similar thing.

As you can see, both directive and role names contain the domain name and the
directive name.

.. rubric:: Default Domain

To avoid having to writing the domain name all the time when you e.g. only
describe Python objects, a default domain can be selected with either the config
value :confval:`primary_domain` or this directive:

.. rst:directive:: .. default-domain:: name

   Select a new default domain.  While the :confval:`primary_domain` selects a
   global default, this only has an effect within the same file.

If no other default is selected, the Python domain (named ``py``) is the default
one, mostly for compatibility with documentation written for older versions of
Sphinx.

Directives and roles that belong to the default domain can be mentioned without
giving the domain name, i.e. ::

   .. function:: pyfunc()

      Describes a Python function.

   Reference to :func:`pyfunc`.
