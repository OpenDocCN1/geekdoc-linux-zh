# # CREATING A SELF-SIGNED CERTIFICATE FOR sendmail

The default location for SSL certificates is **/etc/pki/tls/certs** (PKI stands for public key infrastructure). Working with *root* privileges, give the command `make sendmail.pem` in this directory to generate the required certificates. Apache uses a similar procedure for creating a certificate (page 970).

```
```
# cd /etc/pki/tls/certs
# make sendmail.pem
... 
Generating a 2048 bit RSA private key
................................................................++++++
writing new private key to '/tmp/openssl.snxDr0'

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:California
Locality Name (eg, city) [Default City]:San Francisco
Organization Name (eg, company) [Default Company Ltd]:Sobell Associates Inc.
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:sobell.com
Email Address []:mgs@sobell.com
..............................+++++++++
```
```

You can enter any information you wish in the certificate.

# # ENABLING SSL IN SENDMAIL

Once you have a certificate, instruct **sendmail** to use it by uncommenting (removing the leading `d1` from) the following lines in **sendmail.mc**:

```
```
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
```
```

These lines specify the authentication mechanisms.

Next, uncomment the following lines in **sendmail.mc** to tell **sendmail** where the certificate is:

```
```
define('confCACERT_PATH', '/etc/pki/tls/certs')d1
define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')d1
define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')d1
define(`confSERVER_KEY', `etc/pki/tls/certs/sendmail.pem')d1
```
```

Encrypted connections are made in one of two ways: SSL (simpler) or TLS. SSL requires a dedicated port and has the client and the server negotiate a secure connection and