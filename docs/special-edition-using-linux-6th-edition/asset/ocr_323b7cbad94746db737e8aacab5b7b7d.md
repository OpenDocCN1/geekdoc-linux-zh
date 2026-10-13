Different ways to sign files are available. For example, if Sherman just wants to sign the encryptme file and send it to John, he can use the following command:

```
gpg -b signme
```

This says to sign the signme file (specifies the ID that is doing the signing) and make the resulting file binary (the default). Of course, the file is not readable in this state because it is not ASCII. To make it a signed ASCII armored file instead, use the following command:

```
gpg -ba signme
```

The resulting file looks similar to Listing 25.4.

# LISTING 25.4. GPG SIGNED FILE WITH ASCII ARMORING (ENCODED)

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.0.1 (GNU/Linux)
Comment: For info see http://www.gnupg.org

iEYEABECAAYFAj1NktMACgkQ60COBBLqho2/fACfWAD+140hZH02emtCA2cJgF9o
g8IAnifn/yI2X0Y0m2mmdEx85ImlgY1Z
=/c0p
-----END PGP SIGNATURE-----
```

The -b option creates a detached signature file. The signature file carries the same name as the file signed, but with either a .gpg suffix, or an .asc suffix, depending on whether simple (binary) or ASCII armored signing was specified.

# ENCRYPTING FILES

Imagine that you have a public key from someone else and you want to encrypt something for that person. The key has been added to the public key ring, a file is ready to be encrypted, and all that is needed is a command to encrypt it.

The following command does the trick:

```
gpg -r recipient -e filename
```

The recipient parameter (-r) needs to be enough of an identifier to allow GPG to locate the ID in its public key ring. For instance, use Sherman's signme file as an example again:

> John,
> 
> Something fishy is going on here...
> Can you come over and check it out?
> 
> Thanks...
> 
> Sherman

The following command can be executed by Sherman to encrypt the signme file in such a way that only John can read it:

```
gpg -r john -e signme
```