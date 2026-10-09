```
$ sudo apache2-ssl-certificate
creating selfsigned certificate
replace it with one signed by a certification authority (CA)

enter your ServerName at the Common Name prompt

If you want your certificate to expire after x days call this program
with -days x
Generating a 1024 bit RSA private key ..............++++++++
............++++++++
writting new private key to '/etc/apache2/ssl/apache.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguishing Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Some-State]:California
Locality Name (eg, city) []:San Francisco
Organization Name (eg, company; recommended) []:Sobel1 Associates Inc.
Organizational Unit Name (eg, section) []:
server name (eg, ssl.domain.tld; required!!) []:www.sobel1.com
Email Address []:msg@sobel1.com
```

The answers to the first five questions are arbitrary: They can help clients identify a
site when they examine the certificate. The answer to the sixth question (**server
name**)
is critical. Because certificates are tied to the name of the server, you must enter the
server's FQDN accurately. If you mistype this information, the server name and the
name of the certificate will not match. A browser will then generate a warning mes-
 sage each time a connection is made.

Now you must create an SSL-enabled virtual host in /etc/apache2/sites- available.
Host-by-name virtual hosting will not work with SSL because the HTTP Host head-
 er sent by the client that Apache uses to differentiate between host-by-name virtual
hosts is encrypted. You can use only one SSL certificate, matching one domain per
IP address. You can have multiple virtual hosts on that IP address, but if they are
accessed over HTTPS, the client will receive an error saying that the certificate does
not match the domain name. After you enable the new virtual host and restart
Apache, the new certificate will be in use.

Following is an example wildcard setup for /etc/apache2/sites- available/ssl. Enable
it with **sudo a2ensite ssl**.

```
VirtualHost *:80>
Redirect permanent / https://www.sobel1.com/
</VirtualHost>
```