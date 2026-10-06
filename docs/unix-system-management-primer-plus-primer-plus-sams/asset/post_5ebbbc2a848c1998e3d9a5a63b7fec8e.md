
# 38 UNIX SYSTEM MANAGEMENT PRIMER PLUS

New userid: "Joe User <joeuser@example.com>".
New signature from keyID 0XA38C5D0 on userid Joe User <joeuser@example.com>

Added:

- new key(s)
- new signatures(s)
- new user ID(s)

# Listing Your Key Ring Contents

You can list the contents of your key ring by typing ppg -kv. Some people have many email addresses, and you can use this command if you forget under which person's key was registered in your key ring.

Nancy now signs Joe's public key, which verifies that the public key is Joe's. Otherwise PGP constantly warns you that the public key has not been proven to belong to Joe. ppg -ks signs the keys, as follows:

```bash
pgp -ks joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
```

A secret key to make a signature.
You specified no user ID to select your secret key, using default signing key set, otherwise the default user ID and will be the most recently added key on your secret keyring.
Key for user ID: Joe User <joeuser@example.com>
1024-bit DSS key 0XA38C5D0, created 2002/04/20

```
Key fingerprint = 0A 16 68 8B FD D9 0F 01 ID EF 08 AD 12 53 64 6E C
```

READABILY: Based on your direct first-hand knowledge, are you absolutely certain that you are prepared to solemnly certify that the above public key actually belongs to the user specified by the above user ID (y/N)? y
You need a phrase to unlock your secret key.
Key for user ID "nancy@example.com"
Enter pass phrase:
Passphrase is good

Finally, Nancy now can encrypt a file with Joe's public key using ppg -ea (the a is necessary to store the encrypted file in ASCII format for email transport). The syntax of ppg -ea is as-follows:

ppg -ea file userid [other users]
If Nancy wants to encrypt each message, the command to encrypt it with Joe's public-key would look like this:

```bash
pgp -ea message joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
```

# Chapter 13 IMPLEMENTING SYSTEM SECURITY

Uses the RSAREF(tm) Toolkit, which is copyrighted RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.

Recipients' public key(s) will be used to encrypt.

Key for user ID: Joe User <joeuser@example.com>
1024-bit DSS key, Key ID 0CA38C5D0, created 2002/04/20

Transport armor file: message.asc
The encrypted file is stored in message.asc, and this looks like this:

```
--- BEGIN PGP MESSAGE ---
Version: PGP 6.5.8
QAN1RDBE4DL509YCrvxQBAQ6/s0xizuenQ+Y7e2Ij3JQ0C9gecuUwboSBi4
G5N4B81p4F3ZL3u00KZt44pA2ulIFGkhzthuuyY8SAYJokKMF400pgn5mtP
Y1JB5A689Y71f17M9uAELK+kqtIGHYpJpauVv01ss38Yw7Hcd0b6dpl1gc4+cx
CCZNPGQ022XhI4FXRAE1Qub4D1Y2RAWW86HK69YwaXRfGPUSC3siJs16
JApKmIMQgN45g5ffipYk15axWI5knf1Te65S3YUR4a908f6Jb7EY/Q+L1kDG8
GyukltUA/Q2WIFFAXRI3BYXVYwLznkf1Te65SR9rwGy5hZ59yrhu5UJ9TZCL+bLIN1T9w40QibBuEI3XIa
C14MgowGpcfpkBBRGI4M55Nhm9iF50CguGh5Qhm3Mr321JnU0Y3BH4+40QibEu3XIa
N67iYEFJ3LB14/cr12/YTvVsek9w4R9055cltXwXXC5GI8EnoEz8ba4=
4uf
--- END PGP MESSAGE ---
```

Once you receive this file in email, you can decrypt it using your private key. The nice thing about PGP is that the only password you need to remember is the passphrase protecting your private key, everything else is stored in your key ring. Decryption with PGP is simple—just type filename and enter your passphrase:

```bash
$ pgp message.asc
Good Privacy (tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAREF(tm) Toolkit, which is copyrighted RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
```

File is encrypted. Secret key is required to read it.

Key for user ID: Joe User <joeuser@example.com>
1024-bit DSS key, Key ID 0CA38C5D0, created 2002/04/20
You can sign.
You need a passphrase to unlock your secret key.

Enter pass phrase:

```
Plaintext envelope: message
$ cat message
Hi Joe,
```

If you can read this, you've figured out how to use PGP!
-Nancy

# Selecting Ciphers and Port Forwarding in SSH Encryption

SSH is the de facto standard for encrypted remote access to Unix. Clients are available on all popular operating systems including Windows and Mac OS, so you don't need a Unix box on your desk to enjoy the benefits of encrypted sessions. SSH was described in detail in Chapter 12, but some additional security features, including ciphers and port forwarding, deserve further discussion.

SSH supports a healthy number of symmetric key ciphers used for the transport encryption:

- AES
- Arcfour
- Blowfish
- CAST
- DES
- Triple DES

You can use the -c option to SSH to specify one of the many ciphers available to encrypt your data. For example, to use the AES cipher with a 128-bit key and CBC checksums to connect to a system called apple, you could type

```bash
ssh -c aes128-cbc apple
```

You can find an official list of ciphers to pass this option in SSH's man page.

SSH has the ability to forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

For example, a company intranet located on a private internal network can be accessed by connecting SSH to a server on that same network and forwarding a port on the client to port 80 (HTTP) on the server. Figure 13.2 summarizes the connections.

![Figure 13.2](https://example.com/figure132.png)

# Chapter 13 IMPLEMENTING SYSTEM SECURITY

To forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

For example, a company intranet located on a private internal network can be accessed by connecting SSH to a server on that same network and forwarding a port on the client to port 80 (HTTP) on the server. Figure 13.2 summarizes the connections.

![Figure 13.2](https://example.com/figure132.png)

# Forwarding Ports

To forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

For example, a company intranet located on a private internal network can be accessed by connecting SSH to a server on that same network and forwarding a port on the client to port 80 (HTTP) on the server. Figure 13.2 summarizes the connections.

![Figure 13.2](https://example.com/figure132.png)

# Local Port Forwarding

To forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

To use local port forwarding, you map a port on your local machine to a port on a remote machine. The syntax for this is:

```bash
ssh -L local_port:remote_host:remote_port user@remote_server
```

For example, if you want to access a web server running on a remote machine at port 80 using your local machine's port 8080:

```bash
ssh -L 8080:localhost:80 user@remote_server
```

Now you can open your browser and go to `http://localhost:8080` to see the remote web server.

# Remote Port Forwarding

To forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

To use remote port forwarding, you map a port on the remote server to a port on your local machine. The syntax for this is:

```bash
ssh -R remote_port:local_host:local_port user@remote_server
```

For example, if you want the remote server's port 8080 to point to your local machine's port 80:

```bash
ssh -R 8080:localhost:80 user@remote_server
```

Now anyone who connects to the remote server on port 8080 will be redirected to your local web server.

# Dynamic Port Forwarding

To forward traffic to ports on the client or server over the encrypted connection to a system on the other side of the connection; it essentially acts as an encrypting proxy. Port forwarding is extremely useful for accessing internal resources from an external network over an encrypted connection.

Dynamic port forwarding uses the SSH connection as a SOCKS proxy. This allows you to route any application traffic through the SSH tunnel. The syntax is:

```bash
ssh -D proxy_port user@remote_server
```

For example, to set up a SOCKS proxy on port 1080:

```bash
ssh -D 1080 user@remote_server
```

Now you configure your browser to use a SOCKS proxy on localhost:1080.
