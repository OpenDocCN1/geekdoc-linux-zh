Lastly, the programs can send and receive data using calls similar to `send()` and `recv()`. These calls have a few differences, however. First, the `flags` parameter is missing; second, if an error occurs, the function returns `-1`. The formal definition of `send()` and `recv()` states that if an error occurs, the return value is negative.

```
/***************************************************************/
/** Send & receive messages                       ***/
/***************************************************************/
int bytes;
bytes = SSL_read(ssl, buf, sizeof(buf));     /* get/decrypt */
bytes = SSL_write(ssl, msg, strlen(msg));    /* encrypt/send */
```

The API has many more functions available for controlling flow, changing SSL state, and configuration.

# ## Creating an SSL Server

The client and server differ only slightly. Both must initialize the context, establish the connection, and start the SSL protocol. The server has a couple more steps it must take. First, the context initialization changes only slightly:

```
/***************************************************************/
/** Initialize Server SSL state                     ***/
/***************************************************************/
SSL_METHOD *method;
SSL_CTX *ctx;
OpenSSL_add_all_algorithms();      /* Load cryptos, et.al. */
SSL_load_error_strings();          /* Load/register error msg */
method = SSLv2_server_method();    /* Create new server-method */
ctx = SSL_CTX_new(method);         /* Create new context */
```

You may have noticed that the program uses SSLv2, not SSLv3. You can use either. However, if you want Netscape to connect with your SSL server, it requires SSLv2. Even then, for some reason, Netscape thinks that it is connected to an SSLv3 socket.

Unlike the client, the server must load its certificate file. This comes in two parts: the certificate and the private key. You must load both as part of initialization. Both parts can reside in the same file.

```
/***************************************************************/
/** Load certificate and private key files            ***/
/***************************************************************/
/* set the local certificate from CertFile */
SSL_CTX_use_certificate_file(ctx, CertFile, SSL_FILETYPE_PEM);
/* set private key from KeyFile */
SSL_CTX_use_PrivateKey_file(ctx, KeyFile, SSL_FILETYPE_PEM);
/* verify private key */
if ( !SSL_CTX_check_private_key(ctx) )
    fprintf(stderr, "Key & certificate don't match");
```