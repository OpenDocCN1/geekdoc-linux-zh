```
Country Name (2 letter code) [US]:
State or Province Name (full name) [WI]:
Locality Name (eg, city) [Madison]:
Organization Name (eg, company) [Reedsburg-LOG]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) [Reedsburg-LOG CA]:
Email Address [chris@linuxtoys.net]:
```

You should have two new files in the keys directory. The ca.key file holds the private key and the ca.crt key holds the new certificate generated from your KEYS values.

6.  **Create parameters for SSL/TLS:** Type the following to build the server-side Diffie-Hellman parameters needed for SSL/TLS connection:

```
# ./build-dh
Generating DH parameters, 1024 bit long safe prime, generator 2
This is going to take a long time
......+....+............................+
```

This creates a file named dh1024.pem in the keys directory.

7.  **Create server keys and certificates:** Run the following command to create the keys and certificates needed on the OpenVPN server, replacing *server1* with your server's hostname or other common name to identify it:

```
# ./build-key-server server1
Generating a 1024 bit RSA private key
..+++++
...................................................................+++++
writing new private key to 'server1.key'
.
.
A challenge password []: chzypassw77
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/2.0/openssl.cnf
.
.
Sign the certificate? [y/n]::y
1 out of 1 certificate requests certified, commit? [y/n]   y
Write out database with 1 new entries
Data Base Updated
```