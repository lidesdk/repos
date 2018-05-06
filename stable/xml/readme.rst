xml
===

.. code-block::

 author : Gaspard Bucher
 website: https://github.com/lubyk/xml
 license: MIT/X11
 documentation: http://doc.lubyk.org/xml.html

Very fast xml parser for Lua based on RapidXML to parse XML content.

===============  ==========  ==============
  platform          arch        version
===============  ==========  ==============
  ``Windows``      ``x86``     ``1.1.20``
  ``Linux``        ``x64``     ``1.1.20``
===============  ==========  ==============

Usage
^^^^^

.. code-block:: lua

 local data = xml.load(some_xml)
 local xml_string = xml.dump(some_table)


This xml library uses string keys in Lua tables to store attributes and numerical keys for sub-nodes. Since the 'xml' attribute is not allowed in XML, we use this key to store the tag. Here is an example of Lua content:

**LUA**

.. code-block:: lua

 {xml='document',
  {xml = 'article',
    {xml = 'p', 'This is the first paragraph.'},
    {xml = 'h2', class = 'opt', 'Title with opt style'},
  },
  {xml = 'article',
    {xml = 'p', 'Some ', {xml = 'b', 'important'}, ' text.'},
  },
 }

**XML**

And the equivalent xml:

.. code-block:: xml

 <document>
  <article>
    <p>This is the first paragraph.</p>
    <h2 class='opt'>Title with opt style</h2>
  </article>
  <article>
    <p>Some <b>important</b> text.</p>
  </article>
 </document>



Notes on speed
^^^^^^^^^^^^^^

RapidXML is a very fast parser that uses in-place modification of the input text. Since Lua strings are immutable, we have to make a copy except for the xml.Parser.NonDestructive and xml.Parser.Fastest settings. With these types some xml entities such as &lt; are not translated.

See RapidXML for details.



Class methods

.load (string)
 Parse a string containing xml content and return a table. Uses xml.Parser with the xml.Parser.Default type.

.loadpath (path)
 Parse the XML content of the file at path and return a lua table. Uses xml.Parser with the xml.Parser.Default type.

.dump (table, max_depth)
 Dump a lua table in the format described above and return an XML string. The max_depth parameter is used to avoid infinite recursion in case a table references one of its ancestors.

 Default maximal depth is 3000.

.removeNamespace (data, key)
 This function finds the xmlns:NAME='KEY' declaration and removes NAME: from the tag names.

 Example:

 local data = xml.load [[
  <foo:document xmlns:foo='bar'>
    <foo:name>Blah</foo:name>
  </foo:document>
 ]]

xml.removeNamespace(data, 'bar')

 -- Result
 {xml = 'document', ['xmlns:foo'] = 'bar',
   {xml = 'name', 'Blah'},
 }

.find (data, tag, attr_key, attr_value)
 Recursively find the first table with a tag equal to tag. This search uses lub.search to do an Iterative deepening depth-first search because we usually search for elements close to the surface.

 For more options, use lub.search directly with a custom function.

 You can also pass an attribute key and attribute value to further filter the searched node. This gives this function the same arguments as LuaXML's find function.

 Usage examples:

.. code-block:: lua

  local sect = xml.find(elem, 'simplesect', 'kind', 'section')
  print(xml.find(sect, 'title'))

Classes
^^^^^^^

Parser
 The parser class is used to encapsulate parsing and settings in an object. When using default settings, it is not necessary to create parser objects and one can simply use xml.load.


Installing
^^^^^^^^^^

To install this library I recommend to use the command line of lide, using ``lide install``.

*All dependencies will be installed automatically:*

``$ lide install xml``


Credits
^^^^^^^

bci is designed and implemented by `Gaspard Bucher <https://github.com/lubyk/xml>`_.

License
^^^^^^^
`Public Domain <https://creativecommons.org/publicdomain/mark/1.0/>`_