+   - **ssl.crt** — SSL certificate directory.
+   - **ssl.csr** — Certificate service request directory.
+   - **ssl.key** — SSL certificate private key directory.
+   - **ssl.prn** — SSL certificate parameters.
+   - **ssl.conf** — Primary Web server SSL configuration file.

Now that you’re familiar with the basic components, take a look at the tools used to create SSL certificates:

```
# cd /etc/httpd/conf
# make
This makefile allows you to create:
 o public/private key pairs
 o SSL certificate signing requests (CSRs)
 o self-signed SSL test certificates

To create a key pair, run "make SOMETHING.key".
To create a CSR, run "make SOMETHING.csr".
To create a test certificate, run "make SOMETHING.crt".
To create a key and a test certificate in one file, run "make SOMETHING.pem".

To create a key for use with Apache, run "make genkey".
To create a CSR for use with Apache, run "make certreq".
To create a test certificate for use with Apache, run "make testcert".

Examples:
 make server.key
 make server.csr
 make server.crt
 make stunnel.pem
 make genkey
 make certreq
 make testcert
```

The make command utilizes the Makefile to create SSL certificates. Without any arguments the make command simply prints the information listed above. The following defines each argument you can give to make:

+   - **make server.key** — Creates generic public/private key pairs.
+   - **make server.csr** — Generates a generic SSL certificate service request.
+   - **make server.crt** — Generates a generic SSL test certificate.
+   - **make stunnel.pem** — Generates a generic SSL test certificate, but puts the private key in the same file as the SSL test certificate.