# # ENCRYPTION IMPLEMENTATION

Most of today's commercial software packages use both public and symmetric key encryption algorithms, taking advantage of the strengths of each and avoiding their weaknesses. The public key algorithm is used first, as a means of negotiating a randomly generated secret key and providing for message authenticity. Then a secret key algorithm, such as 3-DES, IDEA, or Blowfish, encrypts and decrypts the data on both ends for speed. Finally a hash algorithm, such as DSA (Digital Signature Algorithm), generates a message digest that provides a signature that can alert you to tampering. The digest is digitally signed with the sender's private key.

# # GnuPG/PGP

The most popular personal encryption packages available today are GPG (GNU Privacy Guard, also called GnuPG; www.gnupg.org) and PGP (Pretty Good Privacy; www.symantec.com/business/theme.jsp?themeid=pgp). GPG was designed as a free replacement for PGP, a security tool that made its debut during the early 1990s. Phil Zimmerman developed PGP as a PKI (Public Key Infrastructure), featuring a convenient interface, ease of use and management, and the security of digital certificates.

One critical characteristic set GPG apart from the majority of cryptosystems then available: PGP functions entirely without CAs (certification authorities). Until the introduction of PGP, PKI implementations were built around the concept of CAs and centralized key management controls. See page 1169 for a tutorial on using PGP.

Both PGP and GPG rely on the notion of a web of trust<sup>3</sup>: If you trust someone and that person trusts someone else, the person you trust can provide an introduction to the third party. When you trust someone, you perform an operation called key signing. By signing someone else's key, you verify that the person's public key is authentic and safe for you to use to send email. When you sign a key, you are asked whether you trust this person to introduce other keys to you. It is common practice to assign this trust based on several criteria, including your knowledge of a person's character or a lasting professional relationship with the person. The best practice is to sign someone's key only after you have met face to face to avert any chance of a man-in-the-middle scenario (see the adjacent tip). The disadvantage of this scheme is the lack of a central registry for associating with people you do not already know.

# ## MTM (man-in-the-middle) attack

+   * security
+   
+   If Max and Zach try to carry on a secure email exchange over a network, Max first sends Zach his public key. However, suppose Mr. X sits between Max and Zach on the network and intercepts Max's public key. Mr. X then sends his public key to Zach. Zach then sends his public key to Max, but once again Mr. X intercepts it and substitutes his public key and sends that to Max. Without some kind of active protection (a piece of shared information), Mr. X, *the man in the middle*, can decrypt all traffic between Max and Zach, reencrypt it, and send it on to the other party. This type of deception is called a MTM attack.

> 3, For more information see www.gnupg.org/gph/en/manual/x334.html.