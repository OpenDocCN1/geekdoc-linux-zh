
[content]

# 146 Part II The SUSE System

- * Linux System Administrators’ Guide by Lars Wirzenius, Joanna Oja, Stephen Stafford, and Alex Weeks — A detailed document that provides a good deal of information about performing standard system administrative tasks on a Linux system, without focusing on the administrative tools provided by any single distribution.

- * Windows+BSD+Linux Installation Guide by Subhashis Ghosh — If you're interested in multibooting, this document gets into detail how to set up a system that can boot into Windows, Free/OpenBSD, and Linux. Can't make your mind which operating system to use, or want to do different tasks using different operating systems? This document is for you!

The documents in the following list are general documents about using administering Linux, primarily as a desktop environment. In addition, the LDP site hosts some documents targeted toward specific segments of the Linux community other desktop users. Some good examples of these are the following:

- * Custom Linux: A Porting Guide — Porting LinuxPPC to a Custom SBC by Sher Elie — If you're interested in using Linux in an embedded environment, this document provides a good deal of general information about porting Linux to new hardware.

- * EVMS Guide by Christine Lorenz, Joy Goodreau, and Kyle Smith — A great document on the Enterprise Volume Management System, the latest generation of Logical Volume Management (LVM) for Linux. This document is extremely useful for system administrators who are responsible for enterprise systems.

- * Guide to Managing Media and Public Relations in the Linux Community by Sheldon Rose, The Linux Professional Institute — This is an interesting meta-document about Linux that discusses how to create and maintain public relations and media coverage for Linux.

- * Linux Scratch by Gerard Beekmans — Provides good insights and suggestions for customizing and personalizing an existing Linux distribution and using an Linux distribution as the foundation for creating your own distribution.

- * LDP Author Guide by Mark F Komarinski, Jorge Goday, David C. Merrill, and Emma Jane Hogan — A great document on how to write, submit, and maintain LDP documentation.

- * Kernel Module Programming Guide by Peter Jay Salzman and Ori Pomerantz — A great document that provides a variety of information about developing kernel modules for the 2.4 and the 2.6 Linux. Targeted toward driver writers and answering kernel handlers.

- * Pocket Linux Guide by David Horton — A hands-on guide that provides a good deal of fundamental information about organization of a Linux system and how to build a Linux distribution from scratch. This document uses a project Pocket Linux as the foundation for its examples; when you finish the document, you've actually built a small distribution!

# The SUSE Books Package

This package includes works such as the following, which are mostly current or "classic" (in some cases quite old, but still valuable) books from the Linux Documentation Project:

- Linux Installation and Getting Started by Matt Welsh
- Kernel 2.4 Internals by Tigran Aivazian
- Kernel Module Programming Guide by Ori Pomerantz
- Linux Network Administrator’s Guide, Second Edition by Olaf Krich and Terry Dawson
- Linux Programmers’ Guide by Sven Goldt and Sven van der Meer
- Linux Universe Guide by Lars Wirzenius, Joanna Oae, Stefan Stafford, and Alex Weeks
- Linux Users’ Guide by Larry Greenfield

The package (whose full name is books-2004.4.16-3.noarch.rpm at the time this book was written) is available on the DVD if you purchased a boxed copy of the SUSE distribution can also be downloaded from any SUSE FTP site, such as those you you can access through the SUSE portal discussed later in this chapter. After retrieving this package, you can install it using a command similar to the following:

```
rpm -Uvv books-2004.4.16-3.noarch.rpm
```

The rpm switches used in this example simply update any previously installed version of this package (U) and provide very verbose (vv) feedback that includes a histogram of hash marks (h) as each file in the package is installed.

Once installed, these documents (and more) are available as PostScript or PDF files under /usr/share/doc/Books/

# Finding Help Online

The Internet gives you access to a host of additional sources for information about, including Linux and SUSE Linux. This section surveys some of the best sources of information about SUSE Linux that you can find and highlights some of the ways that you can find detailed answers to questions that may not be covered in the official SUSE documentation.

# SUSE Portal

Most companies today, SUSE provides a central site for people searching for customer support, answers to questions about SUSE Linux, software updates and patches, and so on. Located at http://portal.suse.com, the SUSE Portal site (see Figure 5-6) requires that you first create an account in order to access the site, but provides centralized access to many SUSE-related sources of information.

From the SUSE Portal site, you can do any or all of the following:

- Search the SUSE knowledge base of common questions, hot tips, and information gleaned from previous customer support questions

- Submit your own customer support questions, provided that you have registered a SUSE product and are still within the free support window provided by that product, or if you have paid for customer support

- Browse a list of supported hardware, which is software that is known to work with SUSE Linux

- Access the SUSE FTP servers and their mirrors to retrieve product updates and upgrades

- Find shortcuts to SUSE web servers and general-purpose SUSE sites

![](img/e4e45c9f32e76fb35)
Figure 5-6: displaying the SUSE Portal

# Chapter 5

The SUSE Portal is a great place to start when you need to resolve a problem. In addition to the suse-e-mailing list mentioned previously, if you are dealing with the OpenExchange Server (SLOX) or Netline's open source OPEN-CHANGE, you have two useful web sites you can check out:

- * oxhelp.org/ is an unofficial user-supported site where users can post questions and answers. To post questions you need to create a login.

- * http://mirror.open-exchange.org/ox/EN/community/ is an official site provided by the Netline developers. There is a rapidly growing quantity of documentation there, particularly installation instructions for different platforms.

# Topic-Specific Sites

Certain topics, both in the area of hardware support and particular software projects, have a major web site with definitive information.

# Scanners

For information on scanner support under Linux, go to www.sane-project.org.
[/content]
