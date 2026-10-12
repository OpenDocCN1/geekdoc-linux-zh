
will be used by a third party, due to the complexity of secure key exchange. Symmetric cryptography is generally useful for encrypting data for one's own purposes.

A classic use of symmetric cryptography is for a personal password vault. Anyone who has been using the Internet for any amount of time has accumulated a quantity of user names and passwords for accessing various sites and resources. A personal password vault lets you store this access information in an encrypted form. The end result is that you only have to remember one password to unlock all of your access information.

Until recently, the United States government was standardized on a symmetric encryption algorithm called DES (Data Encryption Standard) to secure important information. Because there is no direct way to crack DES encrypted data, to secure DES encrypted data without a password you would have to use an unimaginable amount of computing power to try to guess the password. This is also known as the *brute force* method of decryption.

As personal computing power has increased nearly exponentially, the DES algorithm has had to be retired. In its place, after a very long and interesting search, the United States government has accepted the Rijndael algorithm as what it calls the AES (Advanced Encryption Standard). Although the AES algorithm is also subject to brute force attacks, it requires significantly more computing power to crack than the DES algorithm does.

For more information on AES, including a command line implementation of the algorithm, you can visit `http://aescrypt.sourceforge.net/`.

## Public-key cryptography

*Public-key cryptography* does not suffer from key distribution problems, and that is why it is the preferred encryption method for secure Internet communication. This method uses two keys, one to encrypt the message and another to decrypt the message. The key used to encrypt the message is called the public key because it is made available for all to use. The key used to decrypt the message is the private key and is kept hidden. The entire process works like this:

Imagine that you want to send me a secure message using public-key encryption. Here is what we need:

1. I must have a public and private key pair. Depending on the circumstances, I may generate the keys myself (using special software) or obtain the keys from a key authority.
2. You want to send me a message, so you first look up my public key (or more accurately, the software you are using looks it up).
3. You encrypt the message with the public key. At this point, the message can only be decrypted with the private key (the public key cannot be used to decrypt the message).
4. I receive the message and use my private key to decrypt it.

## Secure Socket Layer

A classic implementation of public-key cryptography is with secure sockets layer (SSL) communication. This is the technology that enables you to securely submit your credit card information to an online merchant. The elements of an SSL encrypted session are as follows:

- SSL-enabled Web browser (Mozilla, Internet Explorer, Opera, Konqueror, etc.)
- SSL-enabled Web server (Apache)
- SSL certificate

To initiate an SSL session, a Web browser first makes contact with a Web server on port 443, also known as the HTTPS port (Hypertext Transport Protocol Secure). After a socket connection has been established between the two machines, the following occurs:

1. The server sends its SSL certificate to the browser.
2. The browser verifies the identity of the server through the SSL certificate.
3. The browser generates a symmetric encryption key.
4. The browser uses the SSL certificate to encrypt the symmetric encryption key.
5. The browser sends the encrypted key to the server.
6. The server decrypts the symmetric key with its private key counterpart of the public SSL certificate.
7. The browser and server can now encrypt and decrypt traffic based on a common knowledge of the symmetric key.

Secure data interchange can now occur.

## Creating SSL Certificates

In order to create your own SSL certificate for secure HTTP data interchange, you must first have an SSL-capable Web server. The Apache Web server (httpd package), which comes with Fedora, is SSL-capable. Once you have a server ready to go, you should familiarize yourself with the important server-side components of an SSL certificate:

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

The /etc/httpd/conf and /etc/httpd/conf.d directories contain all of the components necessary to create your SSL certificate. Each component is defined as follows:

- **httpd.conf** — Web server configuration file.
- **Makefile** — Certificate building script.
- **ssl.crl** — Certificate revocation list directory.
- **ssl.crt** — SSL certificate directory.
- **ssl.csr** — Certificate service request directory.
- **ssl.key** — SSL certificate private key directory.
- **ssl.prm** — SSL certificate parameters.
- **ssl.conf** — Primary Web server SSL configuration file.

Now that you're familiar with the basic components, take a look at the tools used to create SSL certificates:

```bash
# cd /etc/httpd/conf
# make
```

This makefile allows you to create:
- public/private key pairs
- SSL certificate signing requests (CSRs)
- self-signed SSL test certificates

To create a key pair, run “make SOMETHING.key”.
To create a CSR, run “make SOMETHING.csr”.
To create a test certificate, run “make SOMETHING.crt”.
To create a key and a test certificate in one file, run “make SOMETHING.pem”.

To create a key for use with Apache, run “make genkey”.
To create a CSR for use with Apache, run “make certreq”.
To create a test certificate for use with Apache, run “make testcert”.

Examples:

```bash
make server.key
make server.csr
make server.crt
make stunnel.pem
make genkey
make certreq
make testcert
```

The make command utilizes the Makefile to create SSL certificates. Without any arguments the make command simply prints the information listed above. The following defines each argument you can give to make:

- **make server.key** — Creates generic public/private key pairs.
- **make server.csr** — Generates a generic SSL certificate service request.
- **make server.crt** — Generates a generic SSL test certificate.
- **make stunnel.pem** — Generates a generic SSL test certificate, but puts the private key in the same file as the SSL test certificate.
- **make genkey** — Same as `make server.key` except it places the key in the `.ssl.key` directory.
- **make certreq** — Same as `make server.csr` except it places the certificate service request in the `.ssl.csr` directory.
- **make testcert** — Same as `make server.crt` except it places the test certificate in the `.ssl.crt` directory.

## Using third-party certificate signers

In the real world, I know who you are because I recognize your face, your voice, and your mannerisms. On the Internet, I cannot see these things and must rely on a trusted third party to vouch for your identity. To ensure that a certificate is immutable, it has to be signed by a trusted third party when the certificate is issued and validated every time an end user taking advantage of your secure site loads it. The following is a list of the trusted third-party certificate signers:

- **GlobalSign** — http://www.globalsign.net/
- **GeoTrust** — http://www.geotrust.com/
- **VeriSign** — http://www.verisign.com/
- **FreeSSL** — http://www.freesll.com/
- **Thawte** — http://www.thawte.com/
- **En Trust** — http://www.entrust.com/
- **ipscA** — http://www.ipsca.com/
- **COMODO Group** — http://www.comodogroup.com/

NOTE: Because of the fluid nature of the certificate business, some of these companies may not be in business when you read this, while others may have come into existence. To get a more current list of certificate authorities, use your Mozilla Firefox browser select Edit Preferences. From the Preferences window that appears, select Advanced Manage Certificates. From the Certificate Manager window that appears, refer to the Authorities tab to see Certificate Authorities from which you have received certificates.

Each of these certificate authorities has gotten a chunk of cryptographic code embedded into nearly every Web browser in the world. This chunk of cryptographic code allows a Web browser to determine whether or not an SSL certificate is authentic. Without this validation, it would be trivial for crackers to generate their own certificates and dupe people into thinking they are giving sensitive information to a reputable source.
