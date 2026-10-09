
...register, upgrade, or email a mailing list. We have no idea how many FreeBSD users are in the world.
Since FreeBSD is by far the most popular open source BSD, that's not an inconsiderable number of machines. And since one FreeBSD server can handle hundreds of thousands of internet domains, a disproportionate number of sites use FreeBSD as their supporting operating system. This means that there are hundreds of thousands, if not millions, of FreeBSD system administrators out in the world today.

## Other BSDs

FreeBSD might be the most popular BSD, but it's not the only one. BSD 4.4-Lite2 spawned several different projects, each with its own focus and purpose. Those projects in turn had their own offspring, several of which thrive today.

### NetBSD

NetBSD is similar to FreeBSD in many ways, and NetBSD and FreeBSD share developers and code. NetBSD's main goal is to provide a secure and reliable operating system that can be ported to any hardware platform with minimal effort. As such, NetBSD runs on VxWorks, PocketPC devices, and high-end SPARC and Alpha servers. I ran NetBSD on my HP Jornada handheld computer.$^{2}$

### OpenBSD

OpenBSD branched off from NetBSD in 1996 with the goal of becoming the most secure BSD. OpenBSD was the first to support hardware-accelerated cryptography, and its developers are rightfully proud of the fact that their default installation was largely immune to remote exploits for several years. The OpenBSD team has contributed several valuable pieces of software to the world, including the LibreSSL TLS library and the OpenSSH suite used by almost everyone from Linux to Microsoft.

### DragnFly BSD

DragnFly BSD forked from FreeBSD 4 in 2003. It developed in a different direction than FreeBSD, with a new kernel messaging system. DragnFly BSD has very high performance and its HAMMER filesystem supports snapshots and fine-grained history. Check out [http://www.dragonflybsd.org/](http://www.dragonflybsd.org/) for more information.

### macOS

Apple's macOS? That's right. Apple incorporates large chunks of FreeBSD into its macOS on an ongoing basis. If you're looking for a stable operating system with a friendly face and a powerful core, macOS is unquestionably for you. While FreeBSD makes an excellent desktop for a computer professional, I wouldn't put it in front of a random user. I would put macOS in front of that same random user without a second thought, however, and I'd even feel that I was doing the right thing. But macOS includes many things that aren't at all necessary for an internet server, and it runs only on Apple hardware, so I don't recommend it as an inexpensive general-purpose server.

### FreeBSD's Children

Several projects have taken FreeBSD and built other projects or products on top of it. The award-winning FreeNAS transforms a commodity system into a network fileserver. The pfSense project transforms your system into a firewall with a nice web management interface. TrueOS gives FreeBSD a friendly face while supporting resource-intensive advanced features, like ZFS, while GhostBSD puts a friendly face on equipment with less computing oomph. Other projects like this appear from time to time; while not all are successful, I'm sure by the time this book comes out, we'll have one or two more solid members of this group.

## Other Unixes

Several other operating systems derive from or emulate primordial Unix in one way or another. This list is by no means exhaustive, but I’ll touch on the high points.

### Solaris

The best-known Unix might be Oracle Solaris. Solaris runs on high-end hardware that supports dozens of processors and gobs of disk. (Yes, gobs is a technical term, meaning *more than you could possibly ever need, and I know very well that you need more disk than I think you need.*) Solaris, especially early versions of Solaris, had strong BSD roots. Many enterprise-level applications run on Solaris. Solaris runs mainly on the SPARC hardware platform manufactured by Sun, which allows Sun to support interesting features, such as hot-swappable memory and mainboards.

The Oracle Corporation acquired Solaris when they bought Sun Microsystems in 2009. Oracle ceased Solaris development in 2016. While there’s still an extensive installed base of Solaris systems and you can still get Solaris from Oracle, as of today, Oracle Solaris has no future.

### illumos

Several years before Oracle purchased Sun Microsystems, Sun open sourced the majority of Solaris and sponsored the OpenSolaris project to improve that codebase. OpenSolaris ran successfully until Oracle shut down source access and reclaimed all of the OpenSolaris resources.

The OpenSolaris code was still available, though. The OpenSolaris community forked OpenSolaris into illumos ([http://illumos.org/](http://illumos.org/)). If you miss Solaris, you can still use a free, modern, Solaris-like operating system. FreeBSD includes two important features from OpenSolaris, the Zetabyte Filesystem (ZFS) and DTrace, a full-system tracing system.

### AIX

Another Unix contender is IBM's entry, AIX. AIX's main claim to fame is its journaling filesystem, which records all disk transactions as they happen and allows for fast recovery from a crash. It was also IBM's standard Unix for many years, and anything backed by Big Blue shows up all over the place. AIX started life based on BSD, but AT&T has twiddled just about everything so that you won't find much BSD today.

## Linux

Linux is a close cousin of Unix, written from the ground up. Linux is similar to FreeBSD in many ways, though FreeBSD has a much longer heritage and is friendlier to commercial use than Linux. Linux includes a requirement that any user who distributes Linux must make his or her changes available to the end user, while BSD has no such restriction. Of course, a Linux fan would say, “FreeBSD is more vulnerable to commercial exploitation than Linux.” Linux developers believe in share-and-share-like, while BSD developers offer a no-strings-attached gift to everyone. It all depends on what's important to you.

Many new Unix users have a perception of conflict between the BSD and Linux camps. If you dig a little deeper, however, you'll find that most of the developers of these operating systems communicate and cooperate in a friendly and open manner. It's just a hard fringe of users and developers that generate friction, much like different soccer teams' hooligans or different Star Trek series' fans.

## Other Unices

Many Unices have come and gone, while others stagger on. Past contenders include Silicon Graphics' IRIX, Hewlett-Packard's HP/UX, Tru64 Unix, and the suicidal SCO Group's UnixWare. Dig further and you'll find older castoffs, including Apple's A/UX and Microsoft's Xenix. (Yes, Microsoft was a licensed Unix vendor, back in that age when dinosaurs watched the skies nervously and my dad hunted mammoth for all the tribal rituals.) Many high-end applications are designed to run best on one particular flavor of Unix. All modern Unices have learned lessons from these older operating systems, and today's Unixes and Unix-like operating systems are remarkably similar.

## **WHY UNIX-LIKE?**

One thing to note is that FreeBSD, Linux, and so on are called *Unix-like* instead of *Unix*. The term *Unix* is a trademark of The Open Group. For an operating system to receive the right to call itself Unix, the vendor must prove that the OS complies with the current version of the Single Unix Specification. While FreeBSD generally meets the standard, continuous testing and recertification cost money, which the FreeBSD Project doesn't have to spare. Certification as Unix also requires that someone sign a paper stating not only that he or she is responsible for FreeBSD's conformance to the Single Unix Specification but that he or she will fix any deviations from the standard that are found in the future. FreeBSD's development model makes this even more difficult—bugs are found and deviations are fixed, but there's nobody who can sign a piece of paper that guarantees 100 percent standards compliance.

### FreeBSD's Strengths

After all this, what makes FreeBSD unique?

#### Portability

The FreeBSD Project's goal is to provide a freely redistributable, stable, and secure operating system that runs on the computer hardware that
