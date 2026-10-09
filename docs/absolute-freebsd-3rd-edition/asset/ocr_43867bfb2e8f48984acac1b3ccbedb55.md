You’ll see lots of stuff about chains of trust and limitations of liability, as well as lines and lines of the random-looking digital certificates. After all that, however, you’ll see a blank line with no command prompt. You’re speaking directly to the server daemon. As this is a web server, let’s try an HTTP command:

```
```
GET /
```
```

The system responds with:

```
```
HTTP/1.1 400 Bad Request
```
```

The HTTP protocol has changed since the last time I tried this, I guess. But I’m definitely connected to the web server. The network works.

Some of you are probably wondering why we encrypt the service if it’s so easy to talk to the encrypted service. The encryption doesn’t protect the daemon; it protects the data stream between the client and the server. TLS encryption prevents someone from eavesdropping your network conversation in transit—it doesn’t protect either the server or the client. TLS can’t save you if someone breaks into your desktop.

From this point on, I’ll assume that you understand this OpenSSL command and what happens when we use it.

# HARDWARE CRYPTOGRAPHIC SUPPORT

Most modern hardware has built-in encryption acceleration. Unfortunately, FreeBSD doesn’t include it in the default configuration. Hardware crypto acceleration reduces load on the CPU and probably accelerates encryption. The aesni(4) kernel module activates access to Intel’s hardware cryptographic accelerator. A driver for the new AMD accelerator is in development. In-kernel drivers