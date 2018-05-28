Simple Presentation
===================

This presentation has two slides, each with a header and some text.

----

Second slide
============

There is no positioning or anything fancy.

----

Third slide
===========

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

