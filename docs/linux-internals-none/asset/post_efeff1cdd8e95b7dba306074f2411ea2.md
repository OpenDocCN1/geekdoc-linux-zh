
den code snippets, you sometimes find beautiful and superbly crafted yet stunningly efficient design.

## History of Linux

Linux began, as do most successful projects, as a project sprung from necessity, in Finland in 1991. Linus B. Torvalds, then a student at the University of Helsinki, bought himself a PC based on the i386, the first Intel CPU to have on-chip support for virtual memory management. Not entirely satisfied with the MS/DOS operating system, Torvalds decided to implement the Minix OS (need to amplify the origins and nature of Minix) on his PC instead.

When AT&T in the seventies began to realize that their UNIX operating system was becoming a valuable commercial product it decided with version 7 to prohibit the distribution of the source code together with the binary as was previously the practice. Many universities as a result had to drop the study of UNIX and reverted back to studying only theory.

Unfortunately, studying theory does not provide the student the confidence with OS theory that could be achieved when actually applying the concepts to a real OS. Therefore, Andrew Tanenbaum decided to develop an OS that included all of the concepts and features of UNIX but from completely new source code. This way he could avoid the strict licensing restrictions of AT&T and still teach his students about UNIX. Minix was from the beginning designed to run on PCs and was based originally on the feature set of AT&T UNIX Version 7. Soon, however, Tanenbaum significantly enhanced Minix until it came to include all the functions and feature of a modern OS. Minix is still used today as a pedagogic tool but also in production system at selected sites. For a comprehensive overview of Minix, it is advisable to study Andrew S. Tanenbaum’s and Albert S. Woodhull’s seminal work (Operating Systems by Prentice Hall).

Soon he was enhancing Minix to provide the functions and features that he needed for his study. He decided that Minix was too much an academic OS; he began to create an operating system from scratch. Torvalds’ most important decision was to make his new OS’s source code freely available over the Internet—which is to say, Open Source—under the name of Linux, a contraction of Linus and UNIX.

The first version, version 0.01, was made available for download on the Internet in August 1991. In October of the same year, Torvalds made an official announcement of the availability of version 0.02. This version already could execute such UNIX user-land programs as the bash shell, the GNU gcc compiler, and other basic utilities, but not much more.

Because of the Open Source nature of the project, and with the source code immediately available all over the globe, soon many hackers, computer freaks, and PC enthusiasts began looking at the code and enhancing it. Many began to send their suggestions to Torvalds, who inaugurated the “official” reference Linux source code development tree. Looking through their code suggestions, he rejected most, but some he incorporated into Linux. Development continued this way for three more years before a first production version was announced.

In 1992 and 1993, the first Linux distributions appeared. Distributions, the primary way to obtain a fully functional OS, include the Linux kernel, the X windowing system, and a comprehensive package of application programs and utilities, which can number in the hundreds or more. Distributions also include an installer, which prepares the binary image of the OS and the boot/shutdown scripts, and makes sure that all components are compatible with and tuned for each other. Last but not least, distributions also provide documentation. Today many distributions exist, the most successful being RedHat, SuSE, and Caldera.

In March 1994, version 1.0 was made available. It still showed the occasional erratic behavioral quirk, as I fondly remember, but it was quite usable. Linux 1.0 featured TCP/IP, SLIP, and printer support, and had enough drivers to support a wide range of the PC equipment then available. After that, the Linux boom really began, and millions of enthusiasts in all corners of the world started using the system.

The highlights of the steady ascent of Linux to its status as the major power in the IT market today are shown in Table 1.1.

**TABLE 1.1**
**Timeline of Linux development**

| August 1991 | Version 0.01 |
|---|---|
| October 1991 | Official announcement 0.02 |
| November 1993 | First Slackware Distribution with kernel 0.99 |
| March 1994 | Version 1.0 |
| June 1995 | First port to the Alpha architecture |
| October 1996 | Debian Linux is used on the space shuttle in orbit (on an IBM laptop) |
| January 1999 | Version 2.2.0 |
| March 2000 | Version 2.3.49 (pre 2.4.0) |

## Linux Functionality

Linux has come a long way from its humble beginning in 1991. As the phenomenon of Open Source has spread far and wider, more and more people have contributed to the Linux kernel and to its subsystems. At the same time, thousands upon thousands of userspace packages have been added at ever-increasing frequency. With the concurrent rise of the World Wide Web, some Web sites are devoted solely to the purpose of daily announcements about new software versions available for Linux.

Linux is available on many platforms, including Intel, Sparc, Alpha, MIPS, the Motorola 68000 family, and PowerPC. Early on, Linux was brought into conformance with the Portable Operating System Interface (POSIX) standard. Its POSIX compliance allows applications developed under Linux to be very easily ported to other POSIX-compliant OSSs. On Intel CPU-based systems, the Linux binaries conform to iBCS standards. This allows, for example, a statically linked program to run under FreeBSD or Solaris without recompilation.

Technically, Linux provides (among others) the following functions:

- Multi-user environment
- Multi-process, multi-processor (SMP) environment
- Inter-Process communication (IPC, pipes, sockets)
- Process control
- POSIX-style terminal management
- TCP/IP, Ipv4, Ipv6 support
- Support for a wide variety of hardware
- Demand paging with optional Least Recently Used (LRU) algorithms and page coloring
- Swapping
- Buffer cache
- Dynamic and shared libraries
- Support for many file systems (ext2fs, UFS, NTFS, HPFS, MS/DOS, ISO9660, coda, and many more)

## Novelties in the 2.4 Kernel

Linux 2.2 was a major improvement over Linux 2.0 and the Linux 1.x series. It supported many new file systems, a new system of file caching, and it was much more scalable. Linux 2.4 builds on these improvements and more, to be the best Linux kernel yet in a wide variety of situations.

The Linux kernel is a collection of modular components and subsystems, including device drivers, protocols, and other types of component. These are glued to the core of the Linux kernel by Application Programming Interfaces (APIs), which provide a standard method by which the Linux kernel can be expanded. Most of this book focuses on these components of the Linux OS, the components that do the most work.

- In the 2.4 kernel series Linux has vastly improved its ability to handle a large number of processes and tasks. The task limit now numbers beyond 4,090. The scheduler’s efficiency has been improved somewhat, and Linux 2.4 can better handle systems with a large number of concurrent processes than could earlier versions.
- Linux 2.4 can also handle much larger “enterprise-class” hardware than could previous Linux kernel revisions. For example, Linux 2.4, with appropriate patches, can address beyond 4GB of RAM. (One machine I have seen is configured with 12GB of RAM and has one address space of 8.3GB resident size.)
- Scalability on SMP systems is now comparable to proprietary OSs and in some instances even better.
- Support for other processor platforms has been increased, too. In addition to the traditional architectures mentioned earlier, Linux 2.4 now supports the new Transmeta Crusoe processor directly. The 3Com PalmPilot as well as Psion6, both run Linux natively. The new Intel IA64 (next generation, 64-bit successor to the venerable Intel x86 architecture), will probably be ready in 2000, but is not yet included directly with the kernel.
- New file system support has been added (the Irix efs file system and the UDF standard used on DVD disks), while certain other support has been made obsolete (QNX and ext1).
- The introduction of *tasklets*, a revolutionary way of handling low-level interrupts, makes the TCP/IP stack (along with other subsystems and userprograms) much more efficient. New networking protocol software is capable of handling the DECNet standard.
- Linux 2.2 and Linux 2.0 include built-in support for starting a Java interpreter (if present) whenever a Java application is executed. (Linux was one of the first OSs to do this at the kernel level.) Linux 2.4 still includes support for loading Java interpreters as necessary.

1. We will see how tasklets work in Chapter 3.
