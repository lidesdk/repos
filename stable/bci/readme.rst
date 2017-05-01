.. _dcanoh: http://github.com/lidesdk/repos/dcanoh.rst>`.


bci
===

.. code-block::

 author : Luiz Henrique de Figueiredo
 website: http://webserver2.tecgraf.puc-rio.br/~lhf/ftp/lua/#lbci
 license: Pubic Domain

This is a bytecode inspector library for Lua 5.1. It allows you to look
inside Lua functions from Lua.

===============  ==========  ==============
  platform          arch        version
===============  ==========  ==============
  ``Windows``      ``x86``     ``0.1.00``
===============  ==========  ==============

This is a bytecode inspector library for Lua 5.1. It allows you to look
inside Lua functions from Lua.

To try the library, just edit Makefile to reflect your installation of Lua and
then run make. This will build the library and run a simple test. Note that
this library needs inside information from the Lua private headers and so it
needs to be built using a Lua build directory, not just the usual installation
directories.

There is no manual but the library is simple and intuitive; see the summary
below. Read also test.lua and print.lua, which show the library in action.

This code is hereby placed in the public domain.
Please send comments, suggestions, and bug reports to lhf@tecgraf.puc-rio.br .

-------------------------------------------------------------------------------
.. code-block:: lua

-- inspector library:
 getconstant(f,i) 	 getinstruction(f,i) 	 setconstant(f,i,v) 
 getfunction(f,i) 	 getlocal(f,i) 
 getheader(f,i) 	 getupvalue(f,i) 

-------------------------------------------------------------------------------


Installing
^^^^^^^^^^

To install this library I recommend to use the command line of lide, using ``lide install``.

*All dependencies will be installed automatically:*

``$ lide install bci``


Credits
^^^^^^^

bci is designed and implemented by [Luiz Henrique de Figueiredo](http://webserver2.tecgraf.puc-rio.br/~lhf).

License
^^^^^^^

[Public Domain](https://creativecommons.org/publicdomain/mark/1.0/).