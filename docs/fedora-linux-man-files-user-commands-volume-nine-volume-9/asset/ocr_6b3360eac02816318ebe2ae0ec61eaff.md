display the whole server certificate chain: normally only the server certificate itself is displayed.

+   -**-prexit**
+     print session information when the program exits. This will always attempt to print out information even if the connection fails. Normally information will only be printed out once if the connection succeeds. This option is useful because the cipher in use may be renegotiated or the connection may fail because a client certificate is required or is requested only after an attempt is made to access a certain URL. Note: the output produced by this option is not always accurate because a connection might never have been established.

+   -**-state**
+     prints out the ssl session states.

+   -**-debug**
+     print extensive debugging information including a hex dump of all traffic.

+   -**-msg**
+     show all protocol sages with hex dump.

+   -**-nbio_test**
+     tests non-blocking I/O

+   -**-nbio**
+     turns on non-blocking I/O

+   -**-crlf**
+     this option translated a line feed from the terminal into CR+LF as required by so servers.

+   -**-ign_eof**
+     inhibit shutting down the connection when end of file is reached in the input.

+   -**-quiet**
+     inhibit printing of session and certificate information. This implicitly turns on **-ign_eof** as well.

+   -**-no_ign_eof**
+     shut down the connection when end of file is reached in the input. Can be used to override the implicit **-ign_eof** after **-quiet**.

+   -**-psk_identity** *identity*
+     Use the PSK identity *identity* when using a PSK cipher suite.

+   -**-psk** *key*
+     Use the PSK key *key* when using a PSK cipher suite. The key is given as a hexadecimal number without leading 0x, for example -psk 1a2b3c4d.

+   -**-ssl2**, **-ssl3**, **-tls1**, **-tls1_1**, **-tls1_2**, **-dtls1**, **-no_ssl2**, **-no_ssl3**, **-no_tls1**, **-no_tls1_1**, **-no_tls1_2**
+     these options disable the use of certain SSL or TLS protocols. By default the initial handshake uses a thod which should be compatible with all servers and permit them to use SSL v3, SSL v2 or TLS as appropriate.

Unfortunately there are still ancient and broken servers in use which cannot handle this technique and will fail to connect. So servers only work if TLS is turned off.