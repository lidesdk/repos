http
====

.. code-block::

 author : Hernan Dario Cano
 version: 0.0.01
 
HTTP and HTTPS requests support for lide.

===============  ==========  ==============
  platform          arch        version
===============  ==========  ==============
  ``Windows``      ``x86``      ``0.0.01``
===============  ==========  ==============

----------------------------------------------------------------------------------------------------

Lua API
*******

http.download ( url, dest )
	Download the given "url" to "dest" path to the system.

http.test_connection ( url )
	Test HTTP or HTTPS connection.