
# 666

# Part V ✦ Running Servers

"File not found" errors can be checked in the same way as access forbidden and server internal errors. You sometimes find that Apache is not looking where you think it is for a specific file. Generally, the entire path to the file shows up in the error log. Make sure you are accessing the correct virtual host, and check for any Alias settings that might be directing your location to a place you don't expect.

- File permissions — A "file permissions prevent access" error indicates that the apache process is running as a user that is unble to open the requested file. Make sure that the account executes permissions on the directory and every directory above it, as well as permissions on the files themselves. Read permissions on a directory are also necessary if you want Apache to generate an index of files. See the manual page for chmod for more information about how to view and change permissions.

Read permissions are not necessary for compiled binaries, such as those written in C or C++, but can be safely added unless there is a need to keep the contents of the program secret.

- Access denied — A "client denied by server configuration" error indicates that Apache was configured to deny access to the object. Configure the configuration for <Location> and <Directory> sections that might affect the file you are trying to access, remembering that settings applied to a path are also applied to any paths below it. You can override these by changing the permissions only for the specific path to which you want to allow access.

- Index not found — The "Directory index forbidden by rule" error indicates that Apache could not find an index file with a name specified in the DirectoryIndex directive and was to create an index containing a list of files in a directory. Make sure your index page, if you have one of the names specified in the relevant DirectoryIndex directive, add an Options Indexes line to the appropriate <Directory> or <Location> section for that object.

- Script crashed — "Premature end of script headers" error can indicate that a script is crashing before it finishes. Sometimes, the errors that caused this also show up in the error log. When using exec or suPHP, this error may also be caused by a file ownership or permissions error. These errors are indicated in /var/log/apache/suex.log or /var/log/apache/suphph.log.

# Securing Your Web Traffic with SSL/TLS

You add security for your server, using your own certificates. Your certificate is important, and so is your capability to pass it along your network or the Internet to others. Networks aren't secure enough by themselves to protect your communications. This section examines ways in which you can guard your communications.

# Chapter 24 ♦ Running a Linux, Apache, MySQL, and PHP (LAMP) Server 667

Electronic commerce applications such as online shopping and banking are generally encrypted using the Secure Socket Layer (SSL) or Transport Layer Security (TLS) specifications. TLS is based on version 3.0 of the SSL specifications, so they are very similar in nature. Because of this similarity—and because SSL is older—the SSL acronym is often used to refer to either. For Web connections, the SSL connection is established first, and then HTTP communication is “tunneled” through it.

> Because SSL negotiation takes place before any HTTP communication, name-virtual hosting which occurs at the HTTP layer does not work with SSL as a consequence, every SSL host you configure needs to have a unique IP address.

During connection establishment between an SSL client and an SSL server, asymmetric (public key) cryptography is used to verify identities and establish the session parameters. A symmetric encryption algorithm such as DES or RC4 is used with the negotiated key to encrypt the data that is transmitted during the session. The use of asymmetric encryption during the handshake allows safe communication without the use of a shared key, and the symmetric encryption is faster and more practical for use on the data. For the client to verify the identity of the server, the server must have a previously generated private key, as well as a certificate containing the public key and information about the server. This certificate must be verifiable using a public key.

In some cases, the server also requires the client to present a certificate that it can verify. However, this is not commonly found on Web servers in high-security environments with smaller numbers of clients, where the management of certificates is more practical. You can find more information about the SSL protocol at http://developer.netscape.com/docs/manuals/security/html

Certificates are generally digitally signed by a third-party certificate authority (CA) that has verified the identity of the requester and the validity of the request. In most cases, the CA is a company that has its own arrangements with Web vendors to have its certificate installed by default. Commercial certificate authorities vary in features, and browser support, but remember that price is not always indication of quality. Some popular CAs include InstantSSL (www.instantssl.com), Thawte (www.thawte.com), and VeriSign (www.verisign.com).

# Part V ♦ Running Servers

You also have the option of creating self-signed certificates, although these should be used only for testing or when a small number of people will be accessing your server and you do not plan to have certificates on multiple machines. Directions for generating a self-signed certificate are included in the following section. The last option is to run your own certificate authority. This is probably practical if you have a small number of expected users and need to distribute your CA certificate to them (including assisting them with installing it in their browsers). The process for creating a CA is an alternative to generating self-signed certificates. You can find guides on running your own CA at these sites:

- http://www.openssl.org/ssl/ca.html

The following procedure describes how to generate and use SSL keys with the LAMP server (running on a Debian/Linux system). For a general discussion of SSL keys and procedures specific to Fedora and other Red Hat systems, refer to Chapter 6.

# Generating Your Keys

To begin setting up SSL, use the openssl command, which is part of the OpenSSL package, to generate your public and private key:

1. Use APT to verify that OpenSSL is installed. If it is not, APT downloads and installs it automatically:
   # apt-get install openssl

2. Generate a 1024-bit RSA private key and save it to a file:
   # mkdir /etc/apache/ssl.key/
   # cd /etc/apache/ssl.key/
   # openssl genrsa -out server.key 1024
   # chmod 600 server.key

> You can use a filename other than server.key and should if you plan to have more than one SSL host on your machine (which requires more than one IP address). Just make sure you specify the correct filename in the Apache configuration later.

In high-security environments, it is a good idea to encrypt the key by adding the -des3 argument after the genrsa argument on the openssl command line:

```
# openssl genrsa -des3 -out server.key 1024
```

3. You are asked for a passphrase, which is needed every time you start Apache.

# Chapter 24 Running a Linux, Apache, MySQL, and PHP (LAMP) Server 669

![](img/a2d958d7eab32ca5b89b2b8af808aa70_700_0.png)

Do not lose this passphrase because it cannot be recovered.

4. If you plan to have your certificate signed by a CA (including one that you run yourself), generate a public key and a certificate signing request (CSR):

```
# mkdir ../ssl/csr/
# cd ../ssl/csr/
# openssl req -new -key ../ssl/key/server.key -out server.key
```

Country Name (2 letter code) []:US
State or Province Name (full name) [Some-State]:Washington
Locality Name (eg, city) [:Belling
Organization Name (eg, company) [Internet Widgets Pty Ltd]:Example Company, LTD.
Organizational Unit Name (eg, section) [:Network Operations
Common Name (eg, YOUR name) [:secure.example.org
Email Address [:dom@example.org

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password]:
Optional company name []:

The Common Name should match the name that clients will use to access your server. Be sure to get the other details right if you plan to have the CSR signed by a third-party CA.

5. When using a third-party CA, submit the CSR to it and then certify the certificate it provides you to /etc/apache/ssl.crt/server.crt (or a different file, desired).

6. If you don't to sign your certificate, or if you want to test your configuration, generate a self-signed certificate and save it in a named server.crt:

```
# mkdir ../ssl/csr/
# cd ../ssl/csr/
# openssl req -new -x509 -nodes -days 365 -key ..///ssl/key/server.key -out server.crt
```

Country Name (2 letter code) [AU]:
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) [:
Organization Name (eg, company) [Internet Widgets Pty Ltd]:TEST ONLY
Organizational Unit Name (eg, section) [:TEST USE ONLY
Common Name (eg, YOUR name) [:secure.example.org
Email Address [:dom@example.org
