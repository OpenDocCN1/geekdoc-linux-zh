
you can install the certificate in the client web browser or tell your users to trust the certificate. We'll look at both ways.

Both uses of the certificate require a host key.

## TLS Host Key

Both signed and self-signed certificates require a private key for the host. The host key is just a carefully crafted random number. The following command creates a 2,048-bit host key and places it in the file `host.key`:

```
# openssl genrsa 2048 > host.key
```

You'll see a statement that OpenSSL is creating a host key and dots crossing the screen as key generation proceeds. In only a few seconds, you'll have a file containing a key. The key is a plaintext file that contains the words `BEGIN RSA PRIVATE KEY` and a bunch of random characters.

Protect your host key! Make it owned by root and readable only by root. Once you place your certificate in production, anyone who has that key can use it to eavesdrop on your private communications.

```
# chown root host.key
# chmod 400 host.key
```

Place this host key in a directory with the same permissions that we placed on the key file itself.

## Create a Certificate Request

You need a certificate request for either a signed or self-signed certificate. We don't do much with OpenSSL, so we won't dissect this command. Go to the directory with your host key and enter this verbatim:

```
# openssl req -new -key host.key -out csr.pem
```

In response, you'll see instructions and then a series of questions. By hitting `ENTER`, you'll take the default answers. If you've configured OpenSSL, the default answers are correct.

1. Country Name (2 letter code) [US]:
2. State or Province Name (full name) [Michigan]:
3. Locality Name (eg, city) [Detroit]:
4. Organization Name (eg, company) [Burke and Hare Word Mine, LLC]:
5. Organizational Unit Name (eg, section) [Pen-Monkey Division]:
6. Common Name (eg, YOUR name) [www.michaelwlucas.com]:
7. Email Address [mwlucas@michaelwlucas.com]:

The two-letter code for the country 1 is defined in the ISO 3166 standard, so a quick web search will find this for you. If you don’t know the state 2 and city 3 you live in, ask someone who occasionally leaves the server room. The organization name 4 is probably your company, and you list the department or division name 5 as well. If you don’t have a company, list your family name or some other way to uniquely identify yourself, and for a self-signed certificate, you can list anything you want. Different CAs have different standards for noncorporate entities, so check the CA’s instructions.

The common name 6 is frequently misunderstood. It’s not your name; it’s the name of the server as shown in reverse DNS. You must have a server name here, or the request will be useless.

I suggest using a generic email address 7 rather than an individual’s email address. In this case, I am michaelwlucas.com, so I might as well use my address. You don’t want your organization’s certificates tied to an individual who might leave the company for whatever reason.

Please enter the following ‘extra’ attributes to be sent with your certificate request

1. A challenge password []:
2. An optional company name []:

The challenge password 1 is also known as a passphrase. Again, keep this secret because anyone with the passphrase can use your certificate. Use of a certificate passphrase is optional, however. If you use one, you must type it when your server starts. That means that if your web server crashes, the website won’t work until someone enters the passphrase.

While passphrase use is highly desirable, this might be unacceptable. Hit `ENTER` to use a blank passphrase.

You’ve already entered quite a few company names, so a third ¹ is probably unnecessary.

Once you return to a command prompt, you’ll see the file `csr.pem` in the current directory. It looks much like your host key, except that the top line says BEGIN CERTIFICATE REQUEST instead of BEGIN RSA PRIVATE KEY.

Submit `csr.pem` to your Certificate Authority, who will return the actual certificate. I recommend saving the certificate in a file named after the host, such as `www.mrwl.io.crt`. This signed certificate is good for any TLS service, including web pages, `pop3ssl`, or any other TLS-capable daemon.

Some CAs require you use an intermediate certificate with your cert. While most daemons have a configuration option to specify an intermediate certificate, if yours doesn’t, you can append the signed certificate to the end of the intermediate cert.

### Sign a Certificate Yourself

A self-signed certificate is technically identical to a signed certificate, but it’s not submitted to a Certificate Authority. Instead, you provide the signature yourself. Most customers won’t accept a self-signed certificate on a production service, but it’s perfectly suitable for testing. To sign your own CSR, run the following:

```
# openssl x509 -req -days 365 -in csr.pem -signkey host.key \
-out selfsigned.crt
Signature ok
subject=/C=US/ST=Michigan/L=Detroit/O=Burke and Hare Word Mine, LLC/OU=Pen-Monkey Division/CN=michaelwlucas.com/emailAddress=mlucas@michaelwlucas.com
Getting Private key
#
```

That’s it! You now have a self-signed certificate good for 365 days in the file `selfsigned.crt` ². You can use this key exactly like a signed certificate, so long as you’re willing to ignore the warnings your application displays.

If you sign your own certificates, client software generates warnings that the “certificate signer is unknown.” This is expected—after all, people outside my office have no idea who Michael W. Lucas is or why he’s signing web certificates. For some reason, people trust Symantec and other big-company CAs. I’m trusted by the people who know me, but not trusted by the world at large. For this reason, don’t use self-signed certificates anywhere the public will see them because the warnings will confuse, annoy, or even scare them away.

But before you go drop any amount of money on a CA certificate, definitely check out Let’s Encrypt. It really will change your system administration practice.

## TLS Trick: Connecting to TLS-Protected Ports

I said we wouldn’t do much with OpenSSL, and that’s correct. There’s one facility the software offers that’s too useful to pass up, however, and once you know it, you’ll use this one trick at least once a month and be glad you have it.

Throughout this book, we test network services by using telnet(1) to connect to the daemon running on that port and issuing commands. This works well for plaintext services such as SMTP, POP3, and HTTP. It doesn’t work for encrypted services such as HTTPS. You need a program to manage the encryption for you when you connect to these services. OpenSSL includes the `openssl s_client` command, which is intended for exactly this sort of client debugging. While you’ll see a lot of cryptographic information, you’ll also get the ability to issue plaintext commands to the daemon and view its responses. Use the command `openssl s_client -connect` with a hostname and port number, separated by a colon. Here, we connect to the secure web server at www.absolutfreebsd.com:

```bash
# openssl s_client -connect www.michaelwlucas.com:443
CONNECTED(00000003)
depth=2 C = D, O = Digital Signature Trust Co., CN = DST Root CA X3
verify return:1
depth=1 C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3
--SNIP--
```

You’ll see lots of stuff about chains of trust and limitations of liability, as well as lines and lines of the random-looking digital certificates. After all that, however, you’ll see a blank line with no command prompt. You’re speaking directly to the server daemon. As this is a web server, let’s try an HTTP command:

```
GET /
```

The system responds with:

```
HTTP/1.1 400 Bad Request
```

The HTTP protocol has changed since the last time I tried this, I guess. But I’m definitely connected to the web server. The network works.

Some of you are probably wondering why we encrypt the service if it’s so easy to talk to the encrypted service. The encryption doesn’t protect the daemon; it protects the data stream between the client and the server. TLS encryption prevents someone from eavesdropping your network conversation in transit—it doesn’t protect either the server or the client. TLS can’t save you if someone breaks into your desktop.

From this point on, I’ll assume that you understand this OpenSSL command and what happens when we use it.

## HARDWARE CRYPTOGRAPHIC SUPPORT

Most modern hardware has built-in encryption acceleration. Unfortunately, FreeBSD doesn’t include it in the default configuration. Hardware crypto acceleration reduces load on the CPU and probably accelerates encryption. The aesni(4) kernel module activates access to Intel’s hardware cryptographic accelerator. A driver for the new AMD accelerator is in development. In-kernel drivers
