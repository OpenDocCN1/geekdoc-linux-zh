
keys will appear in many places. In addition, you can put your public key fingerprint on your business card. The more places your public key appears, the better. For more information refer to “Using a Keyserver” on page 1178.

Alternatively, you can manually exchange public keys. It is poor practice to use email to give someone your public key because such an exchange can give rise to a man-in-the-middle attack (see the tip on page 1160). A better practice is to use a removable medium (e.g., a USB flash drive) to exchange keys. The following paragraphs explain how to manually exchange keys.

The following command exports public keys (`--export`) in ASCII format (`--armor`; or `-a`) to a file named `sam_pgp.asc` (`--output`; or `-o` followed by the name of the file you want to write to). If you specify a user, the command exports the public key for that user; otherwise, it exports the public keys for all users on the public keyring. Following, Sam writes his public key to `sam_pgp.asc` and then displays that file. Then he saves it on a USB flash drive and gives the drive to Max.

```bash
$ gpg --export --armor --output sam_pgp.asc sam@example.com

$ cat sam_pgp.asc

-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v1.4.14 (GNU/Linux)

mQENBFJNu8vACADPB2CrmGrkpo1VuYghUI2jKKhAabHAeavIMgGuv7i6jS6Ndt7
WJuiXu3D0qep9teJ00FZT0NZeBoWEoYI1ukmP0RNEeSIuzIGuldO2dZFP0as4x8a

...

KU2H6I-X8ktn2Ct1d7Yk7a2gjv24kiukpxXuBr5HNFZL51k3BTJYK/Pgm5cHFky
NuaZZykjq04d5Sh73ixRMPa1tXEZ32CsBhan3x8eb2985ctF5ChK8ZX52
=ItKw
-----END PGP PUBLIC KEY BLOCK-----
```

Without the `--armor` or `-a` option, gpg writes a binary file.

After Max copies Sam’s public key from the flash drive, he adds it to his keyring using the following command:

```bash
[max@guava ~]$ gpg --import sam_pgp.asc
gpg: key D26C84B3: public key "Sam Smith (Sam the Great) <sam@example.com>" imported
gpg: Total number processed: 1
        imported: 1 (RSA: 1)
```

Next, Sam follows the same procedure to add Max’s public key to his keyring. The following examples assume Sam and Max have each other’s public keys on their keyrings.

## SIGNING AND VERIFYING A FILE

Next, Sam wants to send Max a text file named `memoA`.

```bash
$ cat memoA
This is memoA.
This is memoA.
This is memoA.
This is memoA.
```

Sam wants to make sure Max knows the message is from him and that it has not been tampered with but does not care if anyone else can read it; he signs the file but does not encrypt it.

You can use one of two options to sign a file: `--clearsign` or `--detach-sign` (`-b`). The `--clearsign` option creates a clear-text signature that `gpg` appends to the file. This option is good for text files but does not work with binary files. The `--detach-sign` (`-b`) option creates a separate file that holds the signature and works with binary files. This section discusses both options.

Signing a file with either of these options does two things. It provides a digital signature that can prove who signed the file. It also generates a hash of the original file. When the recipient verifies the file, `gpg` confirms who signed the file and confirms that the file has not been tampered with.

### USING THE `--clearsign` OPTION

Sam signs the file using the `--clearsign` option, which generates a single, readable text file. The `gpg` utility requires Sam to enter his passphrase to unlock his secret key that `gpg` uses to sign the file.

```bash
$ gpg --clearsign memoA

    You need a passphrase to unlock the secret key for
    user: "Sam Smith (Sam the Great) <sam@example.com>"
    2048-bit RSA key, ID D26C84B3, created 2013-10-03

    Enter passphrase:
```

The preceding command generates the following file:

```bash
$ cat memoA.asc
    -----BEGIN PGP SIGNED MESSAGE-----
    Hash: SHA1

    This is memoA.
    This is memoA.
    This is memoA.
    This is memoA.
    -----BEGIN PGP SIGNATURE-----
    Version: GnuPG v1.4.14 (GNU/Linux)

    iQEcBAEBAGAG0BjSTcEvAAOJECQw+DSbTSzWMH/0mfjSdENMPC3yAk2jgPADc3
    ...
    wvCffxSdTEAnp7u+juIfVGk2y413rwF8v41Imbh9UFIXwGFrz30+tVGDvyPzo=
    =Xmqk
    -----END PGP SIGNATURE-----
```

Sam can verify the identity of the file (it was properly signed by himself) and message integrity (it was not tampered with) using the `gpg --verify` option. However, the message is not secret.

```bash
$ gpg --verify memoA.asc
gpg: Signature made Thu 03 Oct 2013 12:10:39 PM PDT using RSA key ID D26C8483
gpg: Good signature from "Sam Smith (Sam the Great) <sam@example.com>"
```

If the file had been altered, **gpg** would display the following message:

```bash
$ gpg --verify memoA.asc
gpg: Signature made Thu 03 Oct 2013 12:10:39 PM PDT using RSA key ID D26C8483
gpg: BAD signature from "Sam Smith (Sam the Great) <sam@example.com>"
```

When Sam sends the file to Max and Max verifies the file (using Sam’s public key, which is on his keyring), **gpg** displays the following message:

```bash
[max@guava ~]$ gpg --verify memoA.asc
gpg: Signature made Thu 03 Oct 2013 12:10:39 PM PDT using RSA key ID D26C8483
gpg: Good signature from "Sam Smith (Sam the Great) <sam@example.com>"
gpg: WARNING: This key is not certified with a trusted signature!
gpg:       There is no indication that the signature belongs to the owner.
Primary key fingerprint: 036A DE6E D653 3769 B243 A9EE 286A C3E0 D26C 8483
```

This message says that the signature and file are good based on the copy of Sam’s public key on Max’s keyring, but that the signature cannot be trusted. Someone (a man in the middle; page 1160) could have generated a key pair with Sam’s name on it, sent the public key to Max, and signed the document using the bogus private key. To be trusted, a public key must be signed; see “Signing a Public Key” on page 1177.

### USING THE `--detach-sign` OPTION

The `--clearsign` option does not work with binary files: Appending an ASCII signature to a binary file would render the file useless. Instead, the `--detach-sign` (`-b`) option creates a separate signature file that **gpg** can use to verify the source of the file and also verify that the file has not been tampered with.

Max wants to send Sam `binfile`. He wants to ensure that Sam knows the file is from him and that it has not been altered, but does not care if someone else can use the file. When Max uses the `--detach-sign` option, **gpg** prompts Max to enter his passphrase and creates a `binfile.sig` file that holds the signature. Max must send both the `binfile` and `binfile.sig` files to Sam for Sam to verify the signature (and use the file).

```bash
[max@guava ~]$ gpg --detach-sign binfile
You need a passphrase to unlock the secret key for:
user: "Max Wild <max@example.com>"
2048-bit RSA key, ID 643E62B8, created 2013-10-03
Enter passphrase:
```

```bash
[max@guava ~]$ ls -l binfile
-rwxr-xr-x. 1 max pubs 98226 10-03 12:28 binfile
-rw-r--r--. 1 max pubs     287 10-03 12:30 binfile.sig
```

Assuming Max’s public key is on Sam’s keyring, when Sam specifies the name of the signature file as an argument to **gpg**, **gpg** verifies the file and signature.

```bash
$ gpg binfile.sig

gpg: Signature made Thu 03 Oct 2013 12:30:02 PM PDT using RSA key ID 643E62B8
gpg: Good signature from "Max Wild <max@example.com>"
gpg: WARNING: This key is not certified with a trusted signature!
gpg: There is no indication that the signature belongs to the owner.
Primary key fingerprint: 92CB 8387 8439 C740 8880 6C75 72E3 1884 643E 62B8
```

Again, Max’s public key must be signed to be trusted.

### ENCRYPTING AND DECRYPTING A FILE

When you encrypt a file using a public key, only the corresponding private key can decrypt the file. If you want to send a file to someone such that only that person can read (or run) that file, you can encrypt the file using the recipient’s public key. Then the recipient can decrypt the file using her private key; no one else can read the file.

Following, Max encrypts the `memoB` file using Sam’s public key, yielding an unreadable file named `memoB.gpg`.

```bash
[max@guava ~]$ gpg --recipient sam@example.com --encrypt memoB
[max@guava ~]$ ls -l memoB
-rw-r--r--. 1 max pubs  60 10-03 12:45 memoB
-rw-r--r--. 1 max pubs 349 10-03 12:45 memoB.gpg
```

When Sam receives the file, he decrypts it using his secret key:

```bash
$ gpg --output memoB --decrypt memoB.gpg

You need a passphrase to unlock the secret key for
user: "Sam Smith (Sam the Great) <sam@example.com>"
2048-bit RSA key, ID 569BA710, created 2013-10-03 (main key ID D26C84B3)

gpg: encrypted with 2048-bit RSA key, ID 569BA710, created 2013-10-03
"Sam Smith (Sam the Great) <sam@example.com>"
```

```bash
$ cat memoB
This is memoB.
This is memoB.
This is memoB.
This is memoB.
```

### SIGNING AND ENCRYPTING A FILE

If you want to keep a file from prying eyes and ensure that it comes from the person it says it comes from and that it has not been altered, you can sign the file using your private key and encrypt it using the recipient’s public key. The recipient can then decrypt it using his private key and verify the signature using the sender’s public key.

In the next example, Max encrypts `memoC` using Sam’s public key and signs the file using his private key. The resulting file is named `memoC.gpg`. Because Max is using his private key, he must supply his passphrase.

```bash
$ gpg --recipient sam@example.com --encrypt --sign memoC

You need a passphrase to unlock the secret key for
user: "Max Wild <max@example.com>"
```
