
## UNIX Compatibility

Another reason to choose Linux is because of its UNIX compatibility. At the user level, Linux is very similar to UNIX. If you know UNIX, you know most of Linux.

At the programming level, most applications can be ported between Linux and UNIX with very little effort. Linux was deliberately designed to be UNIX-compatible to take advantage of the large body of UNIX software available.

Linux will interoperate exceedingly well with other UNIX machines. It uses standard UNIX services like RPC (Remote Procedure Call) and NFS (Network File System). It will also interoperate with Windows machines (via the Samba suite) and Macintoshes (with AppleTalk support).

Linux inherits UNIX’s strong flexibility and customizability, making it suitable for a wide range of applications, in traditional server and desktop applications as well as unusual applications such as embedded systems.

## Reliability and Performance

Yet another reason to choose Linux is its reliability and performance. Linux machines routinely stay up for months at a time. Linux provides full memory protection and isolation of tasks from the kernel and each other. That is, misbehaving or badly written programs can only crash themselves. They cannot bring down the operating system or crash other programs. Linux is a very robust system.

Linux is very small and makes efficient use of your hardware. You can quite comfortably set up Linux on an old 486 machine and use it as a firewall or Web server. Linux can breathe new life into old machines, saving you a lot of money.

## Support of Open Standards

Linux is a completely open system. It adheres to open standards like the various POSIX standards and the Internet Engineering Task Force standards for TCP/IP. By avoiding proprietary APIs (Application Programming Interfaces) and protocols, you lessen your dependence on a single supplier. You can choose from a number of Linux providers based on the service and value you get. With proprietary systems, once you commit, you have no choice but to continue with the original system provider, even if you become unhappy with the level of service.

## Linux Features

This section gives a brief overview of the outstanding technical features of Linux. These features provide much of the flexibility and stability of Linux. They are what make Linux so popular in critical server applications.

### Complete Memory Protection

As mentioned previously, Linux offers complete memory protection for all processes. Each process runs in its own virtual address space and cannot damage the address space of other processes or the kernel. A crashing process almost never brings down the system.

### Virtual Memory

Linux can extend the size of physical memory by using part of a disk drive as swap space. This allows you to run more programs at once than will fit into physical memory. This happens invisibly and without the programs’ knowledge. They simply assume they have exclusive access to a large memory space, and the Linux kernel manages the memory for them.

**Note**

Although this capability is referred to as swapping and the disk space as swap space, Linux’s mechanism for using disk space as virtual memory is more correctly referred to as paging.

### Full Multiuser Features

Linux is inherently multiuser. Each process and file is associated with a user. Using “telnet” or the X Window system, your Linux machine can run multiple interactive sessions simultaneously. You can also start jobs in the background and let them continue even after you log out.

Linux offers complete file protection to prevent users from damaging or (if you choose) accessing each other’s files. Important system files are protected from casual users.

### Support for Multiprocessing

If you are lucky enough to have a computer with more than one CPU, Linux can take advantage of multiple processors. The recent 2.2-series kernels greatly improve Linux’s handling of multiple CPUs when compared to the 2.0 series.

### Best-of-Breed TCP/IP Networking

Linux’s TCP/IP networking code is among the most advanced available. It offers full support for current TCP/IP protocols and includes experimental support for IPv6, the next-generation Internet protocol.

In addition to standard TCP/IP support, the Linux kernel includes IP firewalling code, IP masquerading (which lets you hide an entire network behind a dial-up link), IP quality-of-service controls, and many security features. These features rival similar features found in high-end routing equipment sold by companies like Cisco and Nortel.

Finally, because Linux uses resources quite sparingly, very low-end PCs can be used as routers and firewalls. I set up a Linux router and firewall on a second-hand Intel 386 machine that cost $200—less than the cost of an NT Server license.

### Interoperability with Windows and Macintosh

With the Samba suite, Linux can act as a file and print server for Windows clients. It can also be a client for an NT file and print server. Linux includes an AppleTalk module, which allows it to be a file and print server for Macintosh clients.

### Internet Server Software

Apache, the world’s most popular Web server, runs on Linux. Linux also includes an ftp server, an email transfer agent, and POP and IMAP mail servers. You can obtain an LDAP server for Linux for free on the Internet.

### Top-Notch Development Tools

Linux includes the GNU C, C++, Objective-C, and FORTRAN compilers, which are widely recognized as top-notch professional tools, used to develop everything from high-end Linux systems to embedded systems and video game consoles.

In addition, Linux includes a plethora of scripting languages like Perl, Tcl/Tk, Python, and many lesser-known ones. There are also a Linux port of Sun’s Java Development Kit and several Java Virtual Machine implementations.

Combined with powerful editors like Emacs and Vi, and professional debuggers like Gdb and Ddd, Linux provides an unparalleled development environment.

### Modular Kernel

Most drivers can be compiled either as an integral part of the kernel or as a loadable module. Hardware that must be configured before the kernel can access it (such as plug-and-play cards) must have modular drivers.

### Caldera OpenLinux

Caldera OpenLinux is a Linux distribution sold by Caldera Systems, Inc., of Provo, Utah. The version discussed in this book is OpenLinux 2.2, which includes a kernel of the modern 2.2 series. Caldera OpenLinux is a complete Linux distribution with hundreds of free software packages as well as some commercial software. The following commercial software is included with Caldera OpenLinux:

- WordPerfect 8 for Linux from Corel. Note that the version included with OpenLinux is the “download” version for personal use only.
- The StarOffice 5.0 office suite. Again, this version is for personal use only.
- The BRU backup and restore utility.
- Netscape Navigator, Communicator, and Composer.
- Power Quest Partition Magic (Caldera Systems Edition). This version does not recognize hard drives larger than 8 GB; you must purchase the full 4.0 version to handle larger drives.
- Power Quest Boot Magic. The Power Quest software eases the management of dual-boot systems.

Caldera OpenLinux also includes the following proprietary components:

- The Lizard graphical installation program
- The Lisa system administration tool
- Netaire Linux Client
- OpenLinux Windows tools

Caldera's differentiating features are its excellent graphical installation tool and its carefully chosen mix of packages, which, combined with the K Desktop Environment (KDE), make it an excellent choice for a desktop PC or personal workstation. Although most Linux vendors have concentrated on the server market, Caldera OpenLinux is a strong product aimed squarely at the desktop user.

Unfortunately, the license terms of Lizard and Lisa may prevent you from installing Caldera OpenLinux on more than one computer unless you purchase additional licenses. You may download the “Lite” version of the system, which does not include these components.
