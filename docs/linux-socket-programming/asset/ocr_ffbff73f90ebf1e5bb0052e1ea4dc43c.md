+   2.  Run the config file (./config). If it complains, you need to specify the OS type explicitly
    with ./config linux-elf.
3.  Run make to compile the sources.
4.  Run make test to verify the algorithms.
5.  Log in as root. Run make install to move the needed files into their directories
    (/usr/local/ssl/).
6.  Create references to libraries:
7.  `ln -s /usr/local/ssl/lib/libssl.a /usr/lib/`
8.  `ln -s /usr/local/ssl/lib/libcrypto.a /usr/lib/`
9.  Create the reference to include files:

    `ln -s /usr/local/ssl/include/openssl/ /usr/include`

10. Add `MANPATH /usr/local/ssl/man` to your `/etc/man.config` file. (You may want to run
    `makewhatis` to do topic searches.)
11. Add `/usr/local/ssl/bin` to your path.

One little glitch to this process is that all compilations use static libraries, so don't be surprised if your execution files start out at 600KB in size. If you want to use shared libraries, you must convert libssl.a and libcrypto.a to .so files.

After you have all this completed, you are ready to write secure sockets. The linking stage must include the libraries in a specific order. The program link fails with unresolved externals if the two libraries are swapped:

```
cc test.c -lssl -lcrypto
```

You may note that the API includes some demo C++ source files. This is overkill. All calls to the libraries can be plain C. (In fact, if you look at the source itself, you may note that it is really C source in a C++ file.)

# Creating an SSL Client

Now that you have the API installed, you can try it out by writing a simple client/server pair of programs. Creating an SSL client/server is almost as easy as creating a regular socket. In fact, OpenSSL builds on top of that framework.

The first step in the client is to set up the SSL library state:

```
```c
/****/ 
/*** Initialize Client SSL state              ***/ 
/****/ 
SSL_METHOD *method;
SSL_CTX *ctx;
OpenSSL_add_all_algorithms();        /* Load cryptos, et.al. */ 
SSL_load_error_strings();             /* Load/register error msg */ 
method = SSLv2_client_method();      /* Create new client-method */ 
ctx = SSL_CTX_new(method);          /* Create new context */ 
```
```