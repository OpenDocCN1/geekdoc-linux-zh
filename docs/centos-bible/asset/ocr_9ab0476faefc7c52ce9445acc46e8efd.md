Now that you're familiar with the basic components, take a look at the tools used to create SSL certificates.

```
# cd /etc/pki/tls/certs
# make


This makefile allows you to create:
O public/private key pairs
O SSL certificate signing requests (CSRs)
O self-signed SSL test certificates

To create a key pair, run "make SOMETHING.key".
To create a CSR, run "make SOMETHING.csr".
To create a test certificate, run "make SOMETHING.crt".
To create a key and a test certificate in one file, run "make SOME-THING.pem".

To create a key for use with Apache, run "make genkey".
To create a CSR for use with Apache, run "make certreq".
To create a test certificate for use with Apache, run "make testcert".

To create a test certificate with serial number other than zero, add SERIAL=num

Examples:
make server.key
make server.csr
make server.crt
make stunnel.pem
make genkey
make certreq
make testcert
make server.crt SERIAL=1
make stunnel.pem SERIAL=2
make testcert SERIAL=3
```

The make command uses the Makefile to create SSL certificates. (The make command is used for a variety of software tasks with C and C++ programming.) Without any arguments, the make command simply prints the information listed above. The following defines each argument you can give to make:

+   - make server.key — Creates generic public/private key pairs.
+   - make server.csr — Generates a generic SSL certificate service request.
+   - make server.crt — Generates a generic SSL test certificate.
+   - make stunnel.pem — Generates a generic SSL test certificate, but puts the private key in the same file as the SSL test certificate.
+   - make genkey — Same as make server.key except it places the key in the ssl key directory