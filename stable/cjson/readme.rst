cjson
=====

.. code-block::

 author : Mark Pulford
 version: 0.0.01
 website: http://www.kyne.com.au/~mark/software/lua-cjson.php
 documentation: https://www.kyne.com.au/~mark/software/lua-cjson-manual.html#_api_functions

The Lua CJSON module provides JSON support for Lua.

===============  ==========  ==============
  platform          arch        Version 
===============  ==========  ==============
  Windows            x86        2.1.0
  gnu/linux        x86 x64      2.1.0
  android         x86 arm7      2.1.0
===============  ==========  ==============

----------------------------------------------------------------------------------------------------

**Notes:**

Added option ``encode_empty_table_as_array``, enabled by default, to encode empty tables as ``[]`` instead of ``{}``.

----------------------------------------------------------------------------------------------------

**Features:**

* Fast, standards compliant encoding/parsing routines
* Full support for JSON with UTF-8, including decoding surrogate pairs
* Optional run-time support for common exceptions to the JSON specification (infinity, NaN,..)
* No dependencies on other libraries

**Caveats:**

* UTF-16 and UTF-32 are not supported

Lua CJSON is covered by the MIT license. Review the file LICENSE for details.

--------------------------------------------------------------------------

Package usage
*************

.. code-block::

 local json = require'cjson'