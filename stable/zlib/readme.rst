zlib
====

.. code-block::

 author : Tiago Dionizio
 version: 0.4
 website: http://luaforge.net/projects/lzlib/

This package provides a library to access zlib library functions and also to 
read/write gzip files using an interface similar to the base io package.

===============  ================  ===============
   platform        architecture        version 
===============  ================  ===============
  ``Windows``         ``x86``          ``0.4``
===============  ================  ===============

----------------------------------------------------------------------------------------------------

To use this library you need zlib library.
You can get it from http://www.gzip.org/zlib/


Loading the library:

If you built the library as a loadable package

.. code-block::

	[local] zlib = require 'zlib'

If you compiled the package statically into your application, call
the function "luaopen_zlib(L)". It will create a table with the zlib
functions and leave it on the stack.


zlib functions
--------------

zlib.version()
	returns zlib version

zlib.adler32([int adler32, string buffer])
	Without any parameters, returns the inicial adler32 value.

	Call to update the adler32 value, adler is the current value, buffer is passed
	to adler32 zlib function and the updated value is returned.

zlib.crc32([int crc32, string buffer])
	Same as zlib.adler32.

zlib.compress(string buffer [, int level] [, int method] [, int windowBits] [, int memLevel] [, int strategy])
	Return a string containing the compressed buffer according to the given parameters.

zlib.decompress(string buffer [, int windowBits])
	Return the decompressed stream after processing the given buffer.

zlib.deflate(sink: function | { write: function [, close: function, flush: function ] }, compression level, [Z_DEFAILT_COMPRESSION] method, [Z_DEFLATED] windowBits, [15] memLevel, [8] strategy, [Z_DEFAULT_STRATEGY]	dictionary, [""])
	Return a deflate stream.

stream:read((number | '*l' | '*a')*)
	Return a value for each given parameter. Returns a line when
	no format is specified.

stream:lines()
	Return iterator that returns a line each time it is called, or nil
	on end of file.

stream:close()
	Close the stream.

zlib.inflate(source: string | function | { read: function, close: function }, windowBits: number, [15] dictionary, [""])
	Return an inflate stream.

----------------------------------------------------------------------------------------------------

Deflate and inflate streams can be used almost like a normal file:

stream:write(...)
	Write each parameter into the sream.

stream:read([option [, ...]])vc
	Read from the stream, each parameter corresponds to a return value.
	
	With no arguments, it reads a line.
	Parameters are interpreted as follows:
		- number - reads the specified number of bytes
		- 'a' - reads the remaining bytes
		- 'l' - reads a line

stream:lines(...)
	Returns an iterator that returns a new line each time it is called.

stream:flush(['sync' | 'full' | 'finish'])
	Flush output for deflate streams.

stream:close()
	Close the stream.