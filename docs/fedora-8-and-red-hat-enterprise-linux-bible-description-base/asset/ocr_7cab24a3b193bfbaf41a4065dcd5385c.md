Copy and paste this certificate into an empty file called `server.crt`, which must reside in the `/etc/pki/tls/certs` directory, and restart your Web server:

```
# service httpd restart
```

Assuming your Web site was previously working fine, you can now view it in a secure fashion by placing an “s” after the http in the Web address. So if you previously viewed your Web site at http://www.acmemarina.com, you can now view it in a secure fashion by going to https://www.acmemarina.com.

# ## Creating self-signed certificates

Generating and running a self-signed SSL certificate is much easier than having a signed certificate. To generate a self-signed SSL certificate, do the following:

+   1.  Remove the key and certificate that currently exist:

```
# rm /etc/pki/tls/certs/localhost.crt
# rm /etc/pki/tls/private/localhost.key
```

+   2.  Create your own server key:

```
# make genkey
```

+   3.  Create the self-signed certificate by typing the following:

```
# make testcert
umask 77 ; \
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key
    -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
...
```

At this point, it is time to start adding some identifying information to the certificate. Before you can do this, you must unlock the private key you just created. Do so by typing the password you typed earlier. Then follow this sample procedure:

> You are about to be asked to enter information that will be incorporated into your certificate request. What you are about to enter is what is called a Distinguished Name or a DN. There are quite a few fields but you can leave some blank For some fields there will be a default value, If you enter '.', the field will be left blank.
> -----
> Country Name (2 letter code) [GB]:US
> State or Province Name (full name) [Berkshire] : Ohio
> Locality Name (eg, city)  [Newbury]: Cincinnati
> Organization Name (eg, company) [My Company Ltd]:Industrial Press, Inc.
> Organizational Unit Name (eg, section) []:RT