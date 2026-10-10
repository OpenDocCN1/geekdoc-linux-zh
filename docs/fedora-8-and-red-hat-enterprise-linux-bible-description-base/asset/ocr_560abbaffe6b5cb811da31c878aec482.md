4. I receive the message and use my private key to decrypt it.

# Secure Sockets Layer

A classic implementation of public-key cryptography is with secure sockets layer (SSL) communication. This is the technology that enables you to securely submit your credit card information to an online merchant. The elements of an SSL-encrypted session are as follows:

+   - SSL-enabled Web browser (Firefox, Mozilla, Internet Explorer, Opera, Konquerer, and so on)
+   - SSL-enabled Web server (Apache)
+   - SSL certificate

To initiate an SSL session, a Web browser first makes contact with a Web server on port 443, also known as the HTTPS port (HyperText Transport Protocol Secure). After a socket connection has been established between the two machines, the following occurs:

+   1. The server sends its SSL certificate to the browser.
+   2. The browser verifies the identity of the server through the SSL certificate.
+   3. The browser generates a symmetric encryption key.
+   4. The browser uses the SSL certificate to encrypt the symmetric encryption key.
+   5. The browser sends the encrypted key to the server.
+   6. The server decrypts the symmetric key with its private key counterpart of the public SSL certificate.
+   7. The browser and server can now encrypt and decrypt traffic based on a common knowledge of the symmetric key.

Secure data interchange can now occur.

# Creating SSL certificates

In order to be able to use SSL certificates for secure HTTP data interchange, you must have an SSL-capable Web server. The Apache Web server (httpd package), which comes with Fedora and RHEL, is SSL-capable. Here are some of the files you will need to create your own SSL certificates for the Apache Web server:

+   - /etc/httpd/conf/httpd.conf — Web server configuration file
+   - /etc/pki/tls/certs/Makefile — Certificate building script
+   - /etc/httpd/conf.d/ssl.conf — Primary Web server SSL configuration file

Now that you’re familiar with the basic components, take a look at the tools used to create SSL certificates:

```
```
# cd /etc/pki/tls/certs
# make
```
```