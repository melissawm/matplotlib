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

From [`Hunter, Droettboom`_]:

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
images, and so on all correspond to individual ``Artist`` instances. The base
class is ``matplotlib.artist.Artist``, which contains attributes that every
``Artist`` shares. : the transformation which translates the artist coordinate
system to the canvas coordinate system (discussed in more detail below), the
visibility, the clip box which defines the region the artist can paint into, the
label, and the interface to handle user interaction such as "picking"; that is,
detecting when a mouse click happens over the artist.

There is a hierarchy between artists in the same ``Figure``.

The coupling between the ``Artist`` hierarchy and the backend happens in the
``draw`` method.

For example, in the mockup class below where we create SomeArtist which
subclasses Artist, the essential method that SomeArtist must implement is draw,
which is passed a renderer from the backend. The Artist doesn't know what kind
of backend the renderer is going to draw onto (PDF, SVG, GTK+ DrawingArea, etc.)
but it does know the Renderer API and will call the appropriate method
(draw_text or draw_path). Since the Renderer has a pointer to its canvas and
knows how to paint onto it, the draw method transforms the abstract
representation of the Artist to colors in a pixel buffer, paths in an SVG file,
or any other concrete representation.

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
modules like ``matplotlib.backends.backend_qt4agg``.

The job of the ``Renderer`` is to provide a low-level drawing interface for
putting ink onto the canvas. One of the design decisions that has worked quite
well for matplotlib is support for a core pixel-based renderer using the C++
template library *Anti-Grain Geometry* or "agg" [Shemanarev_]. This is a
high-performance library for rendering anti-aliased 2D graphics that produces
attractive images. matplotlib provides support for inserting pixel buffers
rendered by the agg backend into each user interface toolkit we support, so one
can get pixel-exact graphics across UIs and operating systems. Because the PNG
output matplotlib produces also uses the agg renderer, the hardcopy is identical
to the screen display, so what you see is what you get across UIs, operating
systems and PNG output.

The matplotlib ``Event`` framework maps underlying UI events like
``key-press-event`` or ``mouse-motion-event`` to the matplotlib classes
``KeyEvent`` or ``MouseEvent``. Users can connect to these events to callback
functions and interact with their figure and data; for example, to pick a data
point or group of points, or manipulate some aspect of the figure or its
constituents.

The abstraction of the underlying UI toolkit's event framework allows both
matplotlib developers and end-users to write UI event-handling code in a "write
once run everywhere" fashion. For example, the interactive panning and zooming
of matplotlib figures that works across all user interface toolkits is
implemented in the matplotlib event framework.

Further reading
---------------

.. _Hunter, Droettboom: `John Hunter and Michael Droettboom, *The Architecture of Open Source Applications (Volume 2), matplotlib* <https://www.aosabook.org/en/matplotlib.html>`_.`
.. _blog: https://medium.datadriveninvestor.com/data-visualization-with-python-matplotlib-architecture-6b05af533569
.. _Shemanarev: Maxim Shemanarev. Anti-Grain Geometry: A high quality rendering engine for C++, 2002-2006.

.. _xarray: https://xarray.pydata.org


.. toctree::
    :maxdepth: 1

    Concept: Matplotlib Application Interfaces (APIs) <api_interfaces>
    Concept: Output backends <backends>
