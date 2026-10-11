
gpg: /home/ramon/.gnupg/trustdb.gpg: trustdb created
gpg: Total number processed: 1
gpg: imported: 1

Note that when you import this key, GnuPG reports the key ID as **57548DCD**. Use this or the key holder’s e-mail address in all subsequent operations on this public key, or you can use the key holder’s e-mail address also. Next, display the key fingerprint as in the next example, and verify it with the owner out of band (e.g., in person or by phone):

```
[ramon]$ gpg --fingerprint 57548DCD
pub  1024D/57548DCD 1998-07-07 Werner Koch (gnupg sig)
    <dd9jn@gnu.org>
Key fingerprint = 68D9 050F D8FC 941B 4341 2DCC 68B7 AB89 5754 8D0D
```

If the fingerprint matches, you should sign the key on your public keyring:

```
[ramon]$ gpg --edit-key 57548DCD
gpg (GnuPG) 1.0.2; Copyright (C) 2000 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.

pub  1024D/57548DCD  created: 1998-07-07  expires: 2002-12-29
trust: -/q
(1)   Werner Koch (gnupg sig) <dd9jn@gnu.org>

Command> sign

pub  1024D/57548DCD  created: 1998-07-07  expires: 2002-12-29
trust: -/q
            Fingerprint: 68D9 050F D8FC 941B 4341 2DCC 68B7
            AB89 5754 8D0D

      Werner Koch (gnupg sig) <dd9jn@gnu.org>

Are you really sure that you want to sign this key
with your key: "Ramón J. Hontanon (Linux Student)"
<rhontanon@sybex.com>"

Really sign? y

You need a passphrase to unlock the secret key for
user: "Ramon J. Hontanon (Linux Student)
            <rhontanon@sybex.com>"
1024-bit DSA key, ID 3C9EA164, created 2000-11-29
```

You now have a public/private key pair of your own, as well as the (verified and signed) public signature of one of your peers. These are the basic ingredients for the operation of GnuPG.

### Using GnuPG

While there are a number of Linux MUAs that include transparent GnuPG support (Mutt, Pine, and VM, for example), this section will discuss the command-line use of the gpg utility. This is important because most MUAs support GnuPG by piping messages in and out to gpg using the command-line options that discussed in this section. Table 6.2 lists the most commonly used gpg command-line options.

| **Option** | **Meaning** |
|---|---|
| --encrypt | Encrypt the message. |
| --armor | Use ASCII for the encryption output. |
| --clearsign | Sign the message to a cleartext file. |
| --sign | Sign the message (use in conjunction with the --encrypt option). |
| --decrypt | Decrypt the message. |
| --verify | Verify a signature. |
| --list-keys | Show keys in your public keyring. |
| --list-secret-keys | Show keys in your private keyring. |

## Examples

Consider as an example an e-mail message whose text is in the file `message.txt`. You want to digitally sign the message before sending it so that the recipient can be assured that it came from you. Enter the following commands to sign your message:

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

Note that GnuPG prompts you for the passphrase to unlock your secret key. This is because the signing algorithm needs to use the private key to generate a signature. Conversely, the recipient of the message needs your public key to verify that your message is really signed with your private signature:

```bash
[stacia]$ gpg --verify message.txt.asc
gpg: Signature made Wed Nov 29 21:12:23 2000 EST using DSA key
ID 3C9EA164
gpg: Good signature from 'Ramon J. Hontanon (Linux Student)
<rstanton@sybex.com>'
```

Consider the case where you want to ensure both the privacy and the integrity of a message. The following command signs and encrypts the message contained in the file `message.txt`:

```
[ramon]$ gpg --encrypt --sign --armor message.txt

You need a passphrase to unlock the secret key for
user: 'Ramon J. Hontanon (Linux Student)
<rstanton@sybex.com>'

1024-bit DSA key, ID 3C9EA164, created 2000-11-29

You did not specify a user ID. (you may use "-r")

Enter the user ID: stacia@example.com
```

When Stacia receives the message, she then uses her gpg utility to decrypt and verify the signature of the resulting message.txt.asc document:

```
[stacia]$ gpg --decrypt message.txt.asc

You need a passphrase to unlock the secret key for
user: 'Stacia S. Hontanon (Linux Master)
<stacia@example.com>

1024-bit ELG-E key, ID A0626845, created 2000-11-29 (main key
ID 3C9EA034)

This is just a test message. We would like to ensure the integrity
of this message by attaching a digital signature to it.

Regards,

-- ramon
gpg: Signature made Wed Nov 29 21:21:54 2000 EST using DSA key
ID 3C9EA164
gpg: Good signature from 'Ramon J. Hontanon (Linux Student)
<rjhontanon@sybex.com>'
```

In this example, the output of the decryption/verification simply goes out to the screen. If you would like for the output to be directed to the file `message.txt`, simply use the following command (note the `--output` directive):

```
[stacia]$ gpg --output message.txt --decrypt message.txt.asc
```

As you can see, GnuPG is a comprehensive package that includes utilities to encrypt, decrypt, sign, and verify any type of document (including e-mail messages), as well as the tools to manage the private and public keys required to provide this service.

A tool like GnuPG is not only useful for securing e-mail exchanges, but it’s also an additional privacy measure for protecting critical files that you need to store on your Linux server. I recommend that you use GnuPG to encrypt sensitive network topology diagrams, notes containing authentication passwords, and reports of network audits that reveal any vulnerabilities, at least until you’ve had a chance to address them.

## In Sum

A layered approach to application security calls for mechanisms to ensure the privacy and authentication of the application transport (e.g., SSL) and the content of the packets themselves by applying encryption and digital signatures to the data before the traffic even hits the wire (e.g., GnuPG).

This is especially relevant in the case of electronic mail applications, due to the sheer volume of traffic that they handle and the increasingly sensitive content for which companies rely on electronic mail. Regardless of your choice of MTAs, you need to make sure that your mail user agents (clients) support the same type of privacy and authentication mechanisms as your transport agent. It’s also imperative to make sure that your users receive the training they need to use the application in accordance with your security policy.

Electronic mail and Web browsing make up the bulk of the traffic traversing the Internet today. Chapter 7, “HTTP Services,” continues the discussion on application layer security by examining the security issues surrounding the three types of open-source HTTP servers available for Linux servers.

![](img/3258bbaf790525f8c4eb25fabff7844a_199_0.png)

# 7 HTTP Services

This chapter continues the discussion of Part 3, “Application Security,” by taking an in-depth look at the Apache HTTP server, the dominant force behind the Web server explosion of the last five years. This chapter describes the overall security features of the base Apache package, as well as the standard authentication and access control configuration.

While system and network layer security can contribute to sealing most of the low-level threats to your Linux server, the harsh reality is that a service like HTTP requires you to open up a number of ports (TCP 80 and sometimes TCP 443) to the Internet population at large. This forces you to implement a complete set of security measures at the application layer, including authentication, access control, and the protection of the HTTP application server itself.

In addition, if your company conducts electronic commerce using your HTTP server, you’ll need to ensure the privacy of the transactions, as well as provide strong authentication to your prospective customers and business partners. This can be addressed using SSL (Secure Sockets Layer) extensions to the base Apache HTTP distribution. This chapter describes two different packages that you can deploy to ensure the privacy and authentication of your HTTP transactions:

- mod_ssl (part of the OpenSSL initiative)
- Apache-SSL, on which mod_ssl was originally based

Let’s kick off the discussion by describing the security-specific issues at play when you install, configure, and maintain the Apache HTTP server.
