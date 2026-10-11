# Figure 7.4 Certificate window, General tab: Certificate Information

![](bbox=[0.28, 0.16, 0.71, 0.54])

# Using a Self-Signed Certificate

mod_ssl makes it extremely easy to jump-start the process of creating your own self-signed digital certificate to authenticate the Apache server to a Web browser. There are two files of interest:

+   - `/etc/httpd/conf/ssl.key/server.key`: This file is the secret half of the server's private/public pair.
+   - `/etc/httpd/conf/ssl.cert/server.cert`: This file is the server's digital self-signed certificate.

The mod_ssl installation comes with two dummy files in place of the files above, so start by deleting these two dummy files:

```
[ramon]$ sudo rm /etc/httpd/conf/ssl.key/server.key
[ramon]$ sudo rm /etc/httpd/conf/ssl.cert/server.cert
```

Next, use the Makefile provided in the /etc/httpd/conf directory to create a new server key and a new server certificate. Listings 7.7 and 7.8 show the steps involved.