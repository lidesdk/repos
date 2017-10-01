ssl
===

.. code-block::

 author : Bruno Silvestre
 version: 0.4
 documentation: https://github.com/brunoos/luasec/wiki/LuaSec-0.4

LuaSec is a binding for OpenSSL library to provide TLS/SSL communication. It takes an already established TCP connection and creates a secure session between the peers.

===============  ==========  ==============
  platform          arch        Version 
===============  ==========  ==============
  ``Windows``     ``x86``       ``0.4``
  ``Linux``       ``x64``       ``0.4``
===============  ==========  ==============

----------------------------------------------------------------------------------------------------

This is a simple example of a client and server communication using LuaSec:

Client code:

.. code-block:: lua

 require("socket")
 require("ssl")
 
 -- TLS/SSL client parameters (omitted)
 local params
 
 local conn = socket.tcp()
 conn:connect("127.0.0.1", 8888)
 
 -- TLS/SSL initialization
 conn = ssl.wrap(conn, params)
 conn:dohandshake()
 --
 print(conn:receive("*l"))
 conn:close()

Server code:

.. code-block:: lua

 require("socket")
 require("ssl")
 
 -- TLS/SSL server parameters (omitted)
 local params 
 
 local server = socket.tcp()
 server:bind("127.0.0.1", 8888)
 server:listen()
 local conn = server:accept()
 
 -- TLS/SSL initialization
 conn = ssl.wrap(conn, params)
 conn:dohandshake()
 --
 conn:send("one line\n")
 conn:close()

LuaSec needs a set of information (such as protocol, key, certificate, etc.) to wrap the TCP connection. For instance, we can use the following parameters in the example above:

Client parameters:

.. code-block:: lua

 local params = {
   mode = "client",
   protocol = "sslv23",
   key = "/etc/certs/clientkey.pem",
   certificate = "/etc/certs/client.pem",
   cafile = "/etc/certs/CA.pem",
   verify = "peer",
   options = {"all", "no_sslv3"}
 }

Server parameters:

.. code-block:: lua

 local params = {
   mode = "server",
   protocol = "tlsv1_2",
   key = "/etc/certs/serverkey.pem",
   certificate = "/etc/certs/server.pem",
   cafile = "/etc/certs/CA.pem",
   verify = {"peer", "fail_if_no_peer_cert"},
   options = "all"
 }

Lua API
*******

ssl.newcontext(params)
	Creates a context that is used to wrap a TCP connection. In case of errors, the function returns nil, followed by an error message.

	params is a table that contains parameters to create the context. These parameters can be:

	=============  ==============  =============  ==================================================================================================================
	  Key            Value Type      Mandatory      Value                      
	=============  ==============  =============  ==================================================================================================================
	  mode             String        Yes            Use "client" or "server".
	  protocol         String	     Yes            "tlsv1": for TLS version 1 "sslv3": for SSL version 3 "sslv23": for SSL version 2 and 3
	  key              String	     No             Path to the file that contains the key (in PEM format).
	  password         String        No             / Function	Password of the encrypted key, or a callback function that returns it. If the callback does not return a string, a null password is used.
	  certificate      String	     No             Path to the file that contains the chain certificates. These must be in PEM format and must be sorted starting from the subject's certificate (client or server), followed by intermediate CA certificates if applicable, and ending at the highest level CA.
	  cafile           String	     No             Path to the file that contains a set of trusting certificates (in PEM format).
	  capath           String	     No             Path to the directory that constains a set of files with trusting certificates.
	  verify           String        No             / Table	Options used to verify the certificates. Use an array of strings for multiple options.
	  options          String        No             / Table	Options to change the behaviour of the OpenSSL library. Use an array of strings for multiple options.
	  ciphers          String	     No             The list of ciphers to be used in the connection.
	  depth            Number	     No             Maximum depth in the certificate chain verification.
	=============  ==============  =============  ==================================================================================================================

	Please, see OpenSSL documentation for more information.

	The field verify supports:

	- none
	- peer
	- client_once
	- fail_if_no_peer_cert

	The field options supports:

	- all
	- cipher_server_preference
	- cookie_exchange
	- dont_insert_empty_fragments
	- ephemeral_rsa
	- microsoft_big_sslv3_buffer
	- microsoft_sess_id_bug
	- msie_sslv2_rsa_padding
	- netscape_ca_dn_bug
	- netscape_challenge_bug
	- netscape_demo_cipher_change_bug
	- netscape_reuse_cipher_change_bug
	- no_query_mtu
	- no_session_resumption_on_renegotiation
	- no_sslv2
	- no_sslv3
	- no_ticket
	- no_tlsv1
	- pkcs1_check_1
	- pkcs1_check_2
	- single_dh_use
	- single_ecdh_use
	- ssleay_080_client_dh_bug
	- sslref2_reuse_cert_type_bug
	- tls_block_padding_bug
	- tls_d5_bug
	- tls_rollback_bug
	- allow_unsafe_legacy_renegotiation
	- legacy_server_connect
	- cisco_anyconnect
	- cryptopro_tlsext_bug
	- no_compression

Note: you need to check if your version of OpenSSL provides these options.

ssl.wrap(sock, params)
	Wraps the TCP connection sock and returns a new object that is used to establish a secure session. In case of error, the function returns nil, followed by an error message.

	ssl.wrap needs a context, which provides parameters such as protocol, certificate, key, etc., in order to create the new connection object. You can provide a already created context in params or a table with the parameters. In this case, ssl.wrap calls ssl.newcontext to obtain the context.

	Note: ssl.wrap invalidates the socket passed as argument. This prevents the garbage collector to close the TCP connection when the socket object is disposed.