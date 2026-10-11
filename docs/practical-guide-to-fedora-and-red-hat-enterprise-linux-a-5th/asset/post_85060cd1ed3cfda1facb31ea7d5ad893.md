
## Encryption Implementation

security of a symmetric key algorithm relies on the difficulty of determining which boxes were used and the number of times the data was fed through the set of boxes. A good algorithm will cycle the plaintext through a given set of boxes many times before yielding the result, and there will be no obvious mapping from plaintext to ciphertext.

The disadvantage of symmetric key encryption is that it depends heavily on the availability of a secure channel through which to send the key to your friend. For example, you would not use email to send your key; if your email is intercepted, a third party is in possession of your secret key, and your encryption is useless. You could relay the key over the phone, but your call could be intercepted if your phone were tapped or someone overheard your conversation.

Common implementations of symmetric key algorithms include DES (Data Encryption Standard), 3-DES (triple DES), IDEA, RC5, Blowfish, and AES (Advanced Encryption Standard). AES is the new Federal Information Processing Standard (FIPS-197) algorithm endorsed for governmental use and has been selected to replace DES as the de facto encryption algorithm. AES uses the Rijndael algorithm (www.rijndael.com), chosen after a thorough evaluation of 15 candidate algorithms by the cryptographic research community.

None of the aforementioned algorithms has undergone more scrutiny than DES, which has been in use since the late 1970s. However, the use of DES has drawbacks and it is no longer considered secure, as the weakness of its 56-bit key makes it unreasonably easy to break. Because of the advances in computing power and speed since DES was developed, the small size of this algorithm’s key renders it inadequate for operations requiring more than basic security for a relatively short period of time. For a few thousand dollars, you can link off-the-shelf computer systems so that they can crack DES keys in a few hours.

The 3-DES application of DES is intended to combat its degrading resilience by running the encryption three times; it is projected to be secure for years to come. DES is probably sufficient for such tasks as sending email to a friend when you need it to be confidential or secure for only a few days (for example, to send a notice of a meeting that will take place in a few hours). It is unlikely that anyone is sufficiently interested in your email to invest the time and money to decrypt it. Because of 3-DES’s wide availability and ease of use, it is advisable to use it instead of DES.

Most of today’s commercial software packages use both public and symmetric key encryption algorithms, taking advantage of the strengths of each and avoiding their weaknesses. The public key algorithm is used first, as a means of negotiating a randomly generated secret key and providing for message authenticity. Then a secret key algorithm, such as 3-DES, IDEA, AES, or Blowfish, encrypts and decrypts the data on both ends for speed. Finally a hash algorithm, such as DSA (Digital Signature Algorithm), generates a message digest that provides a signature that can alert you to tampering. The digest is digitally signed with the sender’s private key.

## GnuPG/PGP

The most popular personal encryption packages available today are GnuPG (GNU Privacy Guard, also called GPG; www.gnupg.org) and PGP (Pretty Good Privacy; www.pgp.com). GnuPG was developed as a free replacement for PGP, a security tool that made its debut during the early 1990s. Phil Zimmerman developed PGP as a Public Key Infrastructure (PKI), featuring a convenient interface, ease of use and management, and the security of digital certificates. One critical characteristic set PGP apart from the majority of cryptosystems then available: PGP functions entirely without certification authorities (CAs). Until the introduction of PGP, PKI implementations were built around the concept of CAs and centralized key management controls.

PGP and GnuPG rely on the notion of a ring of trust: If you trust someone and that person trusts someone else, the person you trust can provide an introduction to the third party. When you trust someone, you perform an operation called *key signing*. By signing someone else’s key, you verify that the person’s public key is authentic and safe for you to use to send email. When you sign a key, you are asked whether you trust this person to introduce other keys to you. It is common practice to assign this trust based on several criteria, including your knowledge of a person’s character or a lasting professional relationship with the person. The best practice is to sign someone’s key only after you have met face to face to avert any chance of a man-in-the-middle scenario. The disadvantage of this scheme is the lack of a central registry for associating with people you do not already know.

PGP is available without cost for personal use, but its deployment in a commercial environment requires the purchase of a license. This was not always the case: Soon after its introduction, PGP was available on many bulletin board systems, and users could implement it in any manner they chose. PGP rapidly gained popularity in the networking community, which capitalized on its encryption and key management capabilities for secure transmission of email.

After a time, attention turned to the two robust cryptographic algorithms, RSA and IDEA, which form an integral part of PGP’s code. These algorithms are privately owned. The wide distribution of and growing user base for PGP sparked battles over patent violation and licenses, resulting in the eventual restriction of PGP’s use. Enter GnuPG, which supports most of the features and implementations made available by PGP and complies with the OpenPGP Message Format standard.

2. For more information, see the section of *The GNU Privacy Handbook* (www.gnupg.org/docs.html) titled “Validating Other Keys on Your Public Keyring.”

3. Man-in-the-middle: If Alex and Jenny try to carry on a secure email exchange over a network, Alex first sends Jenny his public key. However, suppose that Mr. X sits between Alex and Jenny on the network and intercepts Alex’s public key. Mr. X then sends *his own* public key to Jenny. Jenny then sends her public key to Alex, but once again Mr. X intercepts it and substitutes *his own* public key and then sends that to Alex. Without some kind of active protection (a piece of shared information), Mr. X, the *man-in-the-middle*, can decrypt all traffic between Alex and Jenny, reencrypt it, and send it on to the other party.

Because GnuPG does not use the patented IDEA algorithm but rather relies on BUGS (www.gnu.org/directory/bugs.html), you can use it almost without restriction: It is released under the GNU GPL (refer to “The Code Is Free” on page 4). PGP and GnuPG are considered to be interchangeable and interoperable. The command sequences for and internal workings of these two tools are very similar.

### The GnuPG system includes the gpg program

> tip: GnuPG is frequently referred to as gpg, but gpg is actually the main program for the GnuPG system.

GNU offers a good introduction to privacy, The GNU Privacy Handbook, which is available in several languages and listed at www.gnupg.org (click Documentation→Guides). Click Documentation→HOWTOs on the same Web page to view the GNU Privacy Guard (GnuPG) Mini Howto, which steps through the setup and use of gpg. And, of course, there is a gpg info page.

In addition to encryption, gpg is useful for authentication. For example, you can use it to verify that the person who signed a piece of email is the person who actually sent it.

## FILE SECURITY

From an end user's perspective, file security is one of the most critical areas of security. Some file security is built into Linux: chmod (page 204) gives you basic security control. ACLs (Access Control Lists) allow for more fine-grained control of file access permissions. ACLs are part of Solaris, Windows NT/2000/XP, VAX/VMS, and mainframe operating systems. Fedora/RHEL supports ACLs (page 207). Even these tools are insufficient, however, when your account is compromised (for example, by someone watching your fingers on the keyboard as you type your password). To provide maximum file security, you must encrypt your files. Then even someone who knows your password cannot read your files. (Of course, if someone knows your key, that person can decrypt your files if he or she can get to them.)

## EMAIL SECURITY

Email security overlaps with file security and, as discussed later, with network security. GnuPG is the tool most frequently used for email security, although you can also use PGP. PEM (Privacy Enhanced Mail) is a standard rather than an algorithm and is used less frequently.

## MTAs (MAIL TRANSFER AGENTS)

An increasingly commonplace MTA is STARTTLS (Start Transport Layer Security; www.sendmail.org/~ca/email/starttls.html). TLS itself usually refers to SSL (Secure
