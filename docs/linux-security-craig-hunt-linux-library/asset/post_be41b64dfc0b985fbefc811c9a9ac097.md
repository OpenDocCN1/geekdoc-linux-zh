
## Figure 7.4 Certificate window, General tab: Certificate Information

![](img/3258bbaf790525f8c4eb25fabff7844a_226_0.png)

## Using a Self-Signed Certificate

mod_ssl makes it extremely easy to jump-start the process of creating your own self-signed digital certificate to authenticate the Apache server to a Web browser. There are two files of interest:

- `/etc/httpd/conf/ssl.key/server.key`: This file is the secret half of the server's private/public pair.
- `/etc/httpd/conf/ssl.cert/server.cert`: This file is the server's digital self-signed certificate.

The mod_ssl installation comes with two dummy files in place of the files above, so start by deleting these two dummy files:

```bash
[ramon]$ sudo rm /etc/httpd/conf/ssl.key/server.key
[ramon]$ sudo rm /etc/httpd/conf/ssl.cert/server.cert
```

Next, use the Makefile provided in the /etc/httpd/conf directory to create a new server key and a new server certificate. Listings 7.7 and 7.8 show the steps involved.

### Listing 7.7 Creating a new server key

```bash
[ramon]$ cd /etc/httpd/conf
[ramon]$ sudo make genkey
umask 77 ; \
/usr/bin/openssl genrsa -des3 1024 > \
/etc/httpd/conf/ssl.key/server.key
warning, not much extra random data, consider using the -rand option
Generating RSA private key, 1024 bit long modulus
.............+++++
............+++++
e is 65537 (0x10001)
Enter PEM pass phrase:
Verifying pass phrase - Enter PEM pass phrase:
```

The make genkey command invokes openssl to generate an RSA public/private key pair. This command prompts you for a passphrase, which will be used to protect the private key as it sits on the disk. This is done by PEM-encoding the key with the passphrase so you should use an actual phrase, with at least a half-dozen words; don't use just a single password.

Next, issue the commands in Listing 7.8 to create an X.509 certificate for your server.

### Listing 7.8 Creating a new server certificate

```bash
[ramon]$ cd /etc/httpd/conf
[ramon]$ sudo make testcert
umask 77 ; \
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key \
-x509 -days 365 -out /etc/httpd/conf/ssl.crt/server.crt
Using configuration from /usr/share/ssl/openssl.cnf
Enter PEM pass phrase:
You are about to be asked to enter information that will be
incorporated into your certificate request.
What you are about to enter is what is called a Distinguished Name
or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Virginia
Locality Name (eg, city) []:Ashburn
Organization Name (eg, company) [Internet Widgets Pty Ltd]:Ramon's Pile O Bits
Organization Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:redhat.hontanon.com
Email Address []:rhontanonn@sybex.com
```

Note that the make testcert command also invokes the openssl utility to create a new certificate and sign it with the private RSA key you created in Listing 7.7. The -days 365 option specifies that you want to create a certificate that will be valid for a year. You need to supply the passphrase that you supplied when the key was generated so you can decode it and use it to sign the newly created certificate. You also have to supply the following information to go into the X.509 certificate:

- Country name
- State or province name
- Locality name
- Organization name
- Common name
- E-mail address

These are the attributes that will be associated with your server's X.509 certificate and that will be visible from Web browsers when they connect to your site.

You have now successfully created a new server private key, along with a new certificate. Since Apache caches the certificate when it starts up, you need to restart the Apache daemon for the change to take effect, as shown in Listing 7.9.

### Listing 7.9 Restarting the Apache server with the new certificate

```bash
[ramon]$ sudo /etc/rc.d/init.d/httpd restart
   Shutting down httpd: [  OK  ]
   Starting httpd: [  OK  ]
```

The first time a Web browser contacts the Apache HTTPS server, the user is prompted with a dialog box, asking them to verify the authenticity of the certificate, since it is self-signed and not signed by any well-known certification authority.

Figure 7.5 shows the dialog box displayed by Netscape Navigator whenever a site sends a digital certificate for the first time. Instruct your users to click the More Info button and verify that the fingerprint shown corresponds with the one from your certificate (Figure 7.6). A certificate's fingerprint is a unique summary of the certificate's contents, in a format that can be easily compared visually to a trusted reference. If your customers are concerned about the validity of the certificate, they can validate the fingerprint with you via out-of-band means (in person or over the phone). This is more convenient than verifying the entire contents of the certificate, and it’s just as efficient.

## Figure 7.5 A Web browser receiving a new digital certificate

![](img/3258bbaf790525f8c4eb25fabff7844a_229_0.png)

## Figure 7.6 After clicking the More Info... button

![](img/3258bbaf790525f8c4eb25fabff7844a_229_1.png)

Note that you can obtain the fingerprint from your Apache server using the following commands:

```bash
[ramon]$ cd /etc/httpd/conf/ssl.crt/
[ramon]$ sudo openssl x509 -text -fingerprint -in server.crt | grep MD5
MD5 Fingerprint=80:46:26:AD:4D:9A:6D:63:5A:61:64:58:57:0E:8A:DA
```

The second command in this example invokes the openssl utility to import an X.509 server certificate (-in server.crt) and export a textual fingerprint (-text -fingerprint) corresponding to the input certificate. The result of this command is quite verbose, so I have piped it to a grep command to filter all lines except the one line of interest (the line containing the string MD5, a reference to the cryptographic hash algorithm used to extract the fingerprint from the whole certificate).

Once the user has verified the authenticity of the certificate, they can choose to accept it until it expires by selecting the right option on their Web browser (Figure 7.7).

## Figure 7.7 Storing trust in a digital certificate

![](img/3258bbaf790525f8c4eb25fabff7844a_230_0.png)

As you can see, setting up a small, purpose-built public-key infrastructure is not as challenging as you might think. Apache, OpenSSL, and mod_ssl are the only ingredients you need to build a certificate-driven authentication system to scale to thousands of users.

## Apache-SSL

Developed by Apache core team member Ben Laurie in the United Kingdom, Apache-SSL was actually the precursor of mod_ssl. While they have followed different development paths over the last two years, both distributions provide equivalent functionality: the addition of SSL/TLS security to the base HTTP protocol.

**Application Security**

**PART 3**

One of the important differences between Apache-SSL and mod_ssl is their approach at integrating with the base Apache installation. While Apache-SSL is based on a comprehensive modification of the Apache source code, mod_ssl is a drop-in, or a modular addition, to Apache.

There is no overriding reason why I chose to describe mod_ssl instead of Apache-SSL in this chapter except, perhaps, the fact that a mod_ssl rpm package is available for Red Hat 7.0, which is my primary home Linux server. Whichever flavor of Apache's SSL extension you choose, the concepts presented in the previous section are just as applicable.

The Apache-SSL Web page can be found at www.apache-ssl.org (see Figure 7.8).

### Figure 7.8 The Apache-SSL Project home page

![](img/3258bbaf790525f8c4eb25fabff7844a_231_0.png)

## In Sum

Web content hosting is one of the most popular uses of a Linux server in a production environment. The Apache HTTP server is a complex software package, and ensuring its security is not a trivial pursuit. There are, however, a number of directives that can be used in its configuration file to ensure that your server provides the appropriate level of authentication, authorization, and access control.

In addition, mod_ssl is a mature complement to the base Apache installation that adds confidentiality, integrity, and authentication services by using OpenSSL extensions for SSL and TLS. Using OpenSSL to create a simple certification authority, you can build a complete public-key authentication system using freely available components that have been proven in the most mission-critical of environments, including e-commerce, intranet hosting, and large Web portals.

Chapter 8, “File Sharing and Printing,” wraps up Part 3 of this book with a discussion on the security implications of sharing filesystems and local and network printers from your Linux server.
