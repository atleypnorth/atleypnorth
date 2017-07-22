.. title: PurePath is purely paths
.. slug: purepath-is-purely-paths
.. date: 2016-09-15 21:02:57 UTC+01:00
.. tags: python
.. category: python rtfm
.. link: 
.. description: 
.. type: text

pathlib is a useful library for working with files and paths in a platform neutral way, but one thing to beware of... ::

    >>> import pathlib
    >>> p = pathlib.PurePath(".")
    >>> p
    PureWindowsPath('.')
    >>> p.exists()
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    AttributeError: 'PureWindowsPath' object has no attribute 'exists'

Unless you remember / check that a PurePath is *purely* about paths and does nothing about actual physical representation
of a file the above can puzzle you. Once you remember this fact then it is clear that it should be this ::

    >>> p = pathlib.Path(".")
    >>> p
    WindowsPath('.')
    >>> p.exists()
    True

From the pathlib manual page pure paths - 'which provide purely computational operations without I/O'. Again RTFM ....

