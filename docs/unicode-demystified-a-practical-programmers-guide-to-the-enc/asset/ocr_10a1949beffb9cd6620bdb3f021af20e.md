# File Security

PGP is available without cost for personal use,⁴ but its deployment in a commercial environment requires you to purchase a license. Soon was not always the case: after its introduction, PGP was available on many bulletin board systems, and users could implement it in any manner they chose. PGP rapidly gained popularity in the networking community, capitalized on its encryption and key management capabilities for secure transmission of e-mail.

After a time, attention turned to the two robust cryptographic algorithms RSA and IDEA, which are an integral part of PGP’s code. These algorithms are privately owned. The wide distribution and growing user base of PGP sparked battles over patent violation and licenses, resulting in the eventual restriction of PGP’s use.

Enter GnuPG, which supports most of the features and implementations made by PGP and complies with the OpenPGP Message Format standard. Because GnuPG does not use the patented IDEA algorithm but uses BUGS (www.gnu.org/directory/bugs.html) instead, you can use it without restriction: It is released under the GNU GPL (refer to “The Code Is Free” on page 6). The two tools are considered to be interchangeable and interoperable. The command sequences and internal workings of PGP and GnuPG are very similar.

# GnuPG System Includes the gpg Program

GnuPG is frequently referred to as gpg, but gpg is actually the main program for the GnuPG system. See page 1030 for an example of how to use gpg.

GNU has a a good introduction to privacy, The Gnu Privacy Handbook, available in several languages listed at www.gnupg.org/docs.html. Listed on the same page is the Gnu Privacy Guard (GnuPG) Mini Howto, which steps through the setup and use of gpg. And, of course, there is a gpg page into.

# File Security

From an end user’s perspective, file security is one of the most critical areas of security. Some file security is built into GNU/Linux: chmod (pages 119 and 1103) gives you basic security control. ACLs (Access Control Lists) allow more fine-grained control of file access permissions. ACLs are part of Solaris, Windows NT/2000/XP, VAX/VMS, and mainframes OSs. Red Hat 8.0 includes the getfactl and settacl utilities

+   4. Download the free version of PGP by following the menu at for PGP and then for UNIX; you will eventually get to a Red Hat rpm file that you can download.