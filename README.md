## em-zeromq ##

Low level event machine support for ZeroMQ

# DESCRIPTION: #

WARNING THIS IS ALPHA QUALITY AT THE MOMENT

A minimal test case passes, the basics of this are working.
It needs work for sure, for instance, you cannot remove a socket yet


# Using: #

You must use either rubinius, jruby, or 1.9.x rubies. 1.8.7 unfixable issues.

If you use 1.9.x, be sure to install the ffi gem first.

For all rubies install ffi-rzmq and eventmachine as well.

This only works with ZeroMQ 2.1.x which is still unreleased
Build+Install ZeroMQ 2.1 from HEAD ( https://github.com/zeromq/zeromq2 ) 

Run the specs, see specs for examples

Want to help out? Ask! Much work to be done here

# LICENSE: #

(The MIT License)

Copyright (c) 2009 FIXME (different license?)

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.