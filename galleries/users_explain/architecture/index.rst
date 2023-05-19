.. _architecture:

=======================
Matplotlib architecture
=======================

**Who is this page for?**

The audience for this page is advanced users and contributors (including
maintainers) who want to understand the reasoning behind the Matplotlib
architecture decisions and current implementation.

Overview of the Matplotlib Architecture
---------------------------------------

The top-level Matplotlib object that contains and manages all of the elements in
a given graphic is the ``Figure``. It keeps track of all the child
:class:`~matplotlib.axes.Axes`, a group of 'special' Artists (titles, figure
legends, colorbars, etc), and even nested subfigures.

From `[Hunter, Droettboom 2012] <https://www.aosabook.org/en/matplotlib.html>`_:

  One of the core architectural tasks ``matplotlib`` must solve is implementing
  a framework for representing and manipulating a ``Figure`` that is isolated
  from the act of rendering the ``Figure`` to a user interface window or
  hardcopy. This makes it possible to build increasingly sophisticated features
  and logic into the ``Figure``, while keeping the "backends", or output
  devices, relatively simple. ``matplotlib`` encapsulates not just the drawing
  interfaces to allow rendering to multiple devices, but also the basic event
  handling and windowing of most popular user interface toolkits. Because of
  this, users can create fairly rich interactive graphics and toolkits
  incorporating mouse and keyboard input that can be plugged without
  modification into the
  :ref:`different user interface toolkits we support <backends>`.

To accomplish this, Matplotlib is logically separated into three layers, which
can be viewed as a stack. Each layer that sits above another layer knows how to
talk to the layer below it, but the lower layer is not aware of the layers above
it.

These layers are:

* The **API layer**, which provides a lighter scripting interface (``pyplot``)
  to accomplish simpler tasks, and an explicit object-oriented "Axes" interface.
  This is the topmost layer in the stack.
* The **artist layer**, which is where most of the heavy lifting happens. Every
  object rendered on a Matplotlib figure is an instance of ``Artist``;
* The **backend layer**, at the bottom of the stack, provides concrete
  implementations of abstract interface classes that translate rendering
  commands into the preferred user interfaces and output formats.

This organization makes it possible to separate the ``Figure`` representation
and manipulation from the act of rendering it.

.. plot::
   :align: center

   import matplotlib.pyplot as plt
   text_kwargs = dict(ha='center', va='center', fontsize=22, color='tab:blue')
   fig, ax = plt.subplots(3, 1, figsize=(5, 3))
   for i in range(3):
       ax[i].set_xticks([])
       ax[i].set_yticks([])
       ax[i].set_facecolor('whitesmoke')
   ax[0].text(0.5, 0.5, 'API layer', **text_kwargs)
   ax[1].text(0.5, 0.5, 'Artist layer', **text_kwargs)
   ax[2].text(0.5, 0.5, 'Backend layer', **text_kwargs)

The API layer
~~~~~~~~~~~~~

Matplotlib has two major application interfaces, or styles of using the library:

- An explicit "Axes" interface that uses methods on a Figure or Axes object to
  create other Artists, and build a visualization step by step.  This has also
  been called an "object-oriented" interface.
- An implicit "pyplot" interface that keeps track of the last Figure and Axes
  created, and adds Artists to the object it thinks the user wants.

In addition, a number of downstream libraries (like `pandas` and xarray_) offer
a ``plot`` method implemented directly on their data classes so that users can
call ``data.plot()``.

See :ref:`api_interfaces` and :doc:`../../../devel/MEP/MEP27` for more details.
See also https://github.com/matplotlib/mpl-gui.

.. _artist-layer:

Artist layer
~~~~~~~~~~~~

The ``Artist`` is the object that knows how to take the ``Renderer`` (the
paintbrush) and put ink on the canvas. Everything you see in a matplotlib
``Figure`` is an ``Artist`` instance; the title, the lines, the tick labels, the
images, and so on all correspond to individual ``Artist`` instances arranged in
a hierarchy. The base class is `matplotlib.artist.Artist`, which contains
attributes that every ``Artist`` shares: the transformation which translates the
artist coordinate system to the canvas coordinate system, the visibility, the
clip box which defines the region the artist can paint into, the label, and the
interface to handle user interaction.

The essential method that all ``Artist`` subclasses must implement is ``draw``,
which is responsible for the coupling between the ``Artist`` hierarchy in the
``Figure`` and the chosen backend. The
Artist doesn't know what kind of backend the renderer is going to draw onto but
it does know the Renderer API and will call the appropriate method.

There are two types of Artists: *primitive* and *composite* artists.

**Primitive artists** represent the kinds of objects you see in a plot: Line2D,
Rectangle, Circle, and Text. Composite artists are collections of Artists such
as the Axis, Tick, Axes, and Figure. Each composite artist may contain other
composite artists as well as primitive artists. For example, the Figure contains
one or more composite Axes and the background of the Figure is a primitive
Rectangle.

Backend Layer
~~~~~~~~~~~~~

At the bottom of the stack is the :ref:`backend layer <backends>`, which
provides concrete implementations of the abstract interface classes:

* ``FigureCanvas`` encapsulates the concept of a surface to draw onto (e.g. "the
  paper").
* ``Renderer`` does the drawing (e.g. "the paintbrush").
* ``Event`` handles user inputs such as keyboard and mouse events.

The abstract base class ``FigureCanvas`` has concrete implementations for all
user interface toolkits, such as Qt and GTK. The abstract base classes reside in
`matplotlib.backend_bases` and all of the derived classes live in dedicated
modules (see :mod:`matplotlib.backends`).

The ``Renderer`` provides a low-level drawing interface, and implements methods
such as ``draw_path``, ``draw_image`` and ``draw_gouraud_triangles`` (see
`matplotlib.backend_bases.RendererBase`). Most pixel-based backends in
Matplotlib use the C++ template library *Anti-Grain Geometry* or "agg"
[Shemanarev_]. The ``FigureCanvas`` and the ``Renderer`` handle all the details
of talking to user interface toolkits like wxPython or drawing languages like
PostScript®, while the ``Artist`` handles all the high level constructs like
representing and laying out the figure, text, and lines.

The matplotlib ``Event`` framework maps underlying UI events like key presses,
panning and zooming of figures and mouse movements in a "GUI neutral way."
Although the event handling API is GUI neutral, it is based on the GTK model,
which was the first user interface Matplotlib supported. The events also
understand the Matplotlib coordinate system, and report event locations in both
pixel and data coordinates. See :ref:`event_handling` for details.

Further reading
---------------

* John Hunter and Michael Droettboom, `*The Architecture of Open Source Applications (Volume 2), matplotlib* <https://www.aosabook.org/en/matplotlib.html>`_.

.. _blog: https://medium.datadriveninvestor.com/data-visualization-with-python-matplotlib-architecture-6b05af533569
.. _Shemanarev: Maxim Shemanarev. Anti-Grain Geometry: A high quality rendering engine for C++, 2002-2006.

.. _aos: https://www.aosabook.org/en/matplotlib.html
.. _blog: https://medium.datadriveninvestor.com/data-visualization-with-python-matplotlib-architecture-6b05af533569
.. _Shemanarev: Maxim Shemanarev. Anti-Grain Geometry: A high quality rendering engine for C++, 2002-2006.

.. _xarray: https://xarray.pydata.org


.. toctree::
    :maxdepth: 1

    Concept: Matplotlib Application Interfaces (APIs) <api_interfaces>
    Concept: Output backends <backends>
