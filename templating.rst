.. _qtut_templating:

===================================
05: HTML Generation With Templating
===================================

Most web frameworks don't embed HTML in programming code. Instead,
they pass data into a templating system. In this step we look at the
basics of using HTML templates in Pyramid.

Background
==========

Ouch. We have been making our own ``Response`` and filling the response
body with HTML. You usually won't embed an HTML string directly in
Python, but instead, will use a templating language.

Pyramid doesn't mandate a particular database system, form library,
etc. It encourages replaceability. This applies equally to templating,
which is fortunate: developers have strong views about template
languages. As of Pyramid 1.5a2, Pyramid doesn't even bundle a template
language!

It does, however, have strong ties to Jinja2, Mako, and Chameleon. In
this step we see how to add ``pyramid_chameleon`` to your project,
then change your views to use templating.

Objectives
==========

- Enable the ``pyramid_chameleon`` Pyramid add-on

- Generate HTML from template files

- Connect the templates as "renderers" for view code

- Change the view code to simply return data

Steps
=====

#. Let's begin by using the previous package as a starting point for a
   new project:

   .. code-block:: bash

    $ cd ..; cp -r views templating; cd templating

#. This step depends on ``pyramid_chameleon``, so add it as a dependency
   in ``templating/setup.py``:

   .. literalinclude:: templating/setup.py
    :linenos:

#. Now we can activate the development-mode distribution:

   .. code-block:: bash

    $ $VENV/bin/python setup.py develop

#. We need to connect ``pyramid_chameleon`` as a renderer by making a
   call in the setup of ``templating/tutorial/__init__.py``:

   .. literalinclude:: templating/tutorial/__init__.py
    :linenos:

#. Our ``templating/tutorial/views.py`` no longer has HTML in it:

   .. literalinclude:: templating/tutorial/views.py
    :linenos:

#. Instead we have ``templating/tutorial/home.pt`` as a template:

   .. literalinclude:: templating/tutorial/home.pt
    :language: html

#. For convenience, change ``templating/development.ini`` to reload
   templates automatically with ``pyramid.reload_templates``:

   .. literalinclude:: templating/development.ini
    :language: ini

#. Run your Pyramid application with:

   .. code-block:: bash

    $ $VENV/bin/pserve development.ini --reload

#. Open http://localhost:6543/ and http://localhost:6543/howdy
   in your browser.

Analysis
========

Ahh, that looks better. We have a view that is focused on Python code.
Our ``@view_config`` decorator specifies a :term:`renderer` that points
our template file. Our view then simply returns data which is then
supplied to our template. Note that we used the same template for both
views.

Note the effect on testing. We can focus on having a data-oriented
contract with our view code.

Extra Credit
============

# What causes ``pyramid_chameleon`` to be fetched / installed?  Used
  as a renderer?

# What other options are available for templating?


.. seealso:: :ref:`pyramid:templates_chapter` and
   :ref:`pyramid:available_template_system_bindings`.
