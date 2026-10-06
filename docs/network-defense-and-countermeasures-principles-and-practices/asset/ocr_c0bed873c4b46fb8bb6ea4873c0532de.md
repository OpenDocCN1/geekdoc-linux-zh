1976. An interesting factoid is that the method had actually been developed a few years earlier by Malcolm J. Williamson of the British Intelligence Service, but it was classified.

# ElGamal

ElGamal is based on the Diffie-Hellman key algorithm just described. It was first described by Taher ElGamal in 1984. It is used in some versions of Pretty Good Privacy (PGP).

# MQV

Like ElGamal, MQV (Menezes-Qu-Vanstone) is a protocol for key agreement that is based on Diffie-Hellman. It was first proposed by Menezes, Qu, and in 1995 and modified in 1998, MQV is incorporated in the public standard IEEE P1356.

# Digital Signature Algorithm

Digital Signature Algorithm (DSA) is described in U.S. Patent 5,231,668, filed July 26, 1991, and attributed to David W. Kravitz. It was adopted by the U.S. government in 1993 with FIPS 186. Although any asymmetric algorithm can be used for digital signatures, this algorithm was designed for purpose.

# Elliptic Curve

The Elliptic Curve algorithm was first described in 1985 by Victor Miller (IBM) and Neil Koblitz (University of Washington).

The security of the Elliptic Curve cryptography is based on the fact that the discrete logarithm of a random elliptic curve element with respect to a publicly known base point is difficult to the point of being impractical to do.

The size of the elliptic curve determines the difficulty of the finding, the algorithm, and then the security of the implementation. The level of security afforded by an RSA-based system with a large modulus can be achieved with a much smaller elliptic curve. There are actually several ECC algorithms. There is an ECC version of Diffie-Hellman, an ECC version of DSA, and many others.

The U.S. National Security Agency endorsed ECC (Elliptic Curve Cryptography) by including schemes based on it in its Suite B of recommended algorithms and allows them for protecting information classified up to top secret with 384-bit keys.

# Digital Signatures

A digital signature is using asymmetric cryptography, in reverse order. Consider a situation wherein the concern is not data confidentiality, but rather verifying who sent the message. Perhaps you get e-mail from your boss tells you that you should take next off with pay. It would be a good idea for you to verify this message indeed came from your boss, and is not a spoofed message from a colleague playing a prank. Digital signatures accomplish this.