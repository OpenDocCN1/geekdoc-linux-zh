
negotiation (mod_negotiation.so) Allows content negotiation.
proxy (mod_proxy.so) Allows Apache to act as a proxy server.
proxy_connect (mod_proxy_connect.so) Allows connect request handling.
proxy_ftp (mod_proxy_ftp.so) Provides an FTP extension proxy.
proxy_http (mod_proxy_http.so) Provides an HTTP extension proxy.
rewrite (mod_rewrite.so) Allows on-the-fly URI rewriting based on rules.
setenvif (mod_setenvif.so) Sets environment variables based on a request.
speling (mod_speling.so) Auto-corrects spelling if the requested URL has incorrect capitalization and one spelling mistake.
status (mod_status.so) Allows the server status to be queried and viewed.
unique_id (mod_unique_id.so) Generates a unique ID for each request.
userdir (mod_userdir.so) Allows users to have content directories (public_html).
usertrack (mod_usertrack.so) Allows tracking of user activity on a site.
virtual_host_alias (mod_vhost_alias.so) Allows the configuration of virtual hosting.

## mod_cgi AND CGI SCRIPTS

The CGI (Common Gateway Interface) allows external application programs to interface with Web servers. Any program can be a CGI program if it runs in real time (at the time of the request) and relays its output to the requesting client. Various kinds of scripts, including shell, Perl, Python, and PHP, are the most commonly encountered CGI programs because a script can call a program and reformat its output in HTML for a client.

Apache can handle requests for CGI programs in several different ways. The most common method is to put a CGI program in the cgi-bin directory and then enable its execution from that directory only. The location of the cgi-bin directory, as specified by the ScriptAlias directive (page 958), is /var/www/cgi-bin. Alternatively, an AddHandler directive (page 952) can identify the filename extensions of scripts, such as .cgi or .pl, within the regular content (e.g., AddHandler cgi-script .cgi). If you use AddHandler, you must also specify the ExecCGI option in an Options directive within the appropriate <Directory> container. The mod_cgi module must be loaded to access and execute CGI scripts.

The following Perl CGI script displays the Apache environment. This script should be used for debugging only because it presents a security risk if remote clients can access it:

```perl
#!/usr/bin/perl

## prIntenv -- demo CGI program that prints its environment

print "Content-type: text/plain\n\n";
foreach $var (sort(keys(%ENV))) {
    $val = $ENV{$var};
    $val =~ s/\n/\\n/g;
    $val =~ s/\t/\\t/g;
    print "$var=$val\n";
}
```

SSL (Secure Sockets Layer), which is implemented by the **mod_ssl** module, has two functions: It allows a client to verify the identity of a server and it enables secure two-way communication between a client and a server. SSL is used on Web pages in conjunction with forms that require passwords, credit card numbers, or other sensitive data.

Apache uses the HTTPS protocol—not HTTP—for SSL communication. When Apache uses SSL, it listens on a second port (443 by default) for a connection and performs a handshaking sequence before sending the requested content to the client.

Server verification is critical for financial transactions: You do not want to give your credit card number to a fraudulent Web site posing as a known company. SSL uses a certificate to positively identify a server. Over a public network such as the Internet, the identification is reliable only if the certificate contains a digital signature from an authoritative source such as VeriSign or Thawte. SSL Web pages are denoted by a URL beginning with *https://*.

Data encryption prevents malicious users from eavesdropping on Internet connections and copying personal information. To encrypt communication, SSL sits between the network and an application and encrypts communication between the server and the client.

## SETTING UP **mod_ssl**

You must install the **mod_ssl** package to run SSL. The */etc/httpd/conf.d/ssl.conf* file configures and loads **mod_ssl**. The first few directives in this file instruct Apache to listen on port 443, and set various parameters for SSL operation. About a third of the way through the file is a section labeled *SSL Virtual Host Context* that sets up virtual hosts (page 965).

As with any virtual host, a virtual host for SSL holds directives such as *ServerName* and *ServerAdmin* that need to be configured. In addition, it holds some SSL-related directives. See the example on page 967.

## USING A SELF-SIGNED CERTIFICATE FOR ENCRYPTION

If you require SSL for encryption and not verification—that is, if the client already trusts the server—you can generate and use a self-signed certificate, bypassing the time and expense involved in obtaining a digitally signed certificate. Self-signed certificates generate a warning when you connect to the server: Most browsers display a dialog box that allows you to examine and accept the certificate. The *sendmail* daemon also uses certificates (page 765).

The self-signed certificate depends on two files: a private key and the certificate. The location of each file is specified in */etc/httpd/conf.d/ssl.conf*:

```bash
# grep 'SSLCertificate' /etc/httpd/conf.d/ssl.conf
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
```

The following example creates a self-signed certificate. To generate the private key that the encryption relies on, cd to /etc/pki/tls/certs and enter a make command:

```bash
# cd /etc/pki/tls/certs
# make localhost.key
umask 77 ; \
/usr/bin/openssl genrsa -aes128 2048 > localhost.key
Generating RSA private key, 2048 bit long modulus
.+++
.............................................+++
e is 65537 (0x10001)
Enter pass phrase:
Verifying - Enter pass phrase:
```

The preceding command generates a file named localhost.key that is protected by the passphrase you entered: You will need this passphrase to start the server. Keep the localhost.key file secret.

The next command generates the certificate. This process uses the private key you just created. You need to supply the same passphrase you entered when you created the private key.

```bash
# make localhost.crt
umask 77 ; \
/usr/bin/openssl req -utf8 -new -key localhost.key -x509 -days 365 -out \
localhost.crt -set_serial 0
Enter pass phrase for localhost.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Berkshire]:California
Locality Name (eg, city) [Newbury]:San Francisco
Organization Name (eg, company) [My Company Ltd]:Sobel1 Associates Inc.
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:www.sobel1.com
Email Address []:mgs@sobel1.com
```

The answers to the first five questions are arbitrary: They can help clients identify a site when they examine the certificate. The answer to the sixth question (Common Name) is critical. Because certificates are tied to the name of the server, you must enter the server’s FQDN accurately. If you mistype this information, the server name and that of the certificate will not match. The browser will then generate a warning message each time a connection is made.

As specified by ssl.conf, Apache looks for the files in the directory that you created them in. Do not move these files. After you restart Apache, the new certificate will be in use.

### NOTES ON CERTIFICATES

- As long as the server is identified by the name for which the certificate was issued, you can use the certificate on another server or IP address.
- A root certificate is the certificate that identifies the root certificate authority (root CA). Every browser contains a database of the public keys for the root certificates of the major signing authorities, including VeriSign and Thawte.
- It is possible to generate a root certificate and sign all your server certificates with this root CA. Regular clients can import the public key of the root CA so that they recognize every certificate signed by that root CA. This setup is convenient for a server with multiple SSL-enabled virtual hosts and no commercial certificates. For more information see www.modssl.org/docs/2.8/ssl_faq.html#ToC29.
- A self-signed certificate does not enable clients to verify the identity of the server.

## AUTHENTICATION MODULES AND .htaccess FILES

To restrict access to a Web page, Apache and third parties provide authentication modules and methods that can verify a user's credentials, such as a username and password. Some modules support authentication against various databases including NIS (page 770) and LDAP (page 786).

User authentication directives are commonly placed in a **.htaccess** file. A basic **.htaccess** file that uses the Apache default authentication module (**mod\_auth**) follows. When placed in `/var/www/html`, this file causes Apache to request a password before a browser can access content in the `/var/www/html` directory hierarchy. Substitute appropriate values for the local server.

```bash
# cat .htaccess
AuthUserFile /var/www/html/.htpasswd
AuthGroupFile /dev/null
AuthName "Browser dialog box query"
AuthType Basic
require valid-user
```

The `/var/www/html/.htpasswd` is a typical absolute pathname of a **.htpasswd** file and **Browser dialog box query** is the string that the user will see as part of the dialog box that requests a username and password.

The second line of the preceding **.htaccess** file turns off the group function. The fourth line specifies the user authentication type **Basic**, which is implemented by the default **mod\_auth** module. The last line tells Apache which users can access the protected directory. The entry **valid-user** grants access to the directory to any user whose username appears in the Apache password file and who enters the correct password.

You can put the Apache password file anywhere on the system, as long as Apache can read it. It is safe to put this file in the same directory as the **.htaccess** file because,
