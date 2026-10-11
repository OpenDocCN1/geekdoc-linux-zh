
After a great deal of discussion and debate, Novell decided to aim for both audiences with this certification. To accommodate those who might not have a background in Linux, Novell included a series of objectives in the CLE that covers some basic Linux concepts.

This chapter and Chapter 3 of this study guide present a quick introduction to Linux and provide a review of some common Linux administrative tasks. Be aware that Novell assumes you have some degree of Linux experience prior to taking this course.

The content in this chapter and Chapter 3 are not intended to make you a Linux expert. Instead, they are intended to help you study the key tasks you will need to know in order to complete the exercises that appear later in the study guide. As mentioned in Chapter 1, you might want to obtain additional Linux study materials if you are new to Linux.

If you are already experienced with the Linux operating system, you may want to jump ahead to Chapter 4, “Introduction to Novell Nterprise Linux Services (NNLS),” using this chapter and Chapter 3 as a reference.

## A Historical Review of Linux

Linux is somewhat of an anomaly in the computer software world. Most software products, whether they are applications or operating systems, are developed as a part of a planned and well-organized effort. Usually, a software company first identifies a customer need. It then assembles a design team that hashes out a product requirements document (PRD).

The tasks in the PRD are allocated to teams of software developers who write their assigned portions of the code. The developed code is checked and the product is tested through a series of alpha- and beta-stage testing cycles. If it measures up to expectations (or is at least reasonably close), the finished product is shipped to the customer.

After the customer has used the product for a period of time, the software company notes its deficiencies and a revision process starts the cycle all over again.

The advent of Linux didn’t conform to this corporate product development cycle. Instead, one person—Linus Torvalds—initially developed it while he was a graduate student at the University of Helsinki in Finland.

During his studies in the early 1990s, Torvalds developed an interest in a freeware product called Minix, an educational version of the commercially developed Unix operating system. Andrew S. Tanenbaum, a university professor in the Netherlands, developed Minix, which looked and behaved like Unix, but was written completely from scratch. At the time, there were three main operating systems available:

- MS-DOS (and other variants such as PC-DOS and DR-DOS)
- Mac OS
- Unix

The source code for each of these operating systems was carefully protected by patent and copyright. At an earlier point in time, the source code to Unix had been made available to universities for teaching purposes. This practice had been stopped, however, leaving Tanenbaum without an effective means for teaching his students about the inner workings of an operating system. To provide this, he developed a small educational version of the Unix kernel that he called Minix. Its purpose was to provide students with a real operating system with source code access. Heralding things yet to come, Tanenbaum included the source code to Minix in his textbook *Operating Systems: Design and Implementation*.

Inspired by Tanenbaum and his Minix operating system, Torvalds developed his own Unix clone in 1991, which he dubbed Linux. It’s important to note that Torvalds didn’t initially develop a full-blown operating system complete with a full suite of applications and utilities. Instead, Linux version 0.02, released on October 5, 1991, provided only the Linux kernel and three utilities: bash (a command-line interface), update (a utility for flushing file system buffers), and gcc (a C++ compiler).

> **Note**: Interestingly, Tanenbaum and Torvalds didn’t always get along. They reportedly had many heated email discussions.

In an unprecedented move, Torvalds made the Linux source code freely available over the Internet to anyone who wanted to download it. Torvalds even went so far as to invite other programmers to refine and enhance his code. At that point, Linux became a worldwide collaborative project. Version 1.0 of the Linux kernel was released in 1994. The results since have been nothing short of amazing.

## About GNU

A discussion of the history of Linux would be incomplete without introducing GNU's Not Unix (GNU). The GNU movement exerted a significant influence on Torvald's development of Linux.

In the early 1980s, a programmer from the Massachusetts Institute of Technology named Richard Stallman objected to the proprietary nature of software development, so in 1983 he launched the GNU project. This project was dedicated to the advancement of freely distributable source code. Stallman felt that source code should be free from restrictions against copying, modification, and redistribution. He believed that allowing programmers to modify an application's source code would result in better software.

Powerful applications, such as the GNU C Compiler (gcc), were subsequently developed, and many of them were written to run on Linux. The availability of an array of powerful GNU applications on Linux was a key factor in taking the Linux kernel from a hobbyist's project to a robust tool capable of doing real work.

Linux itself is licensed under the GNU General Public License (GPL), which ensures that the operating system's source code will remain freely available to anyone who wants it. Anyone is free to download the Linux kernel's source code, modify it to meet their own requirements, and then recompile and run it.

This is a very significant aspect of Linux, as most software vendors do not make their products' source code available. To even further protect themselves, most have a section in their End User License Agreement (EULA) that forbids the user from reverse-compiling the software.

> **Note**: *Reverse-compiling is a process in which a special application is run against a binary file to reproduce the file as code in a text file. The resulting code isn't an exact duplicate of the original source code, but it can be very close.*

## Linux Distributions

You're probably aware that there are many different Linux distributions available. Among the choices, there's SUSE Linux, Red Hat Linux, Slackware Linux, and many others. This is yet another unique characteristic of Linux—nearly every other operating system is developed and marketed by a single vendor. For example, the only vendor who develops and sells OS X is Apple, Inc. You can't go to Novell or Microsoft for their versions of the Mac OS.

With Linux, however, there are many different, independent companies that each sell their own distribution.

The GPL also allows developers to bundle their own utilities and applications with the kernel and create what is known as a *distribution*.

To draw a comparison, imagine that you want to purchase a copy of the latest version of Windows. If Windows were licensed under the GPL, you would notice at your local computer store that there are hundreds of different “flavors” of the operating system available from many different software vendors—only one of which is Microsoft.

Each flavor is slightly different from the others; although they’re still based on the same operating system kernel. One might be optimized to provide web-based services, and another might be optimized for video editing. Imagine being able to sort through the different flavors and find the one that is best geared toward what you want to do.

Sounds far-fetched—but with Linux, that’s exactly what is available to you. Many different software vendors have taken the basic Linux kernel, modified and recompiled it according to their specifications, bundled some value-add applications with it, and redistributed it as their own Linux distribution.

Today there are, quite literally, more than 100 different distributions available. This course will use SUSE Linux from Novell as the distribution for running NNLS. Most of the concepts and skills taught in Chapters 2 and 3, however, can be transferred to almost any other distribution. You can learn more about these Linux distributions by visiting http://www.linuxiso.org.

## The Function of Linux in a Computer System

Let’s turn now to a discussion of the part Linux plays in a computer system. Believe it or not, this is actually a point of confusion for many. Because most of the PC systems sold over the past two decades have had a version of either MS-DOS or Windows installed on them, many end users don’t understand the modular role of an operating system.

Many tend to see the operating system as an integral, inseparable part of the PC. I’ve encountered many users who are under the impression that Linux is some kind of application that runs on top of DOS or Windows. I kindly explain to them that Linux is an operating system, not an application, and that it is used *instead of* DOS or Windows. In other words, it is a substitute for Windows, not a complementary application.
