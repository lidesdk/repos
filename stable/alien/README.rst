.. _dcanoh: http://github.com/lidesdk/repos/dcanoh.rst>`.


alien
=====

Alien is a Foreign Function Interface (FFI) for Lua.

===============  ==========  ==============
  platform          arch        version
===============  ==========  ==============
  ``Windows``      ``x86``      ``0.7.0``
===============  ==========  ==============

Alien is a Foreign Function Interface (FFI) for Lua. An FFI lets you
call functions in dynamic libraries (.so, .dylib, .dll, etc.) from Lua
code without having to write, compile and link a C binding from the
library to Lua. In other words, it lets you write extensions that call
native code using just Lua.

Alien works on Unix-based systems and Windows. It has been tested on
Linux/x86, Linux/x64, Linux/ARM, FreeBSD/x86, Windows/x86, OS X/x86,
and OS X/PPC.

The Windows binary uses MSVCR80.DLL for compatibility with LuaBinaries.


instalación
^^^^^^^^^^^

Para instalar ésta libreria recomiendo utilizar la linea de comandos de lide, usando ``lide install``.

*Así todas las dependencias se instalarán automaticamente:*

``$ lide install alien``


Credits
^^^^^^^

Alien is designed and implemented by Fabio Mascarenhas. It uses the
great [libffi](http://sourceware.org/libffi)
library by Anthony Green (and others) to do the heavy lifting of calling
to and from C. The name was stolen from Common Lisp FFIs.

License
^^^^^^^

Alien uses the MIT license (the same as Lua).