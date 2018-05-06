lanes
=====

.. code-block::

 author : Asko Kauppi <akauppi@gmail.com>, Benoit Germain <bnt.germain@gmail.com>
 version: 3.10.1
 website: https://github.com/LuaLanes/lanes
 documentation: http://lualanes.github.io/lanes
 license: MIT/X11 

Running multiple Lua states in parallel.

===============  ==========  ==============
  platform          arch        Version 
===============  ==========  ==============
  ``Windows``     ``x86``      ``3.10.1``
===============  ==========  ==============

----------------------------------------------------------------------------------------------------

=====================
  Usage on Windows:
=====================

For once, Win32 thread prioritazion scheme is actually a good one, and
it works. :)  Windows users, feel yourself as VIP citizens!!

-------------------
  Windows / MSYS:
-------------------

On MSYS, 'stderr' output seems to be buffered. You might want to make
it auto-flush, to help you track & debug your scripts. Like this:

.. code-block:: lua
	
	io.stderr:setvbuf "no"

Even after this, MSYS insists on linewise buffering; it will flush at
each newline only.


===================
  Usage on Linux:
===================

Linux NTPL 2.5 (Ubuntu 7.04) was used in the testing of Lua Lanes.

This document (http://www.icir.org/gregor/tools/pthread-scheduling.html)
describes fairly well, what (all) is wrong with Linux threading, even today.

For other worthy links:
    http://kerneltrap.org/node/6080
    http://en.wikipedia.org/wiki/Native_POSIX_Thread_Library

In short, you cannot use thread prioritation in Linux. Unless you run as
root, and I _truly_ would not recommend that. Lobby for yet-another thread
implementation for Linux, and mail -> akauppi@gmail.com about it. :)

CAVEAT: Anyone sufficiently knowledgeable with pthread scheduling is free to
contact me bnt DOT germain AT gmail DOT com)  with a suitable edit
if this no longer applies on more recent kernels.