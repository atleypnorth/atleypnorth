.. title: range is not an iterator
.. slug: range-is-not-an-iterator
.. date: 2016-08-30 12:19:29 UTC+01:00
.. tags: python 
.. category: python
.. link: 
.. description: 
.. type: text

I was looking to use range to give me a generator that I could use to test something I wrote that would chunk up generators in sub generators. But then I found out this didnt quite work as expected::

    r = range(5)
    for n in r:
       print(n)

    next(r)


    0
    1
    2
    3
    4
    Traceback (most recent call last):
     File "rgen.py", line 5, in <module>
     next(r)
    TypeError: 'range' object is not an iterator

Which is not I was expecting. You can't do next on a range, but isnt it a generator ?? ::

    def myrange(n):
        i = 0
        while i<n:
        yield i
        i += 1

    for n in myrange(5):
        print(n)
    r = myrange(5)
    print(next(r))
    print(next(r))


    0
    1
    2
    3
    4
    0
    1

So I guess range is doing something else - since actually you can reuse the same range unlike a generator.

Reading the documentation Sequence types - list, tuple, range I can see where I went wrong. In the Python pocket reference I use it says '...it returns an iterable object that generates values on demand ...', except that it isn't an iterator in the Python sense Iterator types

The lesson ? Sometimes don't believe everything you read in a book, sometimes the web is right.

