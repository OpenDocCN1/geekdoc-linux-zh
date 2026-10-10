
# 38 UNIX SYSTEM MANAGEMENT PRIMER PLUS

```bash
$ bash md5 apache_1.3.24.tar.gz
beea658c3954731fcc31bd29bc82429 apache_1.3.24.tar.gz
```

The checksums match, so you know your source code is authentic.

# Don't Put All Trust in Checksums

![](img/894492738e879267320b8d6f9a044180_405_0.png)

Although checksums are a highly reliable form of verification, someone could easily hack into a Web server, replace files with viruses or other malicious code, and recalculate the checksums. This situation is highly unlikely, but it illustrates how you cannot blindly trust checksums—always check the contents of files you download before compiling or executing them.

# Using One-Way Hashes for Password Authentication

The Unix crypt function encrypts Unix passwords for storage in /etc/passwd or /etc/shadow files (and NIS). The values stored in these files are not truly encrypted, though; they are 13-character hashes of the password. For example, in one particular instance, the string “password” results in a hash of “I3GSYBVIQ”. The first two letters in the hash are known as salt, which is used to randomly vary the hash algorithm between runs so that the same string is unlikely to produce the same hash. This variability makes it more difficult for a hacker to quickly create a dictionary of passwords and hashes.

When a user authenticates using his or her password, the salt is extracted from the hash and used to hash the password that was just entered. If that hash matches the original password hash, the user has entered the correct password and is allowed to log in.

# Using the crypt Command Encryption Tool

There are a number of tools and features on Unix that provide cryptographic functionality. One of the oldest Unix encryption commands is crypt, which is still available today on Solaris. It is good for casual encryption of files if you have nothing else available, but you should not consider it be industrial strength by any means. Its usage is as follows:

```
crypt [password]
```

crypt takes its data from standard input and outputs to the standard output. It asks you for a password if none is provided on the command line (typing passwords on the command line is very insecure). crypt performs file encryption and decryption in the same manner. To encrypt /etc/passwd and place the output into /tmp/passwd.enc, you could type

```bash
bash$ crypt < /etc/passwd > /tmp/passwd.enc
```

You are asked for a password that will be used to encrypt the file. To decrypt the file, type the following:

```bash
bash$ crypt < /tmp/passwd.enc
```

You next are asked for the password you used to encrypt the original file.

# Pretty Good Privacy (PGP) Encryption

PGP stands for Pretty Good Privacy and was written by Phil Zimmermann in 1994. PGP is a public key encryption system that flourished in the late 1990s as the number one method of email encryption, primarily because it was the most powerful and convenient at the time. The technology since been acquired by Network Associates (http://www.nai.com), which resells the technology commercially PGP continues to employ a large user base, especially in corporate and academic environments. Free versions of PGP still exist; you can download versions for Linux, Solaris, HP-UX, and AIX from http://web.mit.edu/network/pgp.html.

PGP made it easy for every user to use public key encryption on all operating systems, including Unix. To use PGP, a user must generate a key pair with pg -kg. This example creates a new key pair for Joe User (using the free version from www.mit.edu):

```bash
bash$ pg -kg
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAAREF(tm) Toolkit, which is copyrighted RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
```

Choose the public-key algorithm to use with your new key

- 1) DSS/DH (a.k.a. DSS/EGamal) (default)
- 2) RSA

Choose 1 or 2: 1

Choose the type of key you want to generate

- 1) Generate a new signing key (default)
- 2) Generate an encryption key for an existing signing key

Choose 1 or 2: 1

Pick your 'master key' size:

- 1) 1024 bits - Maximum size (Recommended)

Choose 1 or enter desired number of bits: 1
Generating a 1024-bit DSS key.

You need a user ID for your public key. The desired form for this user ID is your name, followed by your E-mail address enclosed in <brackets>, if you have an E-mail address.

For example: John Q. Smith <smith@gmail.com>
Enter a user ID for your public key: Joe User <joeuser@example.com>

Enter the validity period of your signing key in days 0 - 10950
0 is forever (the default is 0): 0

You need a pass phrase to protect your DSS secret key.
Your pass phrase can be any sentence or phrase and may have many words, spaces, punctuation, or any other printable characters.

Enter pass phrase:
Enter same pass phrase again:

PGP will generate a signing key. Do you also require an encryption key? (Y/n) Y

Pick your DH key size:

- 1) 1024 bits- High commercial grade, secure for many years
- 2) 2048 bits- "Military" grade, secure for foreseeable future
- 3) 3072 bits- Archival grade, slow, highest security
Choose 1, 2, 3, or enter desired number of bits: 1

Enter the validity of your encryption key in days from - 10950
0 is forever (the default is): 0

Note that key generation is a lengthy process.
PGP needs to generate some random data. This is done by measuring
time intervals between your keystrokes. Please enter some
random text on your keyboard until the indicator reaches 100%.
Press "D to cancel

100% of required data
Enough, thank you.

******
Make this the default signing key? (Y/n) y
******

Key generation completed.

The key generation process looks complicated, but most users can simply accept the defaults.
You must remember the passphrase to enter into your private key; however, without it,
You won't be able to decrypt anything!

![](img/894492738e879267320b8d6f9a044180_407_0.png)

# PGP Requires True Randomness

PGP is concerned with the randomness of your key pair that it does not trust the operating sys-tem's random number generator. Instead, PGP measures the time between the keystrokes you enter
uses that measurement to generate more randomness than a computer could ever provide.

Joe's key pair and other public keys that he uses to encrypt files are stored in Joe's ring. To
receive encrypted files, Joe User needs to extract his public key from his key ring in ASCII-format The pg -kxa command does, as follows:

```bash
bash5gpg -kxa joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
```

Uses the RSAREF(tm) Toolkit, which is copyrighted RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.

Extract from key '/home/joeuser/.pubring', "joeuser@example.com".
Extract above key into file: joeuser.asc

The public key in joeuser.asc looks like this:

```
--- BEGIN PGP PUBLIC BLOCK ---
Version: PGP 6.5.8
```
```
QGBIB0zQmQMRBADE/x0Fr0VsJGqQWFD0063jWYK4IUK6B00/3OybQHN
4QpJQkLDbE0ilJ4800jwUKH4B7apuri+r1+F0550g40USjKhAwlA
dSjv09V17E860A/S80wBsJ2I006m8/A1aFeI1c0M440011
```
