
You now need to send a signal to the xinetd process to tell it to reload its configuration file. The quickest way to do that is to reload the xinetd service. As the root user, type the following from a shell:

```
# service xinetd reload
Reloading configuration:        [  OK  ]
```

That's it — you have enabled the rsync service. Provided that you have properly configured your FTP server (see Chapter 19), clients should now be able to download files from your computer via the rsync protocol and be able to restart interrupted downloads.

## Securing Servers with SELinux

Although SELinux can be used to lock down every aspect of a Linux system, the targeted policy included with the CentOS implementation of SELinux focuses on securing those services that are most vulnerable to attacks. The boundaries set in those policies help prevent a cracker who has compromised a service from compromising the rest of the system as well.

After you have opened a port in your firewall so others can request a service and then started that service to handle requests, SELinux can be used to set up walls around that service. As a result, its daemon process, configuration files, and data can't access resources they are not specifically allowed to access. The rest of your computer, then, is safer.

As SELinux developers continue to work out the kinks in SELinux, there has been a tendency for users to experience SELinux failures and just disable SELinux. If you have tried SELinux in the past and turned it off when you have a problem, consider that SELinux has improved quite a bit in recent versions and it might be time for you to try it again.

If you do encounter a failure related to SELinux, try to find out if SELinux should have caused the failure. In other words, maybe you were doing something that was unsafe and SELinux was right to fail. However, if the failure you encounter turns out to be a bug with SELinux, file a bug report to http://bugzilla.redhat.com and help make the service better.

See Chapter 9 for a more in-depth description of SELinux in CentOS.

## Protecting Web Servers with Certificates and Encryption

Previous sections told you how to lock the doors to your CentOS system to deny access to crackers. The best dead-bolt lock, however, is useless if you are mugged in your own driveway and have your keys stolen. Likewise, the best computer security can be for nought if you are sending passwords and other critical data unprotected across the Internet.

A savvy cracker can use a tool called a protocol analyzer or a network sniffer to peek at the data flowing across a network and pick up passwords, credit card data, and other juicy bits of information. The cracker does this by breaking into a poorly protected system on the same network and running software, or by gaining physical access to the same network and plugging in her own equipment.

You can combat this sort of theft by using encryption. The two main types of encryption in use today are *symmetric cryptography* and *public-key cryptography*.

### Symmetric Cryptography

*Symmetric cryptography*, also called *private-key cryptography*, uses a single key to both encrypt and decrypt a message. This method is generally inappropriate for securing data that will be used by a third party, because of the complexity of secure key exchange. Symmetric cryptography is generally useful for encrypting data for one's own purposes.

A classic use of symmetric cryptography is for a personal password vault. Anyone who has been using the Internet for any amount of time has accumulated a quantity of usernames and passwords for accessing various sites and resources. A personal password vault lets you store this access information in an encrypted form. The end result is that you have to remember only one password to unlock all of your access information.

Until recently, the U.S. Government was standardized on a symmetric encryption algorithm called DES (Data Encryption Standard) to secure important information. Because there is no direct way to crack DES-encrypted data, to decrypt DES-encrypted data without a password, you would have to use an unimaginable amount of computing power to try to guess the password. This is also known as the *brute-force* method of decryption.

As personal computing power has increased nearly exponentially, the DES algorithm has had to be retired. In its place, after a very long and interesting search, the U.S. Government has accepted the Rijndael algorithm as what it calls the Advanced Encryption Standard (AES). Although the AES algorithm is also subject to brute-force attacks, it requires significantly more computing power to crack than the DES algorithm does.

For more information on AES, including a command-line implementation of the algorithm, you can visit `http://aescrypt.sourceforge.net/`.

### Public-Key Cryptography

*Public-key cryptography* does not suffer from key distribution problems, and that is why it is the preferred encryption method for secure Internet communication. This method uses two keys, one to encrypt the message and another to decrypt the message. The key used to encrypt the message is called the *public key* because it is made available for all to use. The key used to decrypt the message is the *private key* and it is kept hidden. The entire process works like this:

Imagine that you want to send me a secure message using public-key encryption. Here is what we need:

- 1. I must have a public and private key pair. Depending on the circumstances, I may generate the keys myself (using special software) or obtain the keys from a key authority.
- 2. You want to send me a message, so you first look up my public key (or more accurately, the software you are using looks it up).
- 3. You encrypt the message with the public key. At this point, the message can only be decrypted with the private key (the public key cannot be used to decrypt the message).
- 4. I receive the message and use my private key to decrypt it.

## Secure Sockets Layer

A classic implementation of public-key cryptography is with Secure Sockets Layer (SSL) communication. This is the technology that enables you to securely submit your credit card information to an online merchant. The elements of an SSL-encrypted session are as follows:

- SSL-enabled Web browser (Firefox, Mozilla, Internet Explorer, Opera, Konqueror, etc.)
- SSL-enabled Web Server (Apache)
- SSL certificate

To initiate an SSL session, a Web browser first makes contact with a Web Server on port 443, also known as the HTTPS port (Hypertext Transport Protocol Secure). After a socket connection has been established between the two machines, the following occurs:

- 1. The server sends its SSL certificate to the browser.
- 2. The browser verifies the identity of the server through the SSL certificate.
- 3. The browser generates a symmetric encryption key.
- 4. The browser uses the SSL certificate to encrypt the symmetric encryption key.
- 5. The browser sends the encrypted key to the server.
- 6. The server decrypts the symmetric key with its private key counterpart of the public SSL certificate.
- 7. The browser and server can now encrypt and decrypt traffic based on a common knowledge of the symmetric key.

Secure data interchange can now occur.

## Creating SSL Certificates

In order to be able to use SSL certificates for secure HTTP data interchange, you must have an SSL-capable Web server. The Apache Web Server (httpd and mod_ssl packages), which comes with CentOS, is SSL-capable.

Here are some of the files you will need to create your own SSL certificates for the Apache Web Server:

- /etc/httpd/conf/httpd.conf — Web Server configuration file
- /etc/pki/tls/certs/Makefile — Certificate building script
- /etc/httpd/conf.d/ssl.conf — Primary Web Server SSL configuration file

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

- make server.key — Creates generic public/private key pairs.
- make server.csr — Generates a generic SSL certificate service request.
- make server.crt — Generates a generic SSL test certificate.
- make stunnel.pem — Generates a generic SSL test certificate, but puts the private key in the same file as the SSL test certificate.
- make genkey — Same as make server.key except it places the key in the ssl key directory
