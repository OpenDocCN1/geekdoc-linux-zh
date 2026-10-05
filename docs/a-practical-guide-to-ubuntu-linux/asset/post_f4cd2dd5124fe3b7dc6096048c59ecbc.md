
# 1112 APPENDIX C SECURITY

can be properly decrypted with your public key, only you could have encrypted it with your private key, proving the message is authentic. Combining these two modes of operation yields privacy and authenticity. You can sign a message with your private key so it can be verified as authentic, and then you can encrypt it with your friend's public key so that only your friend can decrypt it.

Public key encryption has three major shortcomings:

- 1. Public key encryption algorithms are much slower than symmetric algorithms and usually require a much larger key size and a way to generate large prime numbers to use as components of the key, making them more resource intensive.
- 2. The private key must be stored securely and its integrity safeguarded. If a person's private key is obtained by another party, that party can encrypt, decrypt, and sign messages while impersonating the original owner of the key. If the key is lost or corrupted, any messages previously encrypted with it are also lost, and a new keypair must be generated.
- 3. It is difficult to authenticate the origin of a key—that is, to prove whom it originally came from. This so-called key-distribution problem is the reason for companies such as VerSign (www.verisign.com).

Algorithms such as RSA, Diffie-Hellman, and El-Gamal implement public key encryption methodology. Today a 512-bit key is considered barely adequate for RSA encryption and offers marginal protection, 1024-bit keys are expected to hold off attackers for several more years. Keys that are 2048 bits long are now becoming commonplace and rated as espionage strength. A mathematical paper published in late 2001 and reclaimed in spring 2002 describes how a machine can be built—for a very large sum of money—that could break 1024-bit RSA encryption in seconds (this point is debated in an article at www.schneider.com/crypto-gan-0203.html#6). Although the cost of such a machine exceeds the resources available to most individuals and smaller corporations, it is well within the range of large corporations and governments.

# SYMMETRIC KEY ENCRYPTION

Symmetric key encryption is generally fast and simple to deploy. First you and friend agree on which algorithm to use and a key that you will. Then either you can decrypt or encrypt a file with the same key. Behind the scenes, symmetric encryption algorithms are often implemented as a network of black boxes, which can involve hardware components, software, or a combination of the two. Each box imposes a reversible transformation on the plaintext and passes to the next box, where another reversible transformation further alters the data. The security of a symmetric key algorithm relies on the difficulty of determining which boxes were used and the number of times the data was fed through the set of boxes. A good algorithm will cycle the plaintext many times before yielding the result, and there will be no obvious mapping from plaintext to ciphertext.

# ENCRYPTION 1113

The disadvantage of symmetric encryption is that it depends heavily on the availability of a secure channel through which to send the key to your friend. For example, you would not use email to send your key; if your email is intercepted, a third party is in possession of your secret key, and your encryption is useless. you could relay the key over the phone, but your call could be intercepted if someone tampered or overheard your conversation.

Common implementations of symmetric key algorithms include DES (Data Encryption Standard), 3-DES (triple DES), IDEA, RC5, Blowfish, and AES (Advanced Encryption Standard). AES is the new Federal Information Processing Standard (FIPS-197) algorithm endorsed for government use and has been selected to replace DES as the facto encryption algorithm. AES uses the Rijndael algorithm, chosen after a thorough evaluation of 15 candidates by the cryptographic community.

None of the aforementioned algorithms has undergone more scrutiny than DES, which has been in use since the 1970s. However, the use of DES has drawbacks and is no longer considered secure because the weakness of its 56-bit key makes it unreasonable to break. Given the advances in computing power and speed since DES was developed, the small size of this algorithm renders it inadequate for operations requiring more than basic security for a relatively short period of time. For a few thousand dollars, you can link off-the-shelf computer systems that can crack DES keys in a few hours.

The 3-DES application of DES is intended to combat its degenerating resilience by running the encryption three times; DES is probably sufficient for tasks as sending email to. This was not always the case: Soon after its introduction, PGP was available on many bulletin board systems, and users could implement it in any manner. PGP rapidly gained popularity in the networking community, capitalized on its encryption and management capabilities for secure transmission of email.

# ENCRYPTION IMPLEMENTATION

Most of today's encryption implementations use symmetric key, as 3-DES, IDEA, AES, or Blowfish. Finally a hash algorithm, such as DSA (Digital Signature Algorithm), generates a message signature. The security of a symmetric key algorithm relies on the difficulty of determining. Best practice is to sign someone's key only after you have met face to avert any man-in-the-middle scenario. The disadvantage of this scheme is the lack of a central registry for associating with you do not know.

# GNUPG

The most popular packages available today are GnuPG (GNU Privacy Guard; www.gnupg.org) and PGP (Pretty Good Privacy; www.pgp.com). GnuPG was designed as a replacement for PGP, a security tool that made its debut in the early 1990s. Phil Zimmerman developed PGP as Public Key Infrastructure (PKI), featuring a convenient interface, ease of use and management. Both PGP and GnuPG rely on the notion of a web of trust: When you trust someone, you verify that the person's key is authentic. By signing someone's key, you perform an operation called key signing.

After a time, attention turned to RSA and IDEA, the two robust cryptographic algorithms that form an integral part of PGP's code. These algorithms are privately owned. The wide distribution and growing user base for PGP sparked battles over patent violation and licenses, resulting in the eventual restriction. complies with the OpenPGP Message standard. Because GnuPG does not use the IDEA algorithm but rather relies on BUGS (Big and Useful Great Security; www.gnu.org/directory/bugs.html), you can use it without restriction; it is released under the GNU GPL (refer to “The Code Free” on page 5).

# APPENDIX C SECURITY 1114

Both PGP and GnuPG rely on the notion of a web of trust: When you trust someone, you verify that the person's key is authentic. By signing someone's key, you perform an operation called key signing. The disadvantage of this scheme is the lack of a central registry for associating.

- 1. For more information, the selection of The Gnu Privacy Handbook (www.gnupg.org/documentation) titled "Validating Other Keys on Your Public Keying."
- 2. Man-in-the-middle: If Max and Zach try to carry on a secure email exchange over a network, Max sends Zach his public key. However, Mr X sits between Max and Zach on the network and intercepts Max's public key. Mr. X then sends his public key to Zach. Zach then sends his public key to Max, but once again Mr. X intercepts and substitutes his public key and that. Without some kind of active protection (a piece of shared information), Mr. X, the man-in-the-middle, can decrypt all traffic between Max and Zach, reencrypt it, and send it to the other party.
