# 590 Linux Administration: A Beginner's Guide

This will result in the zlib library being built.

+   Install the zlib library:

```
[root@server zlib-*] make install
```

The resulting zlib will be placed in the /usr/local/lib directory.

+   Now you need to compile OpenSSL. Begin by changing to the directory to which the downloaded OpenSSL was unpacked:

```
[root@server ~] cd /usr/local/src/openssl-1.0.2*
```

+   Once in the OpenSSL directory, all you need to do is run config and make. OpenSSL will take care of figuring out the type of system it is and configure itself to work in an optimal fashion. Here are the exact commands:

```
[root@server openssl-1.0.2*] ./.config -fPIC
[root@server openssl-1.0.2*] make
```

Note that this step may take a few minutes to complete.

+   Once OpenSSL is done compiling, you can test it by running the following:

```
[root@server openssl-1.0.2*] make test
```

+   If all went well, the test should run without problems by spewing a bunch of stuff on the terminal. If there are any problems, the OpenSSL build will report them to you. If you get an error, you should remove this copy of OpenSSL and try the download/unpack/compile procedure again.

+   Once you have finished the test, you can install OpenSSL:

```
[root@server openssl-1.0.2*] make install
```

This step will install OpenSSL into the /usr/local/ssl directory.

+   Now you are ready to decompress the OpenSSH package and begin the actual compile and install of the OpenSSH package. Change into the OpenSSH package directory, like so:

```
[root@server ~]# cd /usr/local/src/openssh-7*
```

+   As with the other two packages, you need to begin running the configure program. For this package, however, you need to specify some additional parameters. Namely, you need to tell it where the other two