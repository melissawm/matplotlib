.. redirect-from:: /devel/document

.. _documenting-matplotlib:
.. _document-build:

*******************
Build Documentation
*******************

All documentation is built from the :file:`doc/`.  The :file:`doc/`
directory contains configuration files for Sphinx and reStructuredText
(ReST_; ``.rst``) files that are rendered to documentation pages.

General file structure
======================
Documentation is created in three ways.  First, API documentation
(:file:`doc/api`) is created by Sphinx_ from
the docstrings of the classes in the Matplotlib library.  Except for
:file:`doc/api/api_changes/`,  ``.rst`` files in :file:`doc/api` are created
when the documentation is built.  See :ref:`writing-docstrings`.

Second, our example pages, tutorials, and some of the narrative documentation
are created by `Sphinx Gallery`_.  Sphinx Gallery converts example Python files
to ``*.rst`` files with the result of Matplotlib plot calls as embedded images.
See :ref:`writing-examples-and-tutorials`.

Third, Matplotlib has informative documentation written in ReST_ in subdirectories of
:file:`doc`. General and historical information about the project is in :file:`doc/project`,
the installation guide is in :file:`doc/install`, and release notes are managed in
:file:`doc/release`. Maintenance documentation is in :file:`doc/devel` and the website
always redirects to the latest version of these documents. We also maintain a list of
external resources in :file:`doc/users/resources/index.rst`. See
:ref:`writing-rest-pages`.

.. note::

  Don't directly edit the ``.rst`` files in :file:`doc/plot_types`,
  :file:`doc/gallery`,  :file:`doc/tutorials`, and :file:`doc/api`
  (excepting :file:`doc/api/api_changes/`).  Sphinx_ regenerates
  files in these directories when building documentation.

Set up the build
================

The documentation for Matplotlib is generated from reStructuredText (ReST_)
using the Sphinx_ documentation generation tool.

To build the documentation you will need to
:ref:`set up Matplotlib for development <installing_for_devs>`. Note in
particular the :ref:`additional dependencies <doc-dependencies>` required to
build the documentation.

Build the docs
==============

The documentation sources are found in the :file:`doc/` directory.
The configuration file for Sphinx is :file:`doc/conf.py`. It controls which
directories Sphinx parses, how the docs are built, and how the extensions are
used. To build the documentation in html format, cd into :file:`doc/` and run:

.. code-block:: sh

   make html

.. note::

   Since the documentation is very large, the first build may take 10-20 minutes,
   depending on your machine.  Subsequent builds will be faster.

Build options
-------------

Other useful invocations include

.. list-table::
  :widths: 30 30 40
  :header-rows: 1
  :stub-columns: 1

  * - invocation
    - description
    - notes
  * - ``make html-noplot``
    - skip generation of the gallery images
    -
  * - ``make html-skip-subdirs``
    - skip specific subdirectories
    - If a gallery directory is skipped, the gallery images are not generated.  The first
      time this is run, it creates ``.mpl_skip_subdirs.yaml`` which can be edited to add
      or remove subdirectories
  * - ``make clean``
    - Delete built files.
    - May help if you get errors about missing paths or broken links.
  * - ``make latexpdf``
    - Build pdf docs
    -

The ``SPHINXOPTS`` variable is set to ``-W --keep-going`` by default to build
the complete docs but exit with exit status 1 if there are warnings.  To unset
it, set
the variable to a blank space. On Windows, set the options as environment variables.

.. tab-set::
  :sync-group: category

  .. tab-item:: Linux & macOS
    :sync: linux

    .. code-block:: sh

      make SPHINXOPTS= html

  .. tab-ITEM:: Windows
    :sync: windows

    .. code-block:: bat

      set SPHINXOPTS= & make html

You can use the ``O`` variable to set additional options:

* ``make O=-j4 html`` runs a parallel build with 4 processes.
* ``make O=-Dplot_formats=png:100 html`` saves figures in low resolution.

Multiple options can be combined, e.g.:

.. tab-set::
  :sync-group: category

  .. tab-item:: Linux & macOS
    :sync: linux

    .. code-block:: sh

      make SPHINXOPTS= O='-j4 -Dplot_formats=png:100' html

  .. tab-ITEM:: Windows
    :sync: windows

    .. code-block:: bat

      set SPHINXOPTS= & set O=-j4 -Dplot_formats=png:100 & make html

Show locally built docs
=======================

The built docs are available in the folder :file:`build/html`. A shortcut
for opening them in your default browser is:

.. code-block:: sh

   make show

.. _ReST: https://docutils.sourceforge.io/rst.html
.. _Sphinx: http://www.sphinx-doc.org
.. _`Sphinx Gallery`: https://sphinx-gallery.readthedocs.io/en/latest/

Theme
=====

Matplotlib has a few subprojects that share the same navbar and style, so these
are centralized as a sphinx theme at
`mpl_sphinx_theme <https://github.com/matplotlib/mpl-sphinx-theme>`_.  Changes to the
style or top bar should be made there to propagate across all subprojects.
