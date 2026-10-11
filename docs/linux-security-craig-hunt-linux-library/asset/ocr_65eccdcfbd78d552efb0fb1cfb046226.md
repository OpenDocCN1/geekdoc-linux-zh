In keeping with the Linux tradition of open-source software and unrestricted licensing, this chapter will concentrate on GnuPG for the remainder of the discussion.

# # Installing GnuPG

While the latest Red Hat Linux distribution includes GnuPG as part of the standard installation, most Linux distributions do not. The package is readily available in RPM format from your favorite repository. To install GnuPG, simply issue a command like the following:

```
`[ramon]$ sudo rpm -i gnupg-1.0.4-5.i386.rpm`
```

This command installs the main GnuPG executable in /usr/bin/gpg. The next section shows you how to get started with GnuPG and how to use it to encrypt and sign files and e-mail messages.

> TIP By default, the gpg executable is not suid root. While this is generally safer, it does prevent the application from "locking" its memory pages into RAM to prevent them from being swapped out to disk. This introduces a security risk because it makes it trivial for any local user to scan the swap partitions for private keys. I recommend that you make the gpg application suid root using the command sudo chmod u+s /usr/bin/gpg. This is safe because the application only uses its root privileges for the page-locking operation.

# # Configuring GnuPG

As with any public key-driven system, the first step after installing GnuPG is to create the public/private key pair that you will use to encrypt and digitally sign files and messages. To generate your first key pair, enter the following command:

```
```
[ramon]$ gpg --gen-key
public and secret key created and signed
```
```

You are prompted for a passphrase that will be used by GnuPG to protect the newly created secret key on your disk. This command automatically creates your secret *keyring*, which is a file where your secret key material is stored (`~/.gnupg/secring.gpg`, by default). In addition, it creates a public keyring (`~/.gnupg/pubring.gpg`) where you can manually add keys that are given to you by other users. It's imperative that you sign other users' public keys as you receive them, and only after you verify that they key is indeed valid for that individual. To do this, follow these simple steps, starting with the actual importing of the key:

```
```
[ramon]$ gpg --import werner.pgp
gpg: key 575480CD: public key imported
```
```