
Use the `psk` key **key** when using a PSK cipher suite. The key is given as a hexadecimal number without leading 0x, for example `-psk 1a2b3c4d`.

- `-ss12`, `-ss13`, `-tls1`, `-tls1_1`, `-tls1_2`, `-dtls1`, `-no_ssl2`, `-no_ssl3`, `-no_tls1`, `-no_tls1_1`, `-no_tls1_2`
  These options disable the use of certain SSL or TLS protocols. By default, the initial handshake uses a method which should be compatible with all servers and permit them to use SSL v3, SSL v2, or TLS as appropriate.

- `-bugs`
  There are several known bugs in SSL and TLS implementations. Adding this option enables various workarounds.

- `-hack`
  This option enables a further workaround for very early Netscape SSL code (?).

- `-cipher` *cipherlist*
  This allows the cipher list used by the server to be modified. When the client sends a list of supported ciphers, the first client cipher also included in the server list is used. Because the client specifies the preference order, the order of the server cipher list is irrelevant. See the **ciphers** command for more information.

- `-serverpref`
  Use the server's cipher preferences, rather than the client's preferences.

- `-tlsxtdebug`
  Print out a hex dump of any TLS extensions received from the server.

- `-no_ticket`
  Disable RFC 4507bis session ticket support.

- `-www`
  Sends a status message back to the client when it connects. This includes lots of information about the ciphers used and various session parameters. The output is in HTML format, so this option will normally be used with a web browser.

- `-WWW`
  Emulates a simple web server. Pages will be resolved relative to the current directory; for example, if the URL is requested, the file `.page.html` will be loaded.

- `-HTTP`
  Emulates a simple web server. Pages will be resolved relative to the current directory; for example, if the URL is requested, the file `.page.html` will be loaded. The files loaded are assumed to contain a complete and correct HTTP response (lines that are part of the HTTP response line and headers start and end with CRLF).

- `-engine` *id*
  Specifying an engine (by its unique **id** string) will cause `s_server` to attempt to obtain a functional reference to the specified engine, thus initializing it if needed. The engine will then be set as the default for all available algorithms.

- `-id_prefix` *arg*
  Generate SSL/TLS session IDs prefixed by **arg**. This is mostly useful for testing any SSL/TLS code (e.g., proxies) that wish to deal with multiple servers, when each of which might be generating a unique range of session IDs (e.g., with a certain prefix).

- `-rand` *file(s)*
  A file or files containing random data used to seed the random number generator, or an EGD socket (see *RAND_egd(3)*). Multiple files can be specified separated by an OS-dependent character. The separator is `;` for MS-Windows, `,` for OpenVMS, and `;` for all others.

### -servername *file*
A file containing one or more blocks of PEM data. Each PEM block should encode a TLS ServerHello extension (2 bytes type, 2 bytes length, followed by “length” bytes of extension data). If the client sends an empty TLS ClientHello extension matching the type, the corresponding ServerHello extension will be returned.

### -no_resumption_on_reneg
Set `SSL_OP_NO_SESSION_RESUMPTION_ON_RENEGOTIATION` flag.

### -status
Enables certificate status request support (aka OCSP stapling).

### -status_verbose
Enables certificate status request support (aka OCSP stapling) and gives a verbose printout of the OCSP response.

### -status_timeout *nsec*
Sets the timeout for OCSP response to **nsec** seconds.

### -status_url *url*
Sets a fallback responder URL to use if no responder URL is present in the server certificate. Without this option, an error is returned if the server certificate does not contain a responder address.

### -nextprotoneg *protocols*
Enable Next Protocol Negotiation TLS extension and provide a comma-separated list of supported protocol names. The list should contain most wanted protocols first. Protocol names are printable ASCII strings, for example “http/1.1” or “spdy/3”.

## CONNECTED COMMANDS

If a connection request is established with an `ssl` client and neither the `-www` nor the `-HTTP` option has been used, then normally any data received from the client is displayed and any key presses will be sent to the client.

Certain single letter commands are also recognized which perform special operations: these are listed below.

- **q**
  End the current `ssl` connection but still accept new connections.
- **Q**
  End the current `ssl` connection and exit.
- **r**
  Renegotiate the `ssl` session.
- **R**
  Renegotiate the `ssl` session and request a client certificate.
- **P**
  Send some plain text down the underlying `tcp` connection: this should cause the client to disconnect due to a protocol violation.
- **S**
  Print out some session cache status information.

## NOTES

`s_server` can be used to debug SSL clients. To accept connections from a web browser the command:

```
openssl s_server -accept 443 -www
```

can be used, for example.

Most web browsers (in particular Netscape and MSIE) only support RSA cipher suites, so they cannot connect to servers which don't use a certificate carrying an RSA key or a version of OpenSSL with RSA disabled.

Although specifying an empty list of CAs when requesting a client certificate is strictly speaking a protocol violation, some SSL clients interpret this to mean any CA is acceptable. This is useful for debugging purposes.

The session parameters can be printed out using the `sess_id` program.

## BUGS

Because this program has a lot of options and also because some of the techniques used are rather old, the C source of `s_server` is rather hard to read and not a model of how things should be done. A typical SSL server program would be much simpler.

The output of common ciphers is wrong: it just gives the list of ciphers that OpenSSL recognizes and the client supports.

There should be a way for the `s_server` program to print out details of any unknown cipher suites a client says it supports.

## SEE ALSO

*openssl(1)*, *openssl_ciphers(1)*, *openssl_s_client(1)*

## HISTORY

The `-no_alt_chains` option was first added to OpenSSL 1.0.2b.

# S_TIME

## NAME

`s_time` - SSL/TLS performance timing program

## SYNOPSIS

```
openssl s_time [-connect host:port] [-www page] [-cert fileName] [-key fileName] [-CApath directory] [-CAfile fileName] [-trusted_first] [-reuse] [-new] [-verify depth] [-nbio] [-time seconds] [-ssl2] [-ssl3] [-bugs] [-cipher cipherlist]
```

## DESCRIPTION

The `s_time` command implements a generic SSL/TLS client which connects to a remote host using SSL/TLS. It can request a page from the server and includes the time to transfer the payload data in its timing measurements. It measures the number of connections within a given timeframe, the amount of data transferred (if any), and calculates the average time spent for one connection.

## OPTIONS

- **-connect** *host:port*
  This specifies the host and optional port to connect to.

- **-www** *page*
  This specifies the page to GET from the server. A value of `/` gets the `index.html` [or `index.htm`] page. If this parameter is not specified, then `s_time` will only perform the handshake to establish SSL connections but not transfer any payload data.

- **-cert** *certname*
  The certificate to use, if one is requested by the server. The default is not to use a certificate. The file is in PEM format.

- **-key** *keyfile*
  The private key to use. If not specified then the certificate file will be used. The file is in PEM format.

- **-verify** *depth*
  The verify depth to use. This specifies the maximum length of the server certificate chain and turns on server certificate verification. Currently the verify operation continues after errors so all the problems with a certificate chain can be seen. As a side effect the connection will never fail due to a server certificate verify failure.

- **-CApath** *directory*
  The directory to use for server certificate verification. This directory should be in “hash format”, see `openssl-verify(1)` for more information. These are also used when building the client certificate chain.

- **-CAfile** *file*
  A file containing trusted certificates to use during server authentication and to use when attempting to build the client certificate chain.

- **-trusted_first**
  Use certificates in CA file or CA directory over the certificates provided by the server when building the trust chain to verify server certificate. This is mainly useful in environments with Bridge CA or Cross-Certified CAs.

- **-new**
  Performs the timing test using a new session ID for each connection. If neither `-new` nor `-reuse` are specified, they are both on by default and executed in sequence.

- **-reuse**
  Performs the timing test using the same session ID; this can be used as a test that session caching is working. If neither `-new` nor `-reuse` are specified, they are both on by default and executed in sequence.

- **-nbio**
  Turns on non-blocking I/O.

- **-ssl2, -ssl3**
  These options disable the use of certain SSL or TLS protocols. By default the initial handshake uses a method which should be compatible with all servers and permit them to use SSL v3, SSL v2, or TLS as appropriate. The timing program is not as rich in options to turn protocols on and off as the `openssl_s_client(1)` program and may not connect to all servers.
