```
```text
gacanepa@ubuntuOS:~$ sudo aptitude install libssl-dev
[sudo] password for gacanepa:
The following NEW packages will be installed:
  libssl-dev libssl-doc[zlib-dev]
0 packages upgraded, 3 newly installed, 0 to remove and 150 not upgraded.
Need to get 2,620 kB of archives. After unpacking 6,773 kB will be used.
Do you want to continue? [Y/n/?] Y
WARNING: untrusted versions of the following packages will be installed!

Untrusted packages could compromise your system's security.
You should only proceed with the installation if you are certain that
this is what you want to do.

  libssl-dev libssl-doc zlib-dev

Do you want to ignore this warning and proceed anyway?
To continue, enter "Yes"; to abort, enter "No": Yes
```
```

Figure 5.3: Installing the libssl-dev package, which provides the OpenSSL library

# 5.3 Creating, signing, and using a certificate

+   * We will create a directory to store our public key and ssl certificate (see Fig. 5.4).

```
```text
gacanepa@ubuntuOS:~$ sudo mkdir /usr/local/nginx/ssl
[sudo] password for gacanepa:
gacanepa@ubuntuOS:~$  
```
```

Figure 5.4: Creating a directory to store the public key and ssl certificate

+   * Now let’s generate the server private key (see Fig. 5.5)

```
```text
gacanepa@ubuntuOS:/usr/local/nginx/ssl$ sudo openssl genrsa -out server.key 1024
Generating RSA private key, 1024 bit long modulus
.....................................+++++++++
............................+++++++++
e is 65537 (0x10001)
gacanepa@ubuntuOS:/usr/local/nginx/ssl$ ls -l
total 4
-rw-r--r-- 1 root root 887 Nov  8 15:50 server.key
gacanepa@ubuntuOS:/usr/local/nginx/ssl$
```
```

Figure 5.5: screenshot