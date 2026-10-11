# Listing 7.7 Creating a new server key

```
[ramon]$ cd /etc/httpd/conf
[ramon]$ sudo make genkey
umask 77 ; \\
/usr/bin/openssl genrsa -des3 1024 >\\
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

# Listing 7.8 Creating a new server certificate

```
[ramon]$ cd /etc/httpd/conf
[ramon]$ sudo make testcert
umask 77 ; \\
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key\\
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
```