
http://www.linux.org/linux/raid.html, which contains a complete listing of all the RAID resources that are currently available for Linux. Software RAID is an incredible tool for enhancing system reliability and performance; I know that it has made a huge positive impact on the performance of my machine!

### Summary

Caldera OpenLinux 2.2 features an innovative graphical installation process called LIZARD, which provides a near-ideal “out of box” experience for the Linux user. In addition, Caldera offers their earlier text-based installer, LISA. Although less advanced, LISA offers more control over the installation process.

Although many users choose to install Caldera in one partition, there are several other partitioning options worth considering. When a partitioning scheme is chosen to complement the intended use of the system, disk performance can often be dramatically enhanced. In addition, Linux Software RAID can be used to increase the integrity and availability of critical data, as well as to further boost disk IO performance.

## Appendix C

## Bibliography

Costales, Bryan, and Eric Allman. *sendmail, Second Edition.* O’Reilly and Associates, Inc., 1997. ISBN 1-56592-222-0. This imposing and intimidating book tells you everything you ever wanted to know about configuring *sendmail*. Impressively cross-indexed and complete, this book reads like a GNU info page on steroids.

Garfinkel, Simson, and Gene Spafford. *Practical UNIX & Internet Security, Second Edition.* O’Reilly and Associates, Inc., 1996. ISBN 1-56592-148-8. This book is the bible of UNIX and network security. If you are even contemplating putting your Linux machine on the Internet, you must read this book.

Harbison, Samuel P., and Guy L. Steele, Jr. *C: A Reference Manual, Fourth Edition.* Prentice Hall, 1995. ISBN 0-13-326224-3. This is a detailed C reference manual covering both ANSI C and common pre-ANSI C dialects.

Harrison, Mark, and Michael McLennan. *Effective Tcl/Tk Programming: Writing Better Programs with Tcl and Tk.* Addison-Wesley Publishing Company, 1998. ISBN 0-201-63474-0. This book assumes a basic knowledge of Tcl/Tk. It describes advanced features and great programming tricks. It comes with a library of freely reusable Tcl routines. The authors have a deep appreciation for Tcl/Tk and their sample programs are clear and elegant.

Lamport, Leslie. *LaTeX: A Document Preparation System, Second Edition.* Addison-Wesley Publishing Company, 1996. ISBN 0-201-52983-1. This book, by the author of LaTeX, describes the typesetting system with clarity and humor. Highly recommended if you want to learn LaTeX.

Ousterhout, John K. *Tcl and the Tk Toolkit.* Addison-Wesley Publishing Company, 1994. ISBN 0-201-63337-X. This book by the author of Tcl and Tk explains how to use the language and toolkit. It is somewhat dated, but still mostly accurate. It is also the clearest Tcl and Tk tutorial I have ever read.

Plauger, P. J. *The Standard C Library.* Prentice Hall, 1992. ISBN 0-13-131509-9. This book gives painstaking description of the C standard library by one of the members of the C standardization committee. This book also contains complete source code for a full implementation of the standard C library.

Rubini, Alessandro. *Linux Device Drivers.* O’Reilly and Associates, Inc., 1998. ISBN 1-56592-292-1. This book describes the Linux kernel internals from the point of view of device drivers. Given the rapid pace of Linux development, such a book quickly becomes outdated. Nevertheless, the book is a great starting point before you plunge into reading the Linux kernel code.

Schneier, Bruce. *Applied Cryptography: Protocols, Algorithms, and Source Code in C, Second Edition*. John Wiley and Sons, Inc., 1996. ISBN 0-471-11709-9. This book is an encyclopedic reference for cryptographic protocols and algorithms. As a bonus, it's fun to read. If you are tempted to invent your own cryptographic algorithm, read this book to find out why it's a bad idea.

Stevens, W. Richard. *Advanced Programming in the UNIX Environment*. Addison-Wesley Publishing Company, 1993. ISBN 0-201-56317-7. A wonderful reference that describes the UNIX API and advanced UNIX programming techniques. This is the preeminent UNIX programming reference text.

*TCP/IP Illustrated, Volume 1: The Protocols*. Addison-Wesley Publishing Company, 1994. ISBN 0-201-63346-9. This book describes the IP, TCP, UDP and ICMP protocols in detail. Stevens illustrates hundreds of test cases using the *tcpdump* tool so that the abstract protocol descriptions are illustrated with concrete and understandable examples.

*UNIX Network Programming, Volume 1, Second Edition: Networking APIs: Sockets and XTI*. Prentice Hall, 1998. ISBN 0-13-490012-X. This book describes the Sockets API (used by Linux) in great detail. If you wish to write client-server software under UNIX, read this book.

## Appendix D

### RPM Listing

All of the examples in this book have assumed a full installation of Caldera OpenLinux. If you have not performed a full installation, some software may be missing. The following table lists all executables in `/bin`, `/sbin`, `/usr/bin` and `/usr/sbin` along with the RPM from which they are derived. Note that the RPM version numbers may change as Caldera OpenLinux is updated. The base name of the RPM should remain the same, however.

Some files do not belong to any packages. For example, `/bin/csh` is listed as not belonging to a package. These files are all symbolic links which are set up during installation. To find the package which creates them, run `rpm -q -f real_file`, where `real_file` is the file to which the symbolic link refers.

#### TABLE D.1 OpenLinux Executables and Their Source RPMs

| Executable | Directory | RPM |
| :--- | :--- | :--- |
| activate | /sbin | lilo-0.21-6 |
| addtosmbpass | /usr/sbin | samba-2.0.5-1 |
| adduser | /usr/sbin | adduser-1.2-1 |
| amd | /etc/rc.d/init.d | am-utils-6.0-4 |
| amd | /usr/sbin | am-utils-6.0-4 |
| arch | /bin | util-linux-2.99-4 |
| arp | /sbin | net-tools-1.52-4 |
| atd | /etc/rc.d/init.d | at-3.1.7-1 |
| atd | /usr/sbin | at-3.1.7-1 |
| avmcapctrl | /sbin | isdn4k-utils-3.0beta2-4 |
| badblocks | /sbin | ext2fs-1.14-2 |
| bash | /bin | bash-1.14.7-9 |
| bash2 | /bin | bash2-2.03-1 |
| bigfs | /etc/rc.d/init.d | SysVinit-scripts-1.05-5 |
| booteer | /sbin | SysVinit-scripts-1.05-5 |
| booteerd | /sbin | SysVinit-scripts-1.05-5 |
| box | /bin | lisa-4.0-7 |
| bru | /bin | BRU-15.0P.11 |
| build_menu | /bin | lisa-4.0-7 |
| bunzip2 | /bin | bzip2-0.9.0b-1 |
| bzcat | /bin | bzip2-0.9.0b-1 |
| bzip2 | /bin | bzip2-0.9.0b-1 |
| bzip2recover | /bin | bzip2-0.9.0b-1 |
| cat | /bin | textutils-1.22-3 |
| cfdisk | /sbin | util-linux-2.9s-4 |
| chat | /usr/sbin | ppp-2.3.8-1 |
| checkpc | /usr/sbin | LPRng-lpd-3.5.3-1 |
| chgrp | /bin | fileutils-4.0-1 |
| chmod | /bin | fileutils-4.0-1 |
| chown | /bin | fileutils-4.0-1 |
| chpasswd | /usr/sbin | shadow-misc-1.1-3 |
| chroot | /usr/sbin | sh-utils-1.16-7 |
| clcandir | /usr/sbin | cleandir-1.0-1 |
| convert_smbpasswd | /usr/sbin | samba-2.0.5-1 |
| convertsmbpasswd | /usr/sbin | samba-2.0.5-1 |
| cp | /bin | fileutils-4.0-1 |
| cpio | /bin | cpio-2.4.2-3 |
| cron | /etc/rc.d/init.d | vixie-cron-3.0.1-18 |
| cron | /usr/sbin | vixie-cron-3.0.1-18 |
| cronloop | /usr/sbin | crontabs-1.12-1 |
| ctags | /bin | vim-5.3-4 |
| ctrlaltdel | /sbin | util-linux-2.9s-4 |
| date | /bin | sh-utils-1.16-7 |
| db_print | /bin | lisa-4.0-7 |
| dd | /bin | fileutils-4.0-1 |
| debugfs | /sbin | ext2fs-1.14-2 |
| depmod | /sbin | modutils-2.1.121-9b |
| df | /bin | fileutils-4.0-1 |
| dhcpcd | /sbin | dhcpd-1.3.17p4-0 |
| dhcpd | /etc/rc.d/init.d | dhcpd-1.0pl2-3 |
| dhcpd | /usr/sbin | dhcpd-1.0pl2-3 |
| diald | /usr/sbin | diald-0.16-1 |
| dip | /usr/sbin | dip-3.3.7a-9 |
| diplogin | /usr/sbin | dip-3.3.7a-9 |

![continues](img/df365d352a104b50fea29e59a052de4d_1044_0.png)
