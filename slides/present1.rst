Pelican Static Site Generation
==============================

Hi! Thanks for coming out.  You're great.  You really are.

----

History and Motivation
======================

* Collect notes and thoughts (profile?)
* Literate programming
* Real World Haskell - inline code samples and results
* Sage Math platform - replace $$$ systems

----

.. image:: https://www.sagemath.org/pix/sage_logo_new_l_hc_edgy-nq8.png

SageMath is a free open-source mathematics software system licensed under the GPL. 

*Mission*: Creating a viable free open source alternative to Magma, Maple, Mathematica and Matlab.

----

.. image:: https://www.sagemath.org/pix/sage_logo_new_l_hc_edgy-nq8.png

SageMath is a free open-source mathematics software system licensed under the GPL. 
It builds on top of many existing open-source packages: 

- NumPy, SciPy, matplotlib
- Sympy, Maxima
- GAP
- FLINT
- R and many more. 
  
Access their combined power through a common, Python-based language or directly via interfaces or wrappers.


----

.. image:: https://sagecell.sagemath.org/static/sagemathcell-logo.png?v=cee2c58e80f2ffd0968d7a8266fac283

SageMathCell project is an easy-to-use web interface to a free open-source mathematics software system SageMath.

It allows embedding Sage computations into any webpage.

----

2D Graphics - Random Data
=========================

.. sage-image:: random matrix eigenvalues
    :file: /pages/sage/overview.rst

----

2D Graphics - Region Plots
==========================

.. sage-image:: region plots
    :file: /pages/sage/overview.rst

----

2D Graphics - Density Plots
===========================

.. sage-image:: density plots
    :file: /pages/sage/overview.rst

----

Differential Equations
======================

.. sage-image:: euler method diffq
    :file: /pages/sage/overview.rst

----

Graph Theory
============

.. sage-image:: graph1
    :file: /pages/sage/overview.rst

----

Graph Theory
============

.. sage-image:: graph2
    :file: /pages/sage/overview.rst

----

Graph Theory
============

.. sage-image:: graph3
    :file: /pages/sage/overview.rst

----

Graph Theory
============

.. sage-image:: graph3 _ removing verts
    :file: /pages/sage/overview.rst

----

Graph Theory - Simple Graphs
============================

We can use PelicanSage to convert these individual blocks into content, using the ipynb directive specifying the zero-indexed order of the cell we want.

.. code:: ReST

    .. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
        :cell-order: 2

----

Fourth slide
============

This results in the following output:

.. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 2

