To initiate an SSL session, a Web browser first makes contact with a Web server on port 443, also known as the HTTPS port (Hypertext Transport Protocol Secure). Once a socket connection has been established between the two machines, the following occurs:

+   1. Server sends SSL certificate to browser.
+   2. Browser verifies identity of server through SSL certificate.
+   3. Browser generates symmetric encryption key.
+   4. Browser uses SSL certificate to encrypt symmetric encryption key.
+   5. Browser sends encrypted key to the server.
+   6. Server decrypts the symmetric key with its private key counterpart of the public SSL certificate.
+   7. Browser and server can now encrypt and decrypt traffic based on a common knowledge of the symmetric key.

Secure data interchange can now occur.

# ### Creating SSL Certificates

In order to create your own SSL certificate for secure HTTP data interchange, you must first have an SSL-capable Web server. The Apache Web server (httpd package), which comes with Red Hat Linux, is SSL-capable. Once you have a server ready to go, you should familiarize yourself with the important server-side components of an SSL certificate:

```
```
# ls -l /etc/httpd/conf
drwxr-xr-x 7 root    root      4096 Aug 12 23:45 .
drwxr-xr-x 4 root    root      4096 Aug 13 00:23 ..
-rw-r--r--  1 root    root     35918 Jul 14 15:45 httpd.conf
lrwxrwxrwx 1 root    root        37 Aug 12 23:45 Makefile ->
../../usr/share/ssl/certs/Makefile
drwx------ 2 root    .root     4096 Aug 12 23:45 ssl.crl
drwx------ 2 root    .root     4096 Aug 12 23:45 ssl.crt
drwx------ 2 root    root      4096 Jul 14 15:45 ssl.csr
drwx------ 2 root    root      4096 Aug 12 23:45 ssl.key
drwx------ 2 root    root      4096 Jul 14 15:45 ssl.prm

# ls -l /etc/httpd/conf.d/ssl.conf
-rw-r--r-- 1 root    root     11140 Jul 14 15:45 ssl.conf
```
```

The /etc/httpd/conf and /etc/httpd/conf.d directories contains all of the components necessary to create your SSL certificate. Each component is defined as follows:

+   *   **httpd.conf** — Web server configuration file.
+   *   **Makefile** — Certificate building script.
+   *   **ssl.crl** — Certificate revocation list directory.