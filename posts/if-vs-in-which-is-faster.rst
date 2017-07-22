.. title: if vs in, which is faster?
.. slug: if-vs-in-which-is-faster
.. date: 2016-08-31 14:59:40 UTC+01:00
.. tags: python
.. category:  python
.. link: 
.. description: 
.. type: text

Sometimes I want to check if at least one value in a set of variables is None. Generally you can write that as an if statement with or clauses. If you have a largish number of variables then it can look little messy so I sometimes a created a list of the variable values and then did a "None in list" but I was wondering that while it may look a bit nicer what hit does it give me in performance?

Time to fire up Jupyter notebook and see ... ::

    s="""\
    a=1
    b=2
    (a is None or b is None)
    """

    s2="""\
    a=1
    b=2
    None in [a,b]
    """

    s3="""\
    a=None
    b=2
    (a is None or b is None)
    """

    s3="""\
    a=None
    b=4
    None in [a,b]
    """

    timeit.timeit(stmt=s, number=100000)
    timeit.timeit(stmt=s2, number=100000)
    timeit.timeit(stmt=s3, number=100000)
    timeit.timeit(stmt=s4, number=100000)

which gives::

    0.004445533733814955
    0.013848952017724514
    0.003327607177197933
    0.010672084987163544

Not surprisingly using the list and in is slower, but with it being slower by a factor of about 3 it is not something you would want to do in tight loop.

You can see the short cut logic in the or version makes it quicker when the first element is None, but then the list one is quicker then because it doesnt have to go over the whole list. 

Lesson? Nicer looking code generally is not the faster way ...

PS making the list a tuple seems to make s2 faster, because it set it as a constant since it is immutable? ::

    s2b="""\
    a=1
    b=2
    None in (a,b)
    """
    timeit.timeit(stmt=s2b, number=100000)
    0.01124082
