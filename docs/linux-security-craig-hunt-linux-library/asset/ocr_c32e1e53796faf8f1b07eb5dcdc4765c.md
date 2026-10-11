restart. This is one of the log entries that should be monitored with the help of an automated log-scanning package such as logcheck and swatch, as discussed in Chapter 3, “System Monitoring and Logging.”

[Mon Dec 4 02:20:50 2000] [notice] httpd: caught SIGTERM, shutting down
[Mon Dec 4 02:20:57 2000] [notice] Apache/1.3.14 (Unix) configured -- resuming normal operations
[Mon Dec 4 02:20:00 2000] [warn] pid file /usr/local/apache/var/run/httpd.pid overwritten -- Un clean shutdown of previous apache run?

# # mod_ssl

Originally developed by Ralf S. Engelschall in early 1998, mod_ssl is the Web interface to the popular OpenSSL implementation by Eric Young and Tim Hudson. This implementation takes advantage of Apache's modular architecture and implements the Secure Sockets Layer extension as an external module in the standard Apache source tree.

The Secure Sockets Layer (SSL) allows for data privacy. Both endpoints of the communication conduct a preliminary handshake and define a secret key to be used for data encryption with a symmetric key algorithm such as DES or RC4. SSL also ensures the integrity of the data being exchanged using a message-digest algorithm such as SHA or MD5. Prior to communicating, SSL endpoints must authenticate each other using public key cryptography, where each end of the connection must present a digital certificate (typically in X.509 format) signed by a certificate authority (CA) that is commonly trusted.

Netscape developed the original SSL specification. Based on its widespread success, the IETF drafted a similar standard called Transport Layer Security (TLS) in RFC2246. TLS 1.0 is based on SSL v.3, and although it provides a way by which TLS peers can back down to SSL v.3, TLS is largely incompatible with SSL. OpenSSL supports both SSL and TLS.

By interposing OpenSSL between the TCP layer and the HTTP application layer, mod_ssl adds strong authentication, data integrity, and privacy to the transfers between the Web client and the Apache HTTP server using both SSL and TLS. Note that mod_ssl can coexist with the non-secure version of Apache. In fact, while plain HTTP uses TCP port 80 for control and data exchanges, all HTTPS (secure HTTP or HTTP over SSL) traffic goes to TCP port 443 on the Linux server.

mod_ssl is protected by the standard BSD license, which makes it freely distributable for both commercial and non-commercial use. At the writing of this book, mod_ssl makes up over 10% of the total Apache installations on the Internet, and that number has grown