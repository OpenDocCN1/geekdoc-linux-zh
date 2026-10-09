
## Authentication

*Authentication* verifies that users are who they say they are. In data communication, authenticating a sender is necessary to verify that the data came from the right source. A receiver is authenticated as well, to verify that the data is going to the right destination.

There are several methods for ensuring authentication.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_692_0.png)

| Method | Description |
|---|---|
| *The known_hosts file* | When you connect to a remote host, the host sends your public host and server keys for authentication. Your system looks up the known_hosts file to locate an entry for the host's keys, and if an entry is found, you will be granted access. |
| *SSH server* | An SSH server automatically generates public host and server keys for authentication purposes. Server keys are automatically regenerated every hour to ensure security. |
| *Challenge Handshake Authentication Protocol (CHAP)* | A security authentication protocol that encrypts the user name and password information using a key and transmits them over the network. CHAP is supported on lines using Point-to-Point Protocol (PPP) encapsulation. |
| *Password Authentication Protocol (PAP)* | A security authentication protocol for logging in to a network. With PAP, the unencrypted user name and password are transmitted over the network to the server. This information is checked against a table containing user name and password pairs of all the users on the network. PAP is supported only on PPP lines. |
| *Kerberos* | A network authentication service that is used by client/server applications. Kerberos creates a key, or ticket, for each user logging in to the network. The tickets are embedded along with the message to identify the sender. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_692_1.png)

### Authentication Factors

The number of factors that are used to show the identity of a user through authentication determines how effective authentication can be. The three types are:

- One-factor authentication, which provides what you know, such as a password or PIN. It is based on recalling a piece of information from your memory or by writing the information down. This type of authentication is the least effective.
- Two-factor authentication, which combines what you have with what you know. For example, your ATM card combined with the PIN provides access to your bank account.
- Three-factor authentication, which also provides proof of the user’s identity through biometrics. It uses physiological identification characteristics such as fingerprints, voice recognition, or signature recognition. This is the best type of authentication.

## Biometric Authentication

To increase the level of reliability of systems and ease of use to users (beyond password authentication), biometric authentication can be introduced. When this type of system is added to an authentication scheme, it is considered to be a strong authentication. The designation of strong is given because a user is not only identified digitally, but by his or her physiological characteristics, through fingerprint scanning, iris scanning, or hand geometry.

## The sshd_config File

The sshd_config file contains options to enable encrypted communication among hosts on an insecure network. SSH is implemented using the sshd daemon.

## Encryption

![](img/477ccb2f05b6ba1b2d563ea74f18c197_693_0.png)

Encryption is a method of controlling user access to information by configuring data to appear as codes that cannot be interpreted by unauthorized users. To authorized users, though, this data appears in its original form. Passwords can also be used to protect data along with encryption. There are various protocols, such as SSH, SSL, and SECURENET, that can be used to implement encryption on a network.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_693_1.png)

Figure 14-3: Securing data using encryption.

### Encryption Solutions

Authorized users of encrypted computer data must have the key that was used to encrypt the data in order to decrypt it. There are different solutions for encrypting data using specific algorithms. Some of the algorithms are described in the following table.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_694_0.png)

| Solution | Description |
| :--- | :--- |
| **Blowfish** | Blowfish is a symmetric block cipher that provides strong encryption and uses key sizes up to 56 bytes (a 448-bit key). Its features include: • Strong key support, handling, and cryptography. • Security to wipe files and clear empty disk space. |
| **3DES** | 3DES (pronounced “triple dez”) is a block cipher algorithm that can encrypt and decrypt data using a single secret key. 3DES uses three stages of DES (Data Encryption Standard), making it a very secure option. Anything encrypted by DES encryption has 72,000,000,000,000,000 (or 72 quadrillion) possible keys. |
| **MD5** | **Message-Digest algorithm 5 (MD5)** is a command-line utility that generates and verifies message digests (digital signatures) using the MD5 algorithm. The MD5 algorithm is intended for digital signature applications, where a large file must be compressed in a secure manner before being encrypted with a private (secret) key under a public-key cryptosystem. MD5 is also used to check the integrity of files. |

### Random Number Generation

**Random number generation** is an encryption method in which the kernel is used to generate random numbers that are assigned to files before transfer. Only when the numbers are matched by the recipient is the transfer completed. The algorithm that governs random number generation is the Pseudo Random Number Generation (PRNG) algorithm. In Red Hat Linux, the kernel files, /dev/random and /dev/urandom, act as the random number generators. Using the concept of permutations and combinations, these kernels are able to generate numbers with millions of digits from a single source number.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_694_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_694_2.png)

*Figure 14-4:* Securing data using the random number generation method.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_695_0.png)

## Cryptographic Hashes

Cryptographic hashes are used in an encryption method in which arbitrary data is encapsulated within a fingerprint, which is attached to a file. A fingerprint is a fixed string called the hash value, checksum, or message digest. The data in the file can be checked for authenticity by verifying the hash value. When any modifications are made to a file, its hash value also changes. There are various algorithms, such as md2, md5, sha, and sha1, that implement cryptographic hash functions.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_695_1.png)

Figure 14-5: Securing data using the cryptographic hashing method.

Various utilities are used to check the hash values of files.

| Utility | Enables You To |
| :--- | :--- |
| sha1sum | Check files for improper sha1 checksums. The syntax of this utility is sha1sum --check {file name} . |
| md5sum | Check files for improper md5 checksums. The syntax of this utility is md5sum --check {file name} . |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_695_2.png)

## Symmetric Encryption

Symmetric encryption is carried out using only a single key, which is used for both encryption and decryption. There are various utilities that perform symmetric encryption.

| Utility | Function |
| :--- | :--- |
| passwd | Used to change the login password. Users who are currently logged in can change only their login password, and not that of other users. However, this does not apply to the root user. When you type the passwd command at the command prompt, you are asked to enter your current password and then the new password you want to set. The new password is effective the next time you log in to the system. |
| gpg | Used to encrypt messages using the GNU Privacy Guard (GnuPG) encryption system. The utility has various commands and options. The syntax of this utility is gpg {options} {command} {arguments} . |
