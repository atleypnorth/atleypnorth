.. title: pprint is slow
.. slug: pprint-is-slow
.. date: 2017-07-30 12:02:20 UTC+01:00
.. tags: python pprint performance
.. category: 
.. link: 
.. description: more reasons why things run slower than you would hope
.. type: text

Wondering why your script is running slow ? Are you using pprint? That may be the reason why especially if you are using it to create
log messages inside a frequently called loop (eg each line of a file read it or row of data generated or modified)

You may think it isn't being called because you can't see the output, for example it is in a log.debug() call and the current
log level is set to info.

So 

* Check how to get expensive functions lazily evaluated in log statements (i.e. they only get called when they are actually needed)
* Think about what you are printing / logging out - there is always a cost for it
