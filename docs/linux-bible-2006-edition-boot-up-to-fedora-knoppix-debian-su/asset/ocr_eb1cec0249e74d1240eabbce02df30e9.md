# Chapter 6 - Securing Linux

81LZXra+acHEStR03RPQJgv2y1mjkPmC1WjoeYfdxH7+Mbg/6fommK9auWAT
WOFIFW+/a8WRYQJLMA2V0QQVh4jnjpGCVNY9AQSHm1UI5JSy7tdl1
----- END CERTIFICATE-----

Copy and paste this certificate into an empty file server.crt, which must reside in the /etc/httpd/conf/ssl.crt directory, and restart your Web server:

```
# service http restart
```

Assuming your Web site was previously functioning, you can now view it in a secure fashion by placing an "s" after the http in the Web address. So if you previously viewed your Web site at http://www.acmemarina.com, you can now view it in a secure fashion by going to https://www.acmemarina.com.

# Creating Self-Signed Certificates

Generating and running a self-signed SSL certificate is much easier than having a signed certificate. To generate a self-signed SSL certificate, do the following:

+   1. Remove the key and certificate that currently exist:

```
# cd /etc/httpd/conf
# rm ssl.key/server.ssl.crt/server.crt
```

+   2. Create your own server key:

```
# make genkey
```

+   3. Create the self-signed certificate by typing the following:

```
# make testcert
umask 77 :
/usr/bin/openssl req -new -key
/etc/httpd/conf/ssl.key/server.key
-x509 -days 365 -out
/etc/httpd/conf/ssl.key/server.crt
```

:
:
..

At this point, it is time to start adding some information to the certificate. Before you do this, you must unlock the private key you just created. By typing the password you typed earlier. Then follow this procedure:

> You are about to be asked to enter information that will be
Incorporated into your certificate request.
What you are about to enter is what is called
a Distinguished Name or a DN.
There are quite few fields but you can leave some blank
For some fields there will be a default value.
If you enter '.', the field will be left blank.