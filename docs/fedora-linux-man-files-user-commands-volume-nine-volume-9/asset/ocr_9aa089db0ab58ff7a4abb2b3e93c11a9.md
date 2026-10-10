# OPTIONS

**-connect** *host:port*
This specifies the host and optional port to connect to.

**-www** *page*
This specifies the page to GET from the server. A value of '/ ' gets the index.html[l] page. If this parameter is not specified, then s_ti will only perform the handshake to establish SSL connections but not transfer any payload data.

**-cert** *certna*
The certificate to use, if one is requested by the server. The default is not to use a certificate. The file is in PEM format.

**-key** *keyfile*
The private key to use. If not specified then the certificate file will be used. The file is in PEM format.

**-verify** *depth*
The verify depth to use. This specifies the maximum length of the server certificate chain and turns on server certificate verification. Currently the verify operation continues after errors so all the problems with a certificate chain can be seen. As a side effect the connection will never fail due to a server certificate verify failure.

**-CApath** *directory*
The directory to use for server certificate verification. This directory st be in “hash format”, see verify for more information. These are also used when building the client certificate chain.

**-CAfile** *file*
A file containing trusted certificates to use during server authentication and to use when attempting to build the client certificate chain.

**-trusted_first**
Use certificates in CA file or CA directory over the certificates provided by the server when building the trust chain to verify server certificate. This is mainly useful in environments with Bridge CA or Cross-Certified CAs.

**-new**
performs the timing test using a new session ID for each connection. If neither -new nor -reuse are specified, they are both on by default and executed in sequence.

**-reuse**
performs the timing test using the sa session ID; this can be used as a test that session caching is working. If neither -new nor -reuse are specified, they are both on by default and executed in sequence.

**-nbio**
turns on non-blocking I/O.

**-ssl2, -ssl3**
these options disable the use of certain SSL or TLS protocols. By default the initial handshake uses a thod which should be compatible with all servers and permit them to use SSL v3, SSL v2 or TLS as appropriate. The timing program is not as rich in options to turn protocols on and off as the (1) program and may not connect to all