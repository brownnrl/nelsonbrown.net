PelicanSage
###########

:date: 2014-06-10 08:00
:tags: Misc
:category: Misc
:author: Nelson Brown
:summary: I have been experimenting, for a while now, with a plugin for the `Pelican Static Site Generator`_. This plugin would be capable of submitting code blocks contained in the restructured text documents to IPython message compatible kernels such as Sage Cell Servers.
:status: draft

I have been experimenting, for a while now, with a plugin for the `Pelican Static Site Generator`_. This plugin would be capable of submitting code blocks contained in the restructured text documents to an IPython message compatible kernel (through a websocket, actually), and then organizing the results into files and ASCII chunks stored in an SQLite database.

Why?  Well, originally, it was targeted for a `Sage Cell Server`_. There already exist notebook converters and Pelican Plugins which can work out of the box to convert a MarkDown formatted notebook into a reasonable page or post.  However, this doesn't give you a method to reference into those results again without directly linking to the converted content.  If you ever wanted to update that notebook again, more than likely you'd lose a bit of those references.

The other thing that would be nice is if you could give people the opportunity to experiment, mold, or change what you had written while still taking the benefit of static site generation and the fast response times associated with not having to have the client make multiple fetches to the sage cell servers.

So to make it work, we can take a look at this RST code block, with a directive provided by the PelicanSage plugin.

.. code::
    
    .. sage::
        :id: interesting graphic
        
        [interesting code to make an interesting graphic]

When executed using the PelicanSage directive, this code block is displayed using some highlighting styles dependent on the CSS in the site's template.  The order of the inputs are captured: this is the first sage block so it is designated [in 1].  The remaining code blocks are ordered [out 1] and [out 1].

.. sage::
    :id: interesting graphic

    import numpy

    difference = 3

    print "hi."
    
    import pylab as plt
    
    t = plt.arange(0.0, 2.0, 0.01)
    s = plt.sin(2*pi*t)
    plt.plot(t, s)
    plt.xlabel('time (s)')
    plt.ylabel('voltage (mV)')
    plt.title('About as simple as it gets, folks')
    plt.grid(True)
    #savefig("test.png")
    plt.show()
    #factorial(2012)


.. sage::

    print difference

    raise Exception()

Let's have an aside for some intermediate graph theory.

.. sage::
    :id: graph1

    H=Graph({0 : [1,2,3], 4 : [0, 2], 6 : [1,2,3,4,5]})
    plot(H)

.. sage::
    :id: reshaped array
    :suppress-results:

    from numpy import *
    
    print arange(10000).reshape(100, 100) 

more things?

.. sage-result:: reshaped array

.. _Pelican Static Site Generator: https://blog.getpelican.com/

.. _Sage Cell Server: https://sagecell.sagemath.org/
