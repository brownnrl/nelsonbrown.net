PelicanSage
###########

:date: 2017-01-22 08:00
:tags: PelicanNotebook
:category: PelicanNotebook
:author: Nelson Brown
:summary: I have been experimenting, for a while now, with a plugin for the `Pelican Static Site Generator`_. This plugin would be capable of submitting code blocks contained in the restructured text documents to IPython message compatible kernels such as Sage Cell Servers.

It is nice to be able to do full conversions of IPython notebooks, but sometimes the converted notebook doesn't look integrated with the style of your site.  Additionally, you may want to reference one or two images or cells from that notebook, leaving the converted and raw notebook for context if people wish to reference them.  To accomplish these goals, you can use an existing plugin to convert the python notebook and then extract the results.  Here, we have two notebooks.

- `Sample Notebook 1 </pages/notebook-test.html>`_
- `Sample Notebook 2 </pages/notebook-test-2.html>`_


We can use PelicanSage to convert these individual blocks into content, using the ipynb directive specifying the zero-indexed order of the cell we want.

.. code:: ReST

    .. notebook:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
        :cell-order: 2

This results in the following output:

.. notebook:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 2

Some notebooks have multiple results associated with them with different types.  However, essentially, they are the same result.  In this next example, we have a base64 encoded png svg image which was returned back from the IHaskell session as 'html' and 'display-data', and hence the two different styled results.

.. notebook:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 3

However, we can include a result-order directive, which will choose only the result desired in the final output.  Other options, such as suppress-code also work.

.. code:: ReST

    .. notebook:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
        :cell-order: 3
        :result-order: 1
        :suppress-code:


.. notebook:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 3
    :result-order: 1
    :suppress-code:

It's not 100% yet, I am still working out many of the kinks.  Intermediate results, file references, and code blocks are read into a SQLite database with the final results written to the pelican output directory.  So this doesn't work well with the continuously running Pelican development server, or with some of the deployment tools.  Rsync on the output directory with a simple, custom bash script is the direction that I have chosen to deploy the site.  If there are errors or issues, I delete and regenerate the DB and output directories.  I am hoping that as I write more articles and generally use the plugin to write out different entries on the site it will evolve.

.. _Pelican Static Site Generator: https://blog.getpelican.com/

.. _Real World Haskell: http://book.realworldhaskell.org/

.. _this post's content: https://raw.githubusercontent.com/brownnrl/nelsonbrown.net/master/2017-01-22-pelicansage.rst 
