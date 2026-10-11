
![](img/7933c44717ab0711177ea7153f959fc5_83_0.png)

Fig. 3.3 Converting Cleartext into Ciphertext through Encryption

- **Confidentiality.** Allowing information to be made available only to those who are participants in a particular communication. Historically, confidentiality is the predominant use of cryptography.
- **Authentication.** The process of verifying a particular individual's identity. This is often accomplished through the use of some form of verification such as a picture identification or a fingerprint. Authentication through cryptographic means is used predominantly to validate a user's identity when other means are not available. Digital signatures offer one such cryptographic method and are very valuable in assuring that the author is in fact who he or she claims to be.
- **Integrity.** Within the context of data, an assessment of the completeness and correctness of information. In a computing environment, data integrity validation is used to ensure that the original data has not been corrupted or changed. Cryptographic one-way hash functions are commonly used to provide this functionality.

The following sections will generally describe the use of cryptography, which provides confidentiality, authentication, and integrity in computing environments.

## Algorithm Types

**Symmetric Encryption** A *symmetric* encryption algorithm is one that requires a key to encipher and to decipher messages. This is also often called a *shared-key* algorithm, because all users of such an algorithm involved in the communication must have the same key. We will refer to the shared key as a *secret key*.^[8]

There are a number of symmetric algorithms in common use today. Among them are the Data Encryption Standard (DES), the International Data Encryption Algorithm (IDEA, patented algorithm) which is incorporated in PGP, and Blowfish (an unpatented algorithm written by Bruce Schneier and incorporated in, among other tools, SSH—see Chapter 11).

One of the concerns about available symmetric algorithms is their cryptographic strength. The strength of a cryptographic algorithm is a measure of its resistance to cryptanalytic attacks. A thorough treatment of this topic may be found in the references cited in the section *Cryptography References* on page 47. In part, an algorithm’s strength is measured by the size of its key. IDEA uses a 128-bit key. Blowfish offers a user configurable key size ranging from 32 bits to 448 bits. The longer the key, the greater the cryptographic strength. DES uses a 56-bit key. It is considered a relatively weak algorithm for this and other reasons (see *Cracking DES* in the section, *Cryptography References* on page 47).

One way to increase the strength of symmetric encryption is to use multiple keys and execute the algorithm multiple times. An example implementation is that of Triple-DES (incorporated into some publicly available tools), wherein the data is first encrypted with one key, then the encrypted data is decrypted with a second key, and finally that data is encrypted with yet a third key.^[9]

The fundamental problem with the use of symmetric algorithms is the shared-key requirement. In order to successfully enter into an encrypted communication, we must first make sure that all parties to the communication have the necessary keys. There are many ways to ensure this, such as sending the key to the other parties by FAX, postal service, or courier. These methods are cumbersome at best and each has its own set of vulnerabilities. A more convenient approach, although not without vulnerabilities itself, is to use asymmetric encryption to encrypt the secret key or keys and send them electronically through the same network used to carry the encrypted communication.

### Asymmetric Encryption

An *asymmetric encryption* algorithm is one that requires one key to encrypt and a different but related key to decrypt. This type of algorithm is also often called a *public-key or two-key* algorithm. One of the two keys will be disclosed to anyone requesting it. This key is called the *public key*. The other key should never be disclosed to anyone except the owner and is known as the *private key*.^[10]

The motivation for the development of asymmetric encryption algorithms came from the need to pass secret keys over insecure channels. The first such system was developed by Ralph Merkle in 1974.^[11] The first asymmetric algorithm to gain popular use was the Diffie-Hellman algorithm, which was created by Whitfield Diffie and Martin Hellman in 1976. In 1977, Ron Rivest, Adi Shamir, and Len Adleman developed a similar algorithm called RSA.

Generally, asymmetric encryption algorithms can perform general data encryption (confidentiality) and can be used to generate digital signatures (authentication). It turns out that asymmetric algorithms are poor performers relative to symmetric algorithms. Consequently, asymmetric algorithms are most commonly used to encrypt secret keys for transmission over insecure channels and to generate digital signatures.

## Hash Functions and Digital Signatures

### One-Way Cryptographic Hash Functions

A hash function (also known as a message digest), as it generally relates to computer science, is a mathematical function that takes data as input and produces a storage address as output. The output of any hash function is simply called the hash. A cryptographic one-way hash function, or simply a one-way hash function, is a mathematical transformation having the following properties:

- It accepts variable sized data and produces a value that is fixed in size (e.g., 160 bits).
- Computation of the hash from the data is easy.
- It is computationally impractical to compute the original data given the hash.
- It is computationally unfeasible to find two similar data sets that when transformed by the function, result in the same hash (this is called collision resistance).

The whole idea behind this type of algorithm is to come up with an identifier for any given file or message that will change if someone changes the file. In this way we can use these functions to fingerprint files.

Unfortunately, since most such hash algorithms are readily available, it is possible that someone could change both the file and the hash, making it impossible to detect the change. There are a number of ways to combat this potential vulnerability. One way is to compute the hash on important files in their pristine state and store them offline. Such is the approach of Tripwire (discussed in Chapter 14) and tiger (Chapter 13). Another method is to compute, then encrypt the hash. For example, include the hash in a digital signature (see Digital Signatures on page 45). This can also be done with RPM (see RPM Resources on page 28).

One purpose of such functions is to verify the integrity of data. We explore the application of hashing for integrity purposes in our discussions of tiger and Tripwire. Another purpose of hashing is for authentication. We examine this purpose in our discussions of pluggable authentication modules (PAM—see Chapter 5) and one-time passwords (OTP—see Chapter 6).

There are a number of hash algorithms available. Among them are the RSA Data Security, Inc., MD4 Message Digest Algorithm (simply known as MD4); the RSA Data Security, Inc., MD5 Message Digest Algorithm (simply known as MD5); the Secure Hash Algorithm (SHA-1), which is part of the larger specification known as the Digital Signature Algorithm^[12] (DSA); and the Research and Development in Advanced Communication Technologies in Europe Integrity Primitives Evaluation Message Digest (RIPEMD).

### Passwords Aren't Encrypted, They're Hashed!

Another hashing algorithm is the Linux crypt(3) function. It implements a modified DES algorithm which accepts a maximum 64-bit input (8 characters) and produces a 104-bit hash value (13 characters, the first 2 of which are not part of the hash [see man 3 crypt]). This is the function used as the standard password hashing function. Each user’s 13-character hashed password is stored in /etc/shadow (or, in its absence, /etc/passwd). Quite often, the hashed password is referred to as the encrypted password. The use of the term encrypted implies that the encrypted data may be decrypted. While it may be possible to decrypt a hashed password, it is computationally difficult (perhaps impossible when MD5 is used) and it is not done. Instead, when a user enters his or her password, the password is hashed by crypt(3) and the resulting hash is compared to what is stored in /etc/shadow. For this reason, we will use the phrase hashed password instead of encrypted password throughout the book.

**Digital Signatures** *A digital signature is an authentication mechanism designed to verify the author or sender of electronic information. Digital signatures are commonly generated using asymmetric algorithms. Very frequently, digital signatures include the hash value of the signed file to verify not only the author but also the integrity of the file.*

### An Overview of PGP

Pretty Good Privacy (PGP) was written by Phil Zimmerman. It is a software package that utilizes asymmetric algorithms (RSA only in PGP version 2.6.x; RSA and Diffie-Hellman are available in PGP version 5.0 and later) for general data encryption (generally e-mail and secret keys) and for the generation and validation of digital signatures. PGP also uses IDEA for symmetric encryption of files.

---
Footnotes:
8. Some texts refer to this key as a *private* key.
9. This is one way to implement Triple-DES. There are others.
10. Some texts refer to this key as the *secret key*.
11. Ralph Merkle, *Secure Communication Over Insecure Channels*, Communications of the ACM 21, no. 4, 1978, pp. 294–299.
12. DSA is an algorithm that incorporates El Gamal for encryption and SHA-1 for hash computations. It was adopted by the National Institute of Standards and Technology (NIST) in 1991.
