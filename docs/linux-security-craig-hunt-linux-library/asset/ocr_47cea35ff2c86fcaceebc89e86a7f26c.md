# Examples

Consider as an example an e-mail message whose text is in the file `message.txt`. You want to digitally sign the message before sending it so that the recipient can be assured that it came from you. Enter the following commands to sign your message:

```
```bash
[ramon]$ gpg --clearsign message.txt
You need a passphrase to unlock the secret key for: "Ramon J.
Hontanon (Linux Student) <rhontanon@sybex.com>"
1024-bit DSA key, ID 3C9EA164, created 2000-11-29

[ramon]$ cat message.txt.asc
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

This is just a test message. We would like to ensure the integrity
of this message by attaching a digital signature to it.

Regards,

-- ramon
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.0.2 (GNU/Linux)
Comment: For info see http://www.gnupg.org

iD8D8QE6JbeHnwa9rjey0wQRAhnSAj9WtkILSphi22IrSWHoDpIG2bb8W0gCgH+uB
I/au/YZbCRdhhVpoxSwGJWo=
=peFj
-----END PGP SIGNATURE-----
```
```

Note that GnuPG prompts you for the passphrase to unlock your secret key. This is because the signing algorithm needs to use the private key to generate a signature. Conversely, the recipient of the message needs your public key to verify that your message is really signed with your private signature:

```
```bash
[stacia]$ gpg --verify message.txt.asc
gpg: Signature made Wed Nov 29 21:12:23 2000 EST using DSA key
ID 3C9EA164
```
```