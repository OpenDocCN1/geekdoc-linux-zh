# NOTES

s_server can be used to debug ssl clients. To accept connections from a web browser the command:

```
openssl s_server -accept 443 -www
```

can be used for example.

Most web browsers (in particular Netscape and MSIE) only support RSA cipher suites, so they cannot connect to servers which don't use a certificate carrying an RSA key or a version of OpenSSL with RSA disabled.

Although specifying an empty list of CAs when requesting a client certificate is strictly speaking a protocol violation, so SSL clients interpret this to an any CA is acceptable. This is useful for debugging purposes.

The session paraters can printed out using the sess_id program.