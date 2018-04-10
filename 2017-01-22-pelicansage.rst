PelicanSage
###########

:date: 2017-01-22 08:00
:tags: PelicanSage
:category: PelicanSage
:author: Nelson Brown
:summary: I have been experimenting, for a while now, with a plugin for the `Pelican Static Site Generator`_. This plugin would be capable of submitting code blocks contained in the restructured text documents to IPython message compatible kernels such as Sage Cell Servers.

I have been experimenting, for a while now, with a plugin for the `Pelican Static Site Generator`_. This plugin would be capable of submitting code blocks contained in the restructured text documents to an IPython message compatible kernel (through a websocket, actually), and then organizing the results into files and ASCII chunks stored in an SQLite database.

Why?  Part of the motivation came from the system used to generate the content for `Real World Haskell`_.  I'd say inspiration, but that would be giving more credit to my work than is due in comparison.  I liked how it seemed that the results were being fetched and fed into the content of the book automatically.  My PlugIn was originally targeted for a `Sage Cell Server`_, and then expanded to include IHaskell / IPython and now any Jupyter message protocol notebook. There already exist notebook converters and Pelican Plugins which can work out of the box to convert a MarkDown formatted notebook into a reasonable page or post.  However, this doesn't give you a method to reference into those results again without directly linking to the converted content.  If you ever wanted to update that notebook again, more than likely you'd lose a bit of those references.

The other thing that would be nice is if you could give people the opportunity to experiment, mold, or change what you had written while still taking the benefit of static site generation and the fast response times associated with not having to have the client make multiple fetches to the sage cell servers.  So this would rule out using the `Sage Cell Server`_ direct javascript interface (as it would need to be executed and fetched between the reader of the site).  Added to this, you'd lose out on the ecosystem outside of sage.

Plus, sometimes it's nice to keep your thoughts organized into a single file.  If the results aren't too computationally intensive, I like to stay in one frame of mind.  When the results fetch in a few seconds, it is nice not to have to switch back and forth between a notebook and the post you are editing.  You can look at the source for `this post's content`_, and I think that it looks fairly clean.

So to understand how it is used, we can take a look at this RST code block, with a directive provided by the PelicanSage plugin.

.. code:: ReST
    
    .. sage::
        :id: interesting graphic
        
        [interesting code to make an interesting graphic]

When executed using the PelicanSage directive, this code block is displayed using some highlighting styles dependent on the CSS in the site's template.  The order of the inputs are captured: this is the first sage block so it is designated [in 1].  The remaining code blocks are ordered [out 1] and [out 1].

.. sage::
    :id: interesting graphic

    import numpy

    difference = 3

    print "This gets sent to stdout, returned as a stream result."
    
    import pylab as plt
    
    t = plt.arange(0.0, 2.0, 0.01)
    s = plt.sin(2*pi*t)
    plt.plot(t, s)
    plt.xlabel('time (s)')
    plt.ylabel('voltage (mV)')
    plt.title('About as simple as it gets, folks')
    plt.grid(True)
    plt.show()

Notice how you get two types of results out from the above code block?  One is a stream result, and the subsequent is a plot.  We get the two of them automatically added to the final HTML document.

We can also work where there are exceptions that occur in the stream.  The PelicanSage plugin throws a warning for each exception encountered during the execution of a code block; however, doesn't halt the evaluation of subsequent blocks as there may be a reason that the exception occurred.

.. sage::

    print difference

    raise Exception("Maybe this was unintentional or an intentional exception for illustrative purposes.")


Using this, we can make all kinds of plots, graphs, and computations on systems which never have the Sage platform installed.  Which is really nice.

.. sage::
    :id: graph1

    H=Graph({0 : [1,2,3], 4 : [0, 2], 6 : [1,2,3,4,5]})
    plot(H)

This doesn't mean that you can't install Sage and SageCell, and then point the PelicanSage plugin to your local SageCell by configuration setting.  Note, you would want to be careful to not expose the hosted service outside of your local machine unless that is your intention.

In some cases, you may not want to show the code which leads to your result (if you didn't want to show the results then you could just use a code or code-block directive).  So using the following sage directive:

.. code:: ReST

    .. sage::
        :id: reshaped array
        :suppress-results:

        from numpy import *
        
        print arange(10000).reshape(100, 100) 

We get the code block evaluated, but the results suppressed.

.. sage::
    :id: reshaped array
    :suppress-results:

    from numpy import *
    
    print arange(10000).reshape(100, 100) 

When we want to refer to the results again later, we can use the sage-result directive.

.. code:: ReST

    .. sage-result:: reshaped array

Which results in the following:

.. sage-result:: reshaped array

We can reuse this result as many times as we would like:

.. sage-result:: reshaped array

Further we can show results without code.

.. code:: ReST
    
    .. sage::
        :id: graph2
        :suppress-code:

        H1=Graph({0 : [1,2,3], 4 : [0, 2], 6 : [1,2,3,4,5]})
        plot(H1)
        H2=Graph({0 : [1,2,3], 2 : [0, 2], 6 : [1,2,3,4,5]})
        plot(H2)

Note that the below we see results of the execution, and not in the associated code.  However, each block returned also has options for viewing the code that generated the result: a permalink to the public sage cell server with the block / entire worksheet, or a link to the raw text file of the code block kept on the server.

.. sage::
    :id: graph2
    :suppress-code:

    H1=Graph({0 : [1,2,3], 4 : [0, 2], 6 : [1,2,3,4,5]})
    H1.show()
    H2=Graph({0 : [1,2,3], 2 : [0, 2], 6 : [1,2,3,4,5]})
    H2.show()

Notice that there are two resultant graphs in the output.  We can choose to display just one by hiding the results and then using a sage-image directive (note: different from the sage-result directive which is used for stream results), specifying the id of the code block and the zero-indexed order of the returned image.


.. code:: ReST

    .. sage-image:: graph2
        :order: 1 


.. sage-image:: graph2
    :order: 1 

It is still nice to be able to do full conversions of IPython notebooks, but sometimes the converted notebook doesn't look integrated with the style of your site.  Additionally, you may want to reference one or two images or cells from that notebook, leaving the converted and raw notebook for context if people wish to reference them.  To accomplish these goals, you can use an existing plugin to convert the python notebook and PelicanSage to extract results.  Here, we have two notebooks.

- `Sample Notebook 1 </pages/notebook-test.html>`_
- `Sample Notebook 2 </pages/notebook-test-2.html>`_



fp_in_scala
haskellbook
notebook_haskell_sample_nb3format.ipynb
notebook_haskell_sample_nb3format.ipynb-meta
notebook_haskell_sample_nb4format.ipynb
notebooktest2.ipynb
notebooktest2.ipynb-meta

We can use PelicanSage to convert these individual blocks into content, using the ipynb directive specifying the zero-indexed order of the cell we want.

.. code:: ReST

    .. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
        :cell-order: 2

This results in the following output:

.. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 2

Some notebooks have multiple results associated with them with different types.  However, essentially, they are the same result.  In this next example, we have a base64 encoded png svg image which was returned back from the IHaskell session as 'html' and 'display-data', and hence the two different styled results.

.. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 3

However, we can include a result-order directive, which will choose only the result desired in the final output.  Other options, such as suppress-code also work.

.. code:: ReST

    .. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
        :cell-order: 3
        :result-order: 1
        :suppress-code:


.. ipynb:: /pages/notebooks/notebook_haskell_sample_nb3format.ipynb
    :cell-order: 3
    :result-order: 1
    :suppress-code:

It's not 100% yet, I am still working out many of the kinks.  Intermediate results, file references, and code blocks are read into a SQLite database with the final results written to the pelican output directory.  So this doesn't work well with the continuously running Pelican development server, or with some of the deployment tools.  Rsync on the output directory with a simple, custom bash script is the direction that I have chosen to deploy the site.  If there are errors or issues, I delete and regenerate the DB and output directories.  I am hoping that as I write more articles and generally use the plugin to write out different entries on the site it will evolve.

.. _Pelican Static Site Generator: https://blog.getpelican.com/

.. _Sage Cell Server: https://sagecell.sagemath.org/

.. _Real World Haskell: http://book.realworldhaskell.org/

.. _this post's content: https://raw.githubusercontent.com/brownnrl/nelsonbrown.net/master/2017-01-22-pelicansage.rst 
