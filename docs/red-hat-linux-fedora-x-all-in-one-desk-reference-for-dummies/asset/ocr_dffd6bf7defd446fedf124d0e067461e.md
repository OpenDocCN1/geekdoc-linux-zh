# Encrypting and Signing Files with GnuPG 553

# Signing a file

You may find signing files useful if you send out a file to someone and want to assure the recipient no one tampered with the file and you sent the file GPG makes signing a file very easy. When you compress and sign a file named message with the following command:

```
gpg -o message.sig -s message
```

To verify the signature,

```
gpg --verify message.sig
```

To get back the original document, simply type

```
gpg -o message --decrypt message.sig
```

Sometimes you don't care about keeping a message secret, but simply want to sign it out that the message is from you. In such a case, you can generate and append a clear-text signature with the following command:

```
gpg -o message.asc --clearsign message
```

This basically attaches a clear-text signature to the text message. Here's a typical clear-text signature block:

> -----BEGIN GPG SIGNATURE-----
Version: GPG v1.2.4 (GNU/Linux)
idDB0BFAfdDHOH/bud6KS5MRRAO5VAJSGS1waZ36P0JWKZZVSDVCMjphZFACEIYFBYSZMEEDawAtHeq6IM=-yu0=
-----END GPG SIGNATURE-----

When a message has a clear-text signature appended, you can use GPG to verify the signature with the following command:

```
gpg --verify message.asc
```

The last line of the output says that it's a good signature.

# Encrypting and decrypting documents

To encrypt a message meant for a recipient, you can use the --encrypt (or -e) GPG command. Here's how you might encrypt a message for me if you had my public GPG key:

```
gpg -o message.gpg -e r naba@comcast.net message
```