machine (called the authentication server) to run the Kerberos daemon. This dae-
missions tickets to users or services that present credentials, such as passwords,
when they request authentication.

In essence, Kerberos improves upon traditional password security in only two
ways: it never transmits unencrypted passwords on the network, and it relieves
users from having to type passwords repeatedly, making password protection of
network services somewhat more palatable.

The Kerberos community boasts one of the most lucid and enjoyable documents
ever written about a cryptosystem, Bill Bryant’s "Designing an Authentication
System: a Dialogue in Four Scenes."It’s required reading for anyone interested in
cryptography and is available at

web.mit.edu/kerberos/www/dialogue.html

Kerberos offers a better network security model than the "ignoring network sec-
ity entirely" model, but it is neither perfectly secure nor easy to install and
. It does not supersede the other security measures described in this chapter.

Unfortunately (and perhaps predictably), the Kerberos system distributed as part
of Windows Directory uses proprietary, undocumented extensions to the
protocols. As a result, it does not operate well with distributions based on the
MIT code. Fortunately, the winbind module lets UNIX and Linux systems inter-
act with Active Directory’s version of Kerberos. See Configuring Kerberos for Ac-	ive Directory integration on page 1156 for more information.

# PGP: Pretty Good Privacy

See page 763 for
more information
about email privacy.

Phil Zimmermann’s PGP package provides a tool chest of bread-and-butter cryp-
tographic utilities focused primarily on email. It can be used to encrypt
data, to generate signatures, and to verify the origin of files and messages.

PGP has an interesting history that includes lawsuits, criminal prosecutions, and
the privatization of portions of the original PGP suite. Kerberos’s file-
 and protocols are being standardized by the IETF under the name Open-
PP, and multiple implementations of the proposed standard exist. The GNU
project provides an excellent, and widely used implementation known as
GnuPG at gnpgup.org. For clarity, we refer to the system collectively as PGP even
ough individual implementations have their own names.

PGP is perhaps the most popular cryptographic software in use. Unfor-
tunately, the UNIX/Linux version is nuts-and-bolts enough that you have to un-
der a fair amount of cryptographic background in order to use it. Although
y may find PGP useful in your own work, we don’t recommend that you sup-
port it for users because it has been known to spark many puzzled questions. We
have found the Windows version to be considerably easier to use the gpg
command with its 52 different operating modes.

![](bbox=[0.953, 0.335, 0.995, 0.43])