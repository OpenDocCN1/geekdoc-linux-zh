```
sslproxy.2000_Jan_29/sslproxy.c
sslproxy.2000_Jan_29/stdheaders.h
```

Since SSL Proxy comes in source format, you have to compile it using the included Makefile. Before you do that, however, make sure you have the openssl-devel RPM package, which is required by SSL Proxy. This package contains the OpenSSL header files and a library to compile applications against. Most distributions do not include openssl-devel in their standard installations, but you should be able to get the latest version from your favorite RPM archive. Once you have the RPM package, install it on your server using the following command:

```
[ramon]$ sudo rpm -i openssl-devel-0.9.5a-14.1386.rpm
```

Now you’re ready to build your SSL Proxy executable. Enter the following commands:

```
[ramon]$ cd sslproxy.2000_Jan_29
[ramon]$ make
gcc -Wall -I/usr/local/openssl/include -O -c sslproxy.c -o sslproxy.o
gcc -Wall -I/usr/local/openssl/include -0 -o sslproxy sslproxy.o \
    -L/usr/local/openssl/lib -lssl -lcrypto
[ramon]$ sudo mv sslproxy /usr/sbin/
[ramon]$ sudo chown root:root /usr/sbin/sslproxy
[ramon]$ ls -1 /usr/sbin/sslproxy
-rwxr-xr-x 1 root root 28016 Dec 19 21:35 /usr/sbin/sslproxy
```

You have now created the executable /usr/sbin/sslproxy to accept SMB requests from your private network’s Windows clients and to forward them over an SSL tunnel to a remote SMB server across the public network. The sslproxy executable takes the command-line options listed in Table 8.2.

# Table 8.2 sslproxy Command-Line Options

| Option | Meaning |
| :--- | :--- |
| -h | Display help information. |
| -L local-address | Address where proxy should bind (0.0.0.0 is default) |
| -l port | Port where proxy should bind |

Application
Security
PART 3