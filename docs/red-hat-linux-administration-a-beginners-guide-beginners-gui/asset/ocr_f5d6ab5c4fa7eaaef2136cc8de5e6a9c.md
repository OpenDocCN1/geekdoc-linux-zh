# Cryptography References

SSH supports a variety of encription algorithms. Public key encryption happens to be the most interesting and widely used method of performing encryption from site to site and is arguably the most secure. If you want to learn more about cryptography, here are some good books to look into:

+   - *PGP*, by Simon Garfinkel (O’Reilly and Associates, 1994)
+   - *Applied Cryptography: Protocols, Algorithms, and Source Code in C, Second Edition*, by Bruce Schneier (John Wiley & Sons, 1995)
+   - *SSH, The Secure Shell: The Definitive Guide*, by Daniel J. Barrett and Richard Silverman (O’Reilly and Associates, 2001)
+   - *Cryptography and Network Security: Principles and Practice, Second Edition*, by William Stallings (Prentice Hall, 1998)

The PGP book is specific to the PGP program, but it also contains a hefty amount of history and an excellent collection of general cryptography tutorials. The Applied Cryptography book might be a bit overwhelming to many, especially nonprogrammers, but it very successfully explains how actual cryptographic algorithms work. (This text is considered a bible among cypherheads.) Cryptography and network security are heavier on principles than on practice, but they’re useful if you’re interested in the theoretical aspects of cryptography rather than the code itself. The Secure Shell (SSH) is an in depth look at the SSH client and server for UNIX, Windows, and Macintosh—including installation, configuration, and troubleshooting, as well as the use of SSH for tunneling as a way to secure other applications.

# 15.2 Exploring SSH Versions and Distributions

Until the middle of 2000, the U.S. government made it ilegal to develop cryptographic software in the U.S. and export it to other countries. Since the laws have been relaxed, much more software has become available for export outside the U.S.

In addition to this change, there has been a lot of development of the OpenSSH package. This is a completely free implementation of the Secure Shell standard in terms of both the source code and its use. The first version of SSH was available under a fairly open license, but as time went by, it gradually became more and more restrictive. At that time, the SSH that was made available by DataFellows restricted free use of SSH to noncommercial activities. Commercial activities required that licenses be purchased. In early 1999, however, one of the old versions with its less-restrictive license resurfaced. Some of the folks from the OpenBSD project jumped on the chance to fork a totally free version of Secure Shell, and the OpenSSH