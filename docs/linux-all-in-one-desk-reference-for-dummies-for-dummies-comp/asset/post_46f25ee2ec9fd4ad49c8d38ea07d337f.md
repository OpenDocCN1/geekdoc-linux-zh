
# 18 What a Linux Distribution Includes

Table 1-2 (continued)

| Software Package | Description |
| :--- | :--- |
| Coreutils | A package that combines three individual packages called Fileutils, Shellutils, and Textutils and implements utilities such as chgrp, chmod, chown, cp, dd, df, dir, dircolors, du, install, ln, ls, mkdir, mkfifo, mknod, mv, rm, rmdir, sync, touch, vdir, basename, chroot, date, dirname, echo, env, expr, factor, false, groups, hostname, id, logname, nice, nohup, pathchk, printenv, printf, pwd, seq, sleep, stty, su, tee, test, true, tty, uname, uptime, users, who, whoami, yes, cut, join, nl, split, tail, wc, and so on |
| GNUchess | A chess game |
| GNU C Library | For use with all Linux programs |
| cpio | Copies file archives to and from disk or to another part of the file system |
| diff | Compares files, showing line-by-line changes in several different formats |
| ed | A line-oriented text editor |
| emacs | An extensible, customizable, full-screen text editor and computing environment |
| Findutils | A package that includes the find, locate, and xargs utilities |
| finger | A utility program designed to enable users on the Internet to get information about one another |
| gawk | The GNU Project's implementation of the awk programming language |
| gcc | Compilers for C, C++, Objective C, and other languages |
| gdb | Source-level debugger for C, C++, and Fortran |
| gdbm | A replacement for the traditional cfm and ndbm database libraries |
| gettext | A set of utilities that enables software maintainers to internationalize (that means make the software work with different languages such as English, French, Spanish, and so on) a software package's user messages |
| ghostscript | An interpreter for the PostScript and Portable Document Format (PDF) languages |
| ghostview | An X Window System application that makes ghostscript accessible from the GUI, enabling users to view PostScript or PDF files in a window |
| The GIMP | (The GNU Image Manipulation Program): An Adobe Photoshop-like image processing program |
| GNOME | Provides a graphical user interface (GUI) for a wide variety of tasks that a Linux user may perform |
| gnumeric | A graphical spreadsheet (similar to Microsoft Excel) that works in GNOME |
| grep package | Includes the grep, egrep, and fgrep commands that are used to find lines that match a specified text pattern |
| groff | A document-formatting system similar to troff |
| gtk+ | A GUI toolkit for the X Window System (used to develop GNOME applications) |
| gzip | A GNU utility for compressing and decompressing files |
| indent | Formats C source code by indenting it in one of several different styles |
| less | A page-by-page display program similar to more, but with additional capabilities |
| libpng | A library for image files in the Portable Network Graphics (PNG) format |
| m4 | An implementation of the traditional UNIX macro processor |
| make | A utility that determines which files of a large software package need to be recompiled, and issues the commands to recompile them |
| mtools | A set of programs that enables users to read, write, and manipulate files on a DOS file system (typically a floppy disk) |
| ncurses | A package for displaying and updating text on text-only terminals |
| patch | A GNU version of Larry Wall's program to take the output of diff and apply those differences to an original file to generate the modified version |
| rcs | (Revision Control System): Used for version control and management of source files in software projects |
| sed | A stream-oriented version of the ed text editor |
| Sharutils | A package that includes shar (used to make shell archives out of many files) and unshar (to unpack these shell archives) |
| tar | A tape archiving program that includes multivolume support; the capability to archive sparse files (files with big chunks of data that are all zeros), handle compression and decompression, and create remote archives; and other special features for incremental and full backups |
| texinfo | A set of utilities that generates printed manuals, plain ASCII text, and online hypertext documentation (called info), and enables users to view and read online info documents |
| time | A utility that reports the user, system, and actual time that a process uses |

## GUIs and applications

Face it—typing cryptic Linux commands on a terminal is boring. For average users, using the system through a graphical user interface (GUI, pronounced GOO-ee)—one that gives you pictures to click and windows (small w) to open — is much easier. This is where the X Window System, or X, comes to the rescue.

X is kind of like Microsoft Windows, but the underlying details of how X works are completely different from Windows. X provides the basic features of displaying windows on-screen, but (unlike Microsoft Windows) it does not come with any specific look or feel for graphical applications. That look and feel comes from GUIs, such as GNOME and KDE, which make use of the X Window System.

Most Linux distributions come with the X Window System in the form of XFree86 or X.Org X11 — implementations of the X Window System for 80x86 systems. XFree86 and X.Org X11 work with a wide variety of video cards available for today’s PCs.

![](img/11709a8f88c8cd03868a929dc94c0e2b_45_0.png)

Until early 2004, XFree86 from the XFree86 Project (<http://www.xfree86.org>) was the most commonly used X Window System implementation for x86 systems. However, around version 4.4, some changes to the XFree86 licensing terms caused concerns to many Linux and UNIX vendors — they felt that the licensing terms were no longer compatible with the GNU General Public License (GPL). In January 2004, several vendors formed the X.Org Foundation (<http://www.x.org>) to promote continued development of the open source X Window System and graphical desktop. The first release of X.Org X11 uses the same code that was used by XFree86 4.4, up until the time when the XFree86 license changes precipitated the creation of X.Org Foundation.

As for the GUI, Linux distributions include one or both of two powerful GUI desktops: KDE (K Desktop Environment) and GNOME (GNU Object Model Environment). If both GNOME and KDE are installed on a PC, you can choose which desktop you want as the default — or switch between the two. KDE and GNOME provide desktops similar to those of Microsoft Windows and the Mac OS. GNOME also comes with the Nautilus graphical shell that makes finding files, running applications, and configuring your Linux system easy. With GNOME or KDE, you can begin using your Linux workstation without having to know cryptic Linux commands. However, if you ever need to use those commands directly, all you have to do is open a terminal window and type them at the prompt.

Linux also comes with many graphical applications. The most noteworthy program is The GIMP (GNU Image Manipulation Program), a program for working with photos and other images. The GIMP’s capabilities are on a par with Adobe Photoshop.

Providing common productivity software — such as word processing, spreadsheet, and database applications — is an area in which Linux used to be lacking. This situation has changed, though. Linux comes with the OpenOffice.org office productivity applications. In addition, you may want to check out these prominent, commercially available, office productivity applications for Linux that are not included on this book’s companion DVD-ROM:

- **Applixware**: This office package is a good example of productivity software for Linux. You can find it at `www.vistasource.com`.
- **StarOffice**: From Sun Microsystems (`www.sun.com/staroffice`), StarOffice is another well-known productivity software package.
- **CrossOver Office**: From CodeWeavers (`www.codeweavers.com/products/cxoffice`), you can use CrossOver Office to install your Microsoft Office applications (Office 97, Office 2000, and Office XP) as well as several other Windows applications in Linux.

As you can see, there’s no shortage of Linux office applications that are compatible with Microsoft Office.

## Networks

Linux comes with everything you need to use the system in networks so that the system can exchange data with other systems. On networks, computers that exchange data have to follow well-defined rules, or **protocols**. A *network protocol* is a method that the sender and receiver agree upon for exchanging data across a network. Such a protocol is similar to the rules you might follow when you’re having a polite conversation with someone at a party. You typically start by saying hello, exchanging names, and then taking turns talking. That’s about the same way network protocols work. The two computers use the same protocol to send bits and bytes back and forth across the network.

One of the most well-known and popular network protocols is Transmission Control Protocol/Internet Protocol (*TCP/IP*). TCP/IP is the protocol of choice on the Internet — the “network of networks” that now spans the globe. Linux supports the TCP/IP protocol and any network applications that make use of TCP/IP.

## Internet servers

Some popular network applications are specifically designed to deliver information from one system to another. When you send electronic mail (e-mail) or visit Web sites using a Web browser, you use these network applications (also called *Internet services*). Here are some common Internet services:

- **Electronic mail** (e-mail) that you use to send messages to any other person on the Internet using addresses like `joe@someplace.com`
- **World Wide Web** (or simply, Web) that you browse using a Web browser
- **News services**, where you can read newsgroups and post news items to newsgroups with names such as `comp.os.linux.networking` or `comp.os.linux.setup`
