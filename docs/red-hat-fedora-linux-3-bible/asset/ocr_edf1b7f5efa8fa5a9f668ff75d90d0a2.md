# Secure Socket Layer

A classic implementation of public-key cryptography is with secure sockets layer (SSL) communication. This is the technology that enables you to securely submit your credit card information to an online merchant. The elements of an SSL encrypted session are as follows:

+   • SSL-enabled Web browser (Mozilla, Internet Explorer, Opera, Konqueror, etc.)
+   • SSL-enabled Web server (Apache)
+   • SSL certificate

To initiate an SSL session, a Web browser first makes contact with a Web server on port 443, also known as the HTTPS port (Hypertext Transport Protocol Secure). After a socket connection has been established between the two machines, the following occurs:

+   1. The server sends its SSL certificate to the browser.
+   2. The browser verifies the identity of the server through the SSL certificate.
+   3. The browser generates a symmetric encryption key.
+   4. The browser uses the SSL certificate to encrypt the symmetric encryption key.
+   5. The browser sends the encrypted key to the server.
+   6. The server decrypts the symmetric key with its private key counterpart of the public SSL certificate.
+   7. The browser and server can now encrypt and decrypt traffic based on a common knowledge of the symmetric key.

Secure data interchange can now occur.

# Creating SSL Certificates

In order to create your own SSL certificate for secure HTTP data interchange, you must first have an SSL-capable Web server. The Apache Web server (httpd package), which comes with Fedora, is SSL-capable. Once you have a server ready to go, you should familiarize yourself with the important server-side components of an SSL certificate:

```
```bash
# ls -l /etc/httpd/conf
-rw-r--r--  1 root root  36010 Jul 14 15:45 httpd.conf
lrwxrwxrwx  1 root root      37 Aug 12 23:45 Makefile ->
.../../usr/share/ssl/certs/Makefile
drw-r----  2 root root   4096 Aug 12 23:45 ssl.crl
drw-r----  2 root root   4096 Aug 12 23:45 ssl.crt
drw-r----  2 root root   4096 Jul 14 15:45 ssl.csr
drw-r----  2 root root   4096 Aug 12 23:45 ssl.key
drw-r----  2 root root   4096 Jul 14 15:45 ssl.pm

# ls -l /etc/httpd/conf.d/ssl.conf
-rw-r-r--  1 root root  11140 Jul 14 15:45 ssl.conf
```
```