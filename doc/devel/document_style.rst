.. redirect-from:: /devel/style_guide

.. _document_style:

***********
Style guide
***********

This guide contains best practices for the language and formatting of Matplotlib
documentation.

.. seealso::

    For more information about contributing, see the :ref:`documenting-matplotlib`
    section.

Expository language
===================

For explanatory writing, the following guidelines are for clear and concise
language use.

Terminology
-----------

There are several key terms in Matplotlib that are standards for
reliability and consistency in documentation. They are not interchangeable.

.. table::
  :widths: 15, 15, 35, 35

  +------------------+--------------------------+--------------+--------------+
  | Term             | Description              | Correct      | Incorrect    |
  +==================+==========================+==============+==============+
  | |Figure|         | Matplotlib working space | - *For       | - "The figure|
  |                  | for programming.         |   Matplotlib |   is the     |
  |                  |                          |   objects*:  |   working    |
  |                  |                          |   Figure,    |   space for  |
  |                  |                          |   "The Figure|   visuals."  |
  |                  |                          |   is the     | - "Methods in|
  |                  |                          |   working    |   the figure |
  |                  |                          |   space for  |   provide the|
  |                  |                          |   the visual.|   visuals."  |
  |                  |                          | - *Referring | - "The       |
  |                  |                          |   to class*: |   |Figure|   |
  |                  |                          |   |Figure|,  |   Four       |
  |                  |                          |   "Methods   |   leglock is |
  |                  |                          |   within the |   a wrestling|
  |                  |                          |   |Figure|   |   move."     |
  |                  |                          |   provide the|              |
  |                  |                          |   visuals."  |              |
  |                  |                          | - *General   |              |
  |                  |                          |   language*: |              |
  |                  |                          |   figure,    |              |
  |                  |                          |   "Michelle  |              |
  |                  |                          |   Kwan is a  |              |
  |                  |                          |   famous     |              |
  |                  |                          |   figure     |              |
  |                  |                          |   skater."   |              |
  +------------------+--------------------------+--------------+--------------+
  | |Axes|           | Subplots within Figure.  | - *For       | - "The axes  |
  |                  | Contains plot elements   |   Matplotlib |   methods    |
  |                  | and is responsible for   |   objects*:  |   transform  |
  |                  | plotting and configuring |   Axes, "An  |   the data." |
  |                  | additional details.      |   Axes is a  | - "Each      |
  |                  |                          |   subplot    |   |Axes| is  |
  |                  |                          |   within the |   specific to|
  |                  |                          |   Figure."   |   a Figure." |
  |                  |                          | - *Referring | - "The       |
  |                  |                          |   to class*: |   musicians  |
  |                  |                          |   |Axes|,    |   on stage   |
  |                  |                          |   "Each      |   call their |
  |                  |                          |   |Axes| is  |   guitars    |
  |                  |                          |   specific to|   Axes."     |
  |                  |                          |   one        | - "The point |
  |                  |                          |   Figure."   |   where the  |
  |                  |                          | - *General   |   Axes meet  |
  |                  |                          |   language*: |   is the     |
  |                  |                          |   axes, "Both|   origin of  |
  |                  |                          |   loggers and|   the        |
  |                  |                          |   lumberjacks|   coordinate |
  |                  |                          |   use axes to|   system."   |
  |                  |                          |   chop wood."|              |
  |                  |                          |   OR "There  |              |
  |                  |                          |   are no     |              |
  |                  |                          |   standard   |              |
  |                  |                          |   names for  |              |
  |                  |                          |   the        |              |
  |                  |                          |   coordinates|              |
  |                  |                          |   in the     |              |
  |                  |                          |   three      |              |
  |                  |                          |   axes."     |              |
  |                  |                          |   (Plural of |              |
  |                  |                          |   axis)      |              |
  +------------------+--------------------------+--------------+--------------+
  | |Artist|         | Broad variety of         | - *For       | - "Configure |
  |                  | Matplotlib objects that  |   Matplotlib |   the legend |
  |                  | display visuals.         |   objects*:  |   artist with|
  |                  |                          |   Artist,    |   its        |
  |                  |                          |   "Artists   |   respective |
  |                  |                          |   display    |   method."   |
  |                  |                          |   visuals and| - "There is  |
  |                  |                          |   are the    |   an         |
  |                  |                          |   visible    |   |Artist|   |
  |                  |                          |   elements   |   for that   |
  |                  |                          |   when       |   visual in  |
  |                  |                          |   rendering a|   the graph."|
  |                  |                          |   Figure."   | - "Some      |
  |                  |                          | - *Referring |   Artists    |
  |                  |                          |   to class*: |   became     |
  |                  |                          |   |Artist| , |   famous only|
  |                  |                          |   "Each      |   by         |
  |                  |                          |   |Artist|   |   accident." |
  |                  |                          |   has        |              |
  |                  |                          |   respective |              |
  |                  |                          |   methods and|              |
  |                  |                          |   functions."|              |
  |                  |                          | - *General   |              |
  |                  |                          |   language*: |              |
  |                  |                          |   artist,    |              |
  |                  |                          |   "The       |              |
  |                  |                          |   artist in  |              |
  |                  |                          |   the museum |              |
  |                  |                          |   is from    |              |
  |                  |                          |   France."   |              |
  +------------------+--------------------------+--------------+--------------+
  | |Axis|           | Human-readable single    | - *For       | - "Plot the  |
  |                  | dimensional object       |   Matplotlib |   graph onto |
  |                  | of reference marks       |   objects*:  |   the axis." |
  |                  | containing ticks, tick   |   Axis, "The | - "Each Axis |
  |                  | labels, spines, and      |   Axis for   |   is usually |
  |                  | edges.                   |   the bar    |   named after|
  |                  |                          |   chart is a |   the        |
  |                  |                          |   separate   |   coordinate |
  |                  |                          |   Artist."   |   which is   |
  |                  |                          |   (plural,   |   measured   |
  |                  |                          |   Axis       |   along it." |
  |                  |                          |   objects)   | - "In some   |
  |                  |                          | - *Referring |   computer   |
  |                  |                          |   to class*: |   graphics   |
  |                  |                          |   |Axis|,    |   contexts,  |
  |                  |                          |   "The       |   the        |
  |                  |                          |   |Axis|     |   ordinate   |
  |                  |                          |   contains   |   |Axis| may |
  |                  |                          |   respective |   be oriented|
  |                  |                          |   XAxis and  |   downwards."|
  |                  |                          |   YAxis      |              |
  |                  |                          |   objects."  |              |
  |                  |                          | - *General   |              |
  |                  |                          |   language*: |              |
  |                  |                          |   axis,      |              |
  |                  |                          |   "Rotation  |              |
  |                  |                          |   around a   |              |
  |                  |                          |   fixed axis |              |
  |                  |                          |   is a       |              |
  |                  |                          |   special    |              |
  |                  |                          |   case of    |              |
  |                  |                          |   rotational |              |
  |                  |                          |   motion."   |              |
  +------------------+--------------------------+--------------+--------------+
  | Axes interface   | Usage pattern in which   | - Axes       | - explicit   |
  |                  | one calls methods on     |   interface  |   interface  |
  |                  | Axes and Figure (and     | - call       | - object     |
  |                  | sometimes other Artist)  |   methods on |   oriented   |
  |                  | objects to configure the |   the Axes / | - OO-style   |
  |                  | plot.                    |   Figure     | - OOP        |
  |                  |                          |   object     |              |
  +------------------+--------------------------+--------------+--------------+
  | pyplot interface | Usage pattern in which   | - ``pyplot`` | - implicit   |
  |                  | one only calls `.pyplot` |   interface  |   interface  |
  |                  | functions to configure   | - call       | - MATLAB like|
  |                  | the plot.                |   ``pyplot`` | - Pyplot     |
  |                  |                          |   functions  |              |
  +------------------+--------------------------+--------------+--------------+

.. |Figure| replace:: :class:`~matplotlib.figure.Figure`
.. |Axes| replace:: :class:`~matplotlib.axes.Axes`
.. |Artist| replace:: :class:`~matplotlib.artist.Artist`
.. |Axis| replace:: :class:`~matplotlib.axis.Axis`


Headings
--------
We aim to follow the recommendations from the
`Python documentation <https://devguide.python.org/documenting/#sections>`_
and the `Sphinx reStructuredText documentation <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#sections>`_
for section markup characters, i.e.:

- ``#`` with overline, for parts. This is reserved for the main title in
  ``index.rst``. All other pages should start with "chapter" or lower.
- ``*`` with overline, for chapters
- ``=``, for sections
- ``-``, for subsections
- ``^``, for subsubsections
- ``"``, for paragraphs

This may not yet be applied consistently in existing docs.

Use `sentence case <https://apastyle.apa.org/style-grammar-guidelines/capitalization/sentence-case>`__
``Upper lower`` for section titles.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | Quick start guide                  | Quick Start Guide                  |
   +------------------------------------+------------------------------------+

Noun phrases and verb phrases are both acceptable for headings. Noun phrases
are preferred for higher-level headings and descriptive sections as they
simply state the content.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | Bug triage and issue curation      | Triage bugs and curate issues      |
   +------------------------------------+------------------------------------+

Verb phrases are preferred for instructive and action-oriented sections; in
particular when they cover steps in a process, such as the subsections in
:ref:`installing_for_devs`.

Use the second-person imperative form of the verb rather than the gerund form.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | Fork the Matplotlib repository     | Forking the Matplotlib repository  |
   +------------------------------------+------------------------------------+


Grammar
-------

Subject
^^^^^^^
Use second-person imperative sentences for directed instructions specifying an
action. Second-person pronouns are for individual-specific contexts and
possessive reference.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | Install Matplotlib from the source | You can install Matplotlib from the|
   | directory using the Python ``pip`` | source directory. You can find     |
   | installer program. Depending on    | additional support if you are      |
   | your operating system, you may need| having trouble with your           |
   | additional support.                | installation.                      |
   +------------------------------------+------------------------------------+

Tense
^^^^^
Use present simple tense for explanations. Avoid future tense and other modal
or auxiliary verbs when possible.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | The fundamental ideas behind       | Matplotlib will take data and      |
   | Matplotlib for visualization       | transform it through functions and |
   | involve taking data and            | methods. They can generate many    |
   | transforming it through functions  | kinds of visuals. These will be the|
   | and methods.                       | fundamentals for using Matplotlib. |
   +------------------------------------+------------------------------------+

Voice
^^^^^
Write in active sentences. Passive voice is best for situations or conditions
related to warning prompts.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | The function ``plot`` generates the| The graph is generated by the      |
   | graph.                             | ``plot`` function.                 |
   +------------------------------------+------------------------------------+
   | An error message is returned by the| You will see an error message from |
   | function if there are no arguments.| the function if there are no       |
   |                                    | arguments.                         |
   +------------------------------------+------------------------------------+

Sentence structure
^^^^^^^^^^^^^^^^^^
Write with short sentences using Subject-Verb-Object order regularly. Limit
coordinating conjunctions in sentences. Avoid pronoun references and
subordinating conjunctive phrases.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | The ``pyplot`` module in Matplotlib| The ``pyplot`` module in Matplotlib|
   | is a collection of functions. These| is a collection of functions which |
   | functions create, manage, and      | create, manage, and manipulate the |
   | manipulate the current Figure and  | current Figure and plotting area.  |
   | plotting area.                     |                                    |
   +------------------------------------+------------------------------------+
   | The ``plot`` function plots data   | The ``plot`` function plots data   |
   | to the respective Axes. The Axes   | within its respective Axes for its |
   | corresponds to the respective      | respective Figure.                 |
   | Figure.                            |                                    |
   +------------------------------------+------------------------------------+
   | The implicit approach is a         | Users that wish to have convenient |
   | convenient shortcut for            | shortcuts for generating plots use |
   | generating simple plots.           | the implicit approach.             |
   +------------------------------------+------------------------------------+


Formatting
==========

It is useful to strive for consistency in the Matplotlib documentation. The
following guidelines specify how to incorporate code and use appropriate
formatting for Matplotlib documentation.

Code examples
-------------
Examples of Python code have comments before or on the same line.

.. table::
   :width: 100%
   :widths: 50, 50

   +---------------------------------------+---------------------------------+
   | Correct                               | Incorrect                       |
   +=======================================+=================================+
   | ::                                    | ::                              |
   |                                       |                                 |
   |    # Data                             |    years = [2006, 2007, 2008]   |
   |    years = [2006, 2007, 2008]         |    # Data                       |
   +---------------------------------------+                                 |
   | ::                                    |                                 |
   |                                       |                                 |
   |    years = [2006, 2007, 2008]  # Data |                                 |
   +---------------------------------------+---------------------------------+

Outputs
-------
When generating visuals with Matplotlib using ``.py`` files in examples,
display the visual with `matplotlib.pyplot.show` to display the visual.
Keep the documentation clear of Python output lines.

.. table::
   :width: 100%
   :widths: 50, 50

   +------------------------------------+------------------------------------+
   | Correct                            | Incorrect                          |
   +====================================+====================================+
   | ::                                 | ::                                 |
   |                                    |                                    |
   |    plt.plot([1, 2, 3], [1, 2, 3])  |    plt.plot([1, 2, 3], [1, 2, 3])  |
   |    plt.show()                      |                                    |
   +------------------------------------+------------------------------------+
   | ::                                 | ::                                 |
   |                                    |                                    |
   |    fig, ax = plt.subplots()        |    fig, ax = plt.subplots()        |
   |    ax.plot([1, 2, 3], [1, 2, 3])   |    ax.plot([1, 2, 3], [1, 2, 3])   |
   |    fig.show()                      |                                    |
   +------------------------------------+------------------------------------+

.. _docstring_formatting:

Docstring formatting conventions
--------------------------------

The basic docstring conventions are covered in the `numpydoc docstring guide`_
and the Sphinx_ documentation.  Some Matplotlib-specific formatting conventions
to keep in mind:

.. _`numpydoc docstring guide`: https://numpydoc.readthedocs.io/en/latest/format.html
.. _Sphinx: http://www.sphinx-doc.org

Quote positions
^^^^^^^^^^^^^^^

The quotes for single line docstrings are on the same line (pydocstyle D200)::

    def get_linewidth(self):
        """Return the line width in points."""

The quotes for multi-line docstrings are on separate lines (pydocstyle D213)::

        def set_linestyle(self, ls):
        """
        Set the linestyle of the line.

        [...]
        """

Function arguments
^^^^^^^^^^^^^^^^^^

Function arguments and keywords within docstrings should be referred to
using the ``*emphasis*`` role. This will keep Matplotlib's documentation
consistent with Python's documentation:

.. code-block:: rst

  If *linestyles* is *None*, the default is 'solid'.

Do not use the ```default role``` or the ````literal```` role:

.. code-block:: rst

  Neither `argument` nor ``argument`` should be used.

Quotes for strings
^^^^^^^^^^^^^^^^^^

Matplotlib does not have a convention whether to use single-quotes or
double-quotes.  There is a mixture of both in the current code.

Use simple single or double quotes when giving string values, e.g.

.. code-block:: rst

  If 'tight', try to figure out the tight bbox of the figure.

  No ``'extra'`` literal quotes.

The use of extra literal quotes around the text is discouraged. While they
slightly improve the rendered docs, they are cumbersome to type and difficult
to read in plain-text docs.

Parameter type descriptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The main goal for parameter type descriptions is to be readable and
understandable by humans. If the possible types are too complex use a
simplification for the type description and explain the type more
precisely in the text.

We do not use formal type annotation syntax for type descriptions in
docstrings; e.g. we use ``list of str`` rather than  ``list[str]``; we
use ``int or str`` rather than ``int | str`` or ``Union[int, str]``.

Generally, the `numpydoc docstring guide`_ conventions apply. The following
rules expand on them where the numpydoc conventions are not specific.

Use ``float`` for a type that can be any number.

Use ``(float, float)`` to describe a 2D position. The parentheses should be
included to make the tuple-ness more obvious.

Use ``array-like`` for homogeneous numeric sequences, which could
typically be a numpy.array. Dimensionality may be specified using ``2D``,
``3D``, ``n-dimensional``. If you need to have variables denoting the
sizes of the dimensions, use capital letters in brackets
(``(M, N) array-like``). When referring to them in the text they are easier
read and no special formatting is needed. Use ``array`` instead of
``array-like`` for return types if the returned object is indeed a numpy array.

``float`` is the implicit default dtype for array-likes. For other dtypes
use ``array-like of int``.

Some possible uses::

  2D array-like
  (N,) array-like
  (M, N) array-like
  (M, N, 3) array-like
  array-like of int

Non-numeric homogeneous sequences are described as lists, e.g.::

  list of str
  list of `.Artist`

Reference types
^^^^^^^^^^^^^^^

Generally, the rules from :ref:`referring-to-other-code` apply. More specifically:

Use full references ```~matplotlib.colors.Normalize``` with an
abbreviation tilde in parameter types. While the full name helps the
reader of plain text docstrings, the HTML does not need to show the full
name as it links to it. Hence, the ``~``-shortening keeps it more readable.

Use abbreviated links ```.Normalize``` in the text.

.. code-block:: rst

   norm : `~matplotlib.colors.Normalize`, optional
        A `.Normalize` instance is used to scale luminance data to 0, 1.

Default values
^^^^^^^^^^^^^^

As opposed to the numpydoc guide, parameters need not be marked as
*optional* if they have a simple default:

- use ``{name} : {type}, default: {val}`` when possible.
- use ``{name} : {type}, optional`` and describe the default in the text if
  it cannot be explained sufficiently in the recommended manner.

The default value should provide semantic information targeted at a human
reader. In simple cases, it restates the value in the function signature.
If applicable, units should be added.

.. code-block:: rst

   Prefer:
       interval : int, default: 1000ms
   over:
       interval : int, default: 1000

If *None* is only used as a sentinel value for "parameter not specified", do
not document it as the default. Depending on the context, give the actual
default, or mark the parameter as optional if not specifying has no particular
effect.

.. code-block:: rst

   Prefer:
       dpi : float, default: :rc:`figure.dpi`
   over:
       dpi : float, default: None

   Prefer:
       textprops : dict, optional
           Dictionary of keyword parameters to be passed to the
           `~matplotlib.text.Text` instance contained inside TextArea.
   over:
       textprops : dict, default: None
           Dictionary of keyword parameters to be passed to the
           `~matplotlib.text.Text` instance contained inside TextArea.

Wrap parameter lists
^^^^^^^^^^^^^^^^^^^^

Long parameter lists should be wrapped using a ``\`` for continuation and
starting on the new line without any indent (no indent because pydoc will
parse the docstring and strip the line continuation so that indent would
result in a lot of whitespace within the line):

.. code-block:: python

  def add_axes(self, *args, **kwargs):
      """
      ...

      Parameters
      ----------
      projection : {'aitoff', 'hammer', 'lambert', 'mollweide', 'polar', \
  'rectilinear'}, optional
          The projection type of the axes.

      ...
      """

Alternatively, you can describe the valid parameter values in a dedicated
section of the docstring.

rcParams
^^^^^^^^

rcParams can be referenced with the custom ``:rc:`` role:
:literal:`:rc:\`foo\`` yields ``rcParams["foo"] = 'default'``, which is a link
to the :file:`matplotlibrc` file description.


Additional resources
====================
This style guide is not a comprehensive standard. For a more thorough
reference of how to contribute to documentation, see the links below. These
resources contain common best practices for writing documentation.


* `Python Developer's Guide <https://devguide.python.org/documenting/#documenting-python>`_
* `Google Developer Style Guide <https://developers.google.com/style>`_
* `IBM Style Guide <https://www.oreilly.com/library/view/the-ibm-style/9780132118989/>`_
* `Red Hat Style Guide <https://stylepedia.net/style/#grammar>`_
