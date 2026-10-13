extract his public key to give to someone else, he might use the following command to
extract his key in binary form:

```
```bash
gpg -a --export sherman > potter.pub.key.asc
```
```

The > potter.pub.key.asc redirects the output (which would otherwise be sent to the
screen) to the file called potter.pub.key.asc. (The name of the file makes no difference at
all; it could be called foo, but it should be something that you can easily associate with its
contents, in this case Potter’s public key in ASCII armor.

> **Note**
> 
> An ASCII armored version of a key is a version in which all non-printing characters have
> been converted to a printable version. This process also makes the file approximately 30%
> larger. Should you accidentally export a binary key to your terminal, try typing `reset` to
> get back to a sane terminal.

Listing 25.2 shows what an extracted key looks like.

# Listing 25.2 — A Public Key

```
```text
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: GnuPG v1.0.1 (GNU/Linux)
Comment: For info see http://www.gnupg.org

mQGiBDlK4UsRBAcqGUwzBbzWncjnWaizpA3ak9SoNpEvBqraRjuRpTHva0B5y7qV
eboRX1pxS98g7bIOlJUZ4mdz0vgqt4hpAEc6XQiDfEJBGqERnabRph5uJnpzWjtG
ft4aIiAzqD+AnKdUbh+dRHtDauk1CtIgnns5D+yqx29t2fopH2YDpAvhuwCgj2i6
JdfTwCn91aDL9BX1kwVIB4MD/RZvvBMMvzGyUnAsfpH27j2hpDJhW4PX1t+VowHb/
I35qYBQ12hynB9g4xK3zFmr23PnkEAFKI/PhYd3f0plUFdk1QLBssEQC/eut6Nt
WJkQ74BG8fDDehBvAkr4+csnf54pMiSFw7lL1nCUqGcG++nCFuLa4sinR1Vth10
sz3DBACEi7oSn/YY4LoTnjJdAB7BGd0e/vB9DlrlGwWKUVnL7nawepWErMR39sM/
Ij1NWfZLZyvg39m+0jsf55C01Kwx1g9tUIvErnDBMPBkN1zXQ0jSVRVj9N913gpF
FJlHcn5QCRRYNTPW6Zk/92/gN4/INB9aDWNIBJrAaS5Ls0jjvLqJRGF2aWGQs4g
QmFuZGVsIDxkYZPzBEwYV95hbmI4LmVbTfEVIGqTEQiAFgCUUrShwCLGQdAXUd
AgMWaGECF4A4Ckg060BBLqhQ1TDCdFH9Ldx+dpK5IhXE4qWBYEbHk32QAnRrJ
9314YV6LEM5T/k4lCUQ5RptqUQENBDlK4VQBACDpjZDXyi7/7hBi6hYskXM4I9
JKXPZdKSmNIG0TZjCsAZJzUqj+dkKmg0fWypBjFMkg1e6nAac6B/zIFGaJ07
J2Zf7+EtLiMXB8hSqfBXORf/yHIWr/otddjJWPQZfi6iS5uB7FaqpfMBfZESrzBjkC
TBxY595nR60FTed7twADBwQAgTGGjSZQpRk11OHguBIGIAV3ynsmUGUnVrNV9
uYa7ve/UgcBbPqQF2CWU/e/gyotuZM6POGSkFOr1ABVI+0UhqTgI9x4mstBuY3Kx
gy7mPDBJfAmiczKKBiWYbjY/G3smHrgU75velJaPkvdr9KH+51AjPY9SBsk4iv
gy+IrGQYEIABgUCOUrhXQAKCRDrRW4EEUgGjZHhAJShf4JOdyE3mE+Exknva+a
frVaIwCfSHBG2PVOZgXYrcOg01gvSQ09r+s=
=uHvY
-----END PGP PUBLIC KEY BLOCK-----
```
```

To see the ID for a key, Sherman can optionally run a key verification and get a listing of
the keys in pubring.gpg using the following command:

```
```bash
gpg --list-keys
```
```

Listing 25.3 shows how the verification looks.