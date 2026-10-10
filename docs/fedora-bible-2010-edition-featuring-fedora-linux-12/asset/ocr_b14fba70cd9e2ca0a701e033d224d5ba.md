# Chapter 13: Computer Security Issues

C2klbXNlCnYuY29tMIGFMA0GCSqGSIb3dQEAQUAANQDADCB4IQKBgQdDaHSk+uzOf 
7/jDPEnQ78UBai1LyPFILKXfjhj3XpXLGW2LmkDmdzj7Xsa4x7AhErplubuNVhjVI0 
FnlDopax4pyr4nn+P8FYm54MS9crbcZykZ1mK2Q1yqz9F/7yOWpD13Qtc4eqYCrazQ 
g9hTXD2/BO4twvCAFCwUWbOQuLCNVZqojDABQBo4AI3TCTCASSCQ5EVDY07TBA7n
ADBEBSgVHGSAFP7XDKAG2C0SAQCCSUBBCsXDMC6wkAYlIKoYBROBuqGZKWhClOJh8g
O18vtzid3lnZ1cmlzlaMUdLdmNvfbS9ycGBwCQWVRBRpBQDRdqMwcGmgCgdIUdqQDHW88g
CWSOSAG+BIEMOGoCwIYBQUaHBCC&C#5aD1FVbmBMQCCmcGAQUPBwBEBcwJiAQ 
BqgBEBFEGQcVWYYAaHRCvDoVvLL29jC2AcudVyaXNP224uY2tMEYGA1UDhW0w/MO 
O6AsODenGNHWOdHA6L9jc mwdudVNvqaZN24uY2tLN8sYXN6M0LulGViJyBmFWa 
B1Ll2XnAr+aChESR0Lb3Qrjgv2yLmwjjkPMCJWjceYfdX4H+Mbg/61QmmK9auWAT
WFo1FW/+a8OWRQJQLMA2QOQVhX4zNj6pGCNVYAQQSHumIlESj7vt4d1LX
----- END CERTIFICATE -----

Copy and paste this certificate into an empty file called server.crt, which must reside in the /etc/pki/tls/certs directory, and restart your Web server.

```
# service httpd restart
```

Assuming your Web site has previously working fine, you can now view it in a secure fashion by placing an "s" after the http in the Web address. So if you previously viewed your Web site at http://www.acmemarina.com, you can now view it in a secure fashion by going to https://www.acmemarina.com.

# Creating self-signed certificates

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
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key \
    -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt 
. 
. 
.
```

At this point, it is time to start adding some identifying information to the certificate. Before you can do this, you must unlock the private key you just created. Do so by typing the password you typed earlier. Then follow this sample procedure:

> You are about to be asked to enter information that will be 
> incorporated into your certificate request.