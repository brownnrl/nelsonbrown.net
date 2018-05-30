Sage - An Overview
##################

:date: 2018-05-29 08:00
:tags: Sage
:category: Sage
:author: Nelson Brown
:summary: An overview of sage capabilities

2D Graphics And Data Generation
===============================

.. sage::
    :id: random matrix eigenvalues

    m = random_matrix(RDF,500)
    e = m.eigenvalues()  #about 2 seconds
    w = [(i, abs(e[i])) for i in range(len(e))]
    show(points(w))


.. sage::
    :id: region plots

    var('x y')
    region_plot(sin(x^2 + y^2)/(1+y+x*y) > 0, (-5,5), (-5,5),
      incol='#ffff7f', outcol='#7f7fff', bordercol='black',
      plot_points=300).show(aspect_ratio=1) 

.. sage::
    :id: density plots

    density_plot(sin(x^2 + y^2) * cos(x+y^2) * sin(y), (-4, 4), (-4, 4),
      cmap='jet', plot_points=100).show(figsize=(6,6), frame=True)


Differential Equations
======================

.. sage::
    :id: euler method diffq

    x,y = var('x,y')
    from sage.ext.fast_eval import fast_float

    def _(f = y, g=-x*y+x^3-x,
          xmin=-1, xmax=1,
          ymin=-1, ymax=1,
          start_x=0.5, start_y=0.5,
          step_size=0.01, steps=600):
        ff = fast_float(f, 'x', 'y')
        gg = fast_float(g, 'x', 'y')
        steps = int(steps)

        points = [ (start_x, start_y) ]
        for i in range(steps):
            xx, yy = points[-1]
            try:
                points.append( (xx + step_size * ff(xx,yy), yy + step_size * gg(xx,yy)) )
            except (ValueError, ArithmeticError, TypeError):
                break

        starting_point = point(points[0], pointsize=50)
        solution = line(points)
        vector_field = plot_vector_field( (f,g), (x,xmin,xmax), (y,ymin,ymax) )

        result = vector_field + starting_point + solution

        pretty_print(html(r"$\displaystyle\frac{dx}{dt} = %s$  $ \displaystyle\frac{dy}{dt} = %s$" % (latex(f),latex(g))))
        result.show(xmin=xmin,xmax=xmax,ymin=ymin,ymax=ymax)

    _()


Graph Theory
============

.. sage::
    :id: graph1

    H=Graph({0 : [1,2,3], 4 : [0, 2], 6 : [1,2,3,4,5]})
    plot(H)


.. sage::
    :id: graph2

    c = graphs.CircularLadderGraph(10)
    show(c)

.. sage::
    :id: graph3

    m=random_matrix(ZZ,10,density=.5)
    a=DiGraph(m)
    plot(a)

.. sage::
    :id: graph3 _ removing verts

    plot(a.subgraph([1,3,7,8]))
