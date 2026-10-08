
### C.5.20 Downloading SSL

SSL is short for Secure Socket Layer. It is the encryption and authentication code and protocol that puts the “s” in https, pop3s, and imaps. This prevents sniffing and spoofing very effectively. Even high-security applications such as Internet banking and commerce rely on it. I am not aware of it having been broken.

> It is important to note that SSL solves only the problems of network sniffing and authentication, and only if used correctly. Some sites fail to use it for all the confidential information sent over the Internet. Even though Netscape Communications invented SSL, some versions of their browser have used it incorrectly, making users vulnerable to dishonest Web sites. This is discussed in “Upgrade Netscape” on page 107.

Do not get a false sense of security that either your browser’s site or your Web site is secure because SSL is used—it is but one component of security. Consider, too, that because SSL provides encrypted communication through your firewall, the firewall cannot detect content-based attacks done over SSL. These include long names causing buffer overflow attacks, non-ASCII data, and many other attacks that Web servers and clients are vulnerable to.

An open-source version of SSL, including the sslproxy program (used for wrapping around the imap and pop3 servers), stunnel, edssl, and the SSL library may be downloaded from

www.openssl.org/

It includes the ssl library needed by fetchmail-ssl and similar programs.

### C.5.21 Downloading sslwrap

The sslwrap program allows wrapping any TCP service in SSL easily. It is especially recommended for imap and pop3. (Note that it is not recommended for https. Apache’s http-ssl is a better solution.) See also “POP and IMAP Servers” on page 152.

www.rickk.com/sslwrap/

### C.5.22 SSH-Wrapped CVS Web Site

CVS is a very useful tool for shared software development over the Internet and has been a part of Linux development since the beginning. Unfortunately, by itself it is not secure. With a small amount of effort, it can be wrapped in SSH, as CVS is just another TCP service to SSH. The Web site

http://cuba.xs4all.nl/~tim/scvs

documents how to do this.

### C.5.23 Downloading Encrypted Disk Driver

The encrypted device driver **PPDD** (Practical Privacy Disk Driver) that may be stacked above a disk driver may be downloaded from

http://linux01.gwdg.de/~alatham/ppdd.html

### C.5.24 Sendmail Without Root

This page explains how to set up sendmail to run without ever being root and to be invoked from inetd to allow the use of TCP Wrappers and to be immune to reverse DNS spoofing.

www.coker.com.au/~russell/sendmail.html

### C.5.25 Downloading postfix

The postfix program is an alternative to sendmail that some security experts consider to be substantially more secure due to its use of “Rings of Security.” Its advantages are discussed in “Sendmail” on page 122.

www.postfix.org/

### C.5.26 Libsafe

This innovative library works around some common C programming bugs that cause buffer overflows. These bugs are one of the most common entry points for Linux compromises and cannot be overcome completely by good system administration practices alone. The library works by intercepting calls to the most common string processing library routines that are called by this buggy code and mitigates the problem.

### C.5.27 Attacks That Have Been Seen

This Web site posts the various attacks that have been launched to various ports; in other words, what Trojans have been seen on these ports. By understanding these, you can get valuable clues to what compromises might have happened to some of your systems.

www.robertgraham.com/pubs/firewall-seen.html

### C.5.28 Analyzing Your Attacker with Sam Spade

This interesting site offers many tools for analyzing another site. It can tell what domain an IP address belongs to, safely analyzes Web pages (though tcpread will do this too), allows looking at sites without giving away your IP address, and can check whether your mail server allows relaying. Unfortunately, this site can be used for evil too but the crackers will discover it anyway. I consider its value to white hats sufficient to list it.

www.samspade.org/

## C.6 URLs for Documentation

These contain useful, well-written documentation. Some of it is translated into languages other than English.

### C.6.1 Linux Documentation

The latest Linux documentation may be obtained from the Linux Documentation Project.

www.linuxdoc.org/

The following will be especially useful. They are the “online” versions. Many also are available as PostScript or PDF from the same site.

- www.linuxdoc.org/HOWTO/Firewall-HOWTO.html
- www.linuxdoc.org/HOWTO/IPCHAINS-HOWTO.html
- www.linuxdoc.org/HOWTO/IP-Masquerade-HOWTO.html
- www.linuxdoc.org/HOWTO/ISP-Hookup-HOWTO.html
- www.linuxdoc.org/HOWTO/Kernel-HOWTO.html
- www.linuxdoc.org/HOWTO/Loopback-Encrypted-Filesystem-HOWTO.html
- www.linuxdoc.org/HOWTO/Mail-Administrator-HOWTO.html
- www.linuxdoc.org/HOWTO/Mutt-GnuPG-PGP-HOWTO.html
- www.linuxdoc.org/HOWTO/Online-Troubleshooting-HOWTO.html
- www.linuxdoc.org/HOWTO/Oracle-8-HOWTO.html
- www.linuxdoc.org/HOWTO/Secure-Programs-HOWTO.html
- www.linuxdoc.org/HOWTO/Securing-Domain-HOWTO.html
- www.linuxdoc.org/HOWTO/Security-HOWTO.html
- www.linuxdoc.org/HOWTO/VPN-HOWTO.html
- www.linuxdoc.org/HOWTO/mini/Firewall-Piercing.html
- www.linuxdoc.org/HOWTO/mini/Home-Network-mini-HOWTO.html
- www.linuxdoc.org/HOWTO/mini/Secure-POP+SSH.html
- www.linuxdoc.org/HOWTO/mini/VPN.html
- file:/usr/doc/pam-0.66/html/pam-6.html *(Red Hat and derivatives)*
- http://tldp.org/HOWTO/Net-HOWTO/index.html
- http://tldp.org/HOWTO/ISP-Setup-RedHat-HOWTO.html

### C.6.2 Writing Secure Programs

These are a collection of papers on writing secure programs, including safe set-UID programs. Some of them are old but useful still. As with any URL, some might no longer be available.

- ftp://ftp.auscert.org.au/pub/auscert/papers/secure_programming_checklist
- http://olympus.cs.ucdavis.edu/~bishop/scriv/1996-sans-tut.pdf
- www.sunworld.com/sunworldonline/swol-08-1998/swol-08-security.html
- www.whitefang.com/sup/

This paper discusses reviewing (auditing) code for security:

www.dnaco.net/~kragen/security-holes.html

This paper offers suggestions on writing safe set-UID programs:

http://olympus.cs.ucdavis.edu/~bishop/scriv/Bish86.pdf

## C.7 URLs for General Tools

Some general tools that are useful for security work are listed here.

### C.7.1 The ddd Debugger

The Data Display Debugger (DDD) may be downloaded from

www.gnu.org/software/ddd/

It is this author's favorite GUI program and shows inspired use of graphics. Its graphing of linked lists of data, with all data changes displayed automatically, and its highlighting of running code allow much more rapid debugging than with straight gdb. To avoid the bother of compiling it or finding Motif or LessTif, you simply may download the statically linked binary.

### C.7.2 Time Zone Computer

When access is seen from a system far away, it is useful to be able to determine local time at that location. Knowing this will indicate whether the access is likely to be legitimate and whether there likely will be a SysAdmin there to answer the telephone or e-mail. The “Sunset Computer” at

www.cavu.com/sunset.html

will provide this information, though this is not its primary purpose.

You will need to supply the nearest large city to the location that you are interested in. Most countries have only a single time zone. Exceptions are the largest countries, such as the United States, Canada, Australia, Russia, Mexico, Argentina, Brazil, Greenland, Indonesia, and Zaire.

## C.8 URLs for Specifications and Definitions

Here I list the URLs for the specifications to some protocols and other items that you might want to study to understand or analyze the security implications. The Internet Engineering Task Force (IETF) is a group of engineers that do continuing development on protocols used to keep the Internet running. Proposed new standards or updates to existing standards are released as Request For Comment (RFC) documents that are numbered. A final accepted document (specification) still is called an RFC. Any of them should be available from

www.faqs.org/rfcs/rfc#.html

where # is the RFC number.

### C.8.1 Orange Book

The Orange Book, more technically known as DoD 5200.28-STD, “Department of Defense Trusted Computer System Evaluation Criteria,” specifies the requirements for secure computing for the U.S. government’s high-security needs for classified material. It is used by the military, the CIA, the NSA, their contractors, and others. (The most secure systems still are kept in locked and shielded rooms with no connections to outside networks.)

www.radium.ncsc.mil/tpsp/library/rainbow/5200.28-STD.html

### C.8.2 RFC 1813: NFS Version 3

The original specification for Sun’s NFS is in RFC 1094. The specification for NFS version 3 is RFC 1813. NFS version 3 started showing up in Linux distributions around late 1999 or early 2000 as did TCP support for NFS. NFS over TCP, although slower than over UDP
