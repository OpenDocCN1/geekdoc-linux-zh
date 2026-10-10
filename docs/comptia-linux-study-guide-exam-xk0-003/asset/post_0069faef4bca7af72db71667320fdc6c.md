
**hub** A type of network hardware that serves as a central exchange point in a network. Each computer has a cable that links to the hub, so all data pass through the hub. Hubs echo all data they receive to all the other computers to which they connect. See also *switch*.

**hung** Term used to describe a program that has stopped responding to user input, network requests, or other types of input to which it should respond. Hung processes sometimes consume a great deal of CPU time.

**Hypertext Transfer Protocol (HTTP)** A protocol used for transferring Web pages from a Web server to a Web browser.

**Hypertext Transfer Protocol Secure (HTTPS)** A variant of HTTP that enables Secure Sockets Layer (SSL) encryption.

**IEEE-1394** An external bus technology that’s used to connect high-speed external devices such as hard disks, scanners, and video equipment.

**IMAP** See *Internet Message Access Protocol* (IMAP).

**incremental backup** A type of backup in which only files that have changed since the last backup are backed up. This is used to reduce the time required to back up a computer, at the cost of potentially greater restoration complexity.

**Industry Standard Architecture (ISA)** The expansion bus used on the original IBM PC. Most manufacturers began dropping ISA from their motherboards around 2001.

**info pages** A type of documentation similar to man pages (see *man pages*), but with a more complex hyperlinked structure within each document. The FSF and some other developers now favor info pages over man pages.

**inode** A filesystem (meaning 1) data structure that contains critical information on the file, such as its size and location on the disk.

**input/output (I/O)** A term that describes the acceptance of data from an external source or the sending of data to an external source. In some cases, the “external source” may be internal to the computer, as in I/O between a hard disk and the CPU or memory. In other cases, I/O is more clearly external, as in network I/O.

**installed file database** A database of files installed via the computer’s package manager (such as RPM or Debian), as well as associated information such as dependencies. Also called the “package database.”

**internal transfer rate** The rate of data transfer within a device. This is typically applied to hard disks and similar devices to describe how quickly they can read or write data from their physical media.

**International Organization for Standardization (ISO)** An international nongovernmental organization that publishes technical standards in many fields. In the computer field, examples include ISO-9660 (a common CD-ROM filesystem) and ISO/IEC 26300:2006 (the OpenDocument Format for office files, implemented by OpenOffice.org and several other Linux productivity programs).

**internet** Any collection of networks linked together by routers. See also *Internet*.

**Internet** The largest network on Earth, which connects computers from around the globe. When used in this way, the word is always capitalized. See also *internet*.

**Internet Message Access Protocol (IMAP)** A protocol for exchanging mail messages. The recipient initiates an IMAP session. IMAP differs from POP in that IMAP enables the recipient to leave messages in organized folders on the server; POP requires that the recipient download the messages to organize them.

**Internet Packet Exchange (IPX)** A protocol that underlies much of Novell’s original networking protocols. Despite the name, this protocol is unrelated to the Internet.

**Internet Printing Protocol (IPP)** A protocol for printing on a network, used in Linux by the Common Unix Printing System (CUPS) server.

**Internet Protocol (IP)** A low-level portion of the TCP/IP stack responsible for handling network addressing. See also *IPv4* and *IPv6*.

**Internet Software Consortium (ISC)** See *Internet Systems Consortium (ISC)*.

**Internet Systems Consortium (ISC)** A nonprofit corporation that develops a number of important network servers, including BIND, the standard Linux DHCP server, and an NTP server.

**interrupt request (IRQ)** A method by which peripherals (SCSI host adapters, sound cards, and so on) signal that they require attention from the CPU. An IRQ also refers to a specific interrupt signal line. The basic 32-bit x86 architecture supports 16 IRQs, numbered 0–15, but IRQs 2 and 9 are linked, so in practice, there are only 15 IRQs in the traditional architecture, and many of these are used by basic hardware like floppy disks. Modern computers usually support more than the 15 IRQs of the traditional x86 architecture.

**intrusion detection system (IDS)** Software that can detect suspicious activity on a computer or network and alert an operator to this activity.

**I/O** See *input/output (I/O)*.

**IP** See *Internet Protocol (IP)*.

**IP address** A computer’s numeric TCP/IP address, such as 192.168.45.203.

**IPP** See *Internet Printing Protocol (IPP)*.

**IPX** See *Internet Packet Exchange* (IPX).

**IRQ** See *interrupt request* (IRQ).

**ISA** See *Industry Standard Architecture* (ISA).

**ISC** See *Internet Systems Consortium* (ISC) (formerly *Internet Software Consortium*).

**ISO** See *International Organization for Standardization* (ISO).

## J

**Java** A programming language created by Sun Microsystems. Java is used on devices as diverse as cell phones and large server computers.

**Java Virtual Machine (JVM)** A method of running cross-platform computer software written in the Java programming language.

**JFS** See *Journaled Filesystem* (JFS).

**Journaled Filesystem (JFS)** One of several journaling filesystems for Linux. JFS was developed by IBM for its AIX OS. A subsequent implementation was created for OS/2, and Linux’s JFS is derived from this code.

**journaled filesystem** A type of filesystem that maintains a record of its operations. Such filesystems can typically recover quickly after a power failure or system crash. Common Linux journaling filesystems are ext3fs, ext4fs, ReiserFS, JFS, and XFS. See also *filesystem*.

**JVM** See *Java Virtual Machine* (JVM).

## K

**KDE Display Manager (KDM)** A popular XDMCP server for Linux.

**KDM** See *KDE Display Manager* (KDM).

## K

**kernel** The core program of any OS. The kernel provides interfaces between the software and the hardware and controls the operation of all other programs. Technically, the Linux kernel is the *only* component that is Linux; everything else, such as shells, X, and libraries, is available on other Unix-like systems.

**kernel module** A driver or other kernel-level program that may be loaded or unloaded as required.

**kernel module autoloader** A utility that loads and unloads kernel modules as required by the kernel, obviating the need to manually load and unload kernel modules.

**kernel ring buffer** A record of recent messages generated by the Linux kernel. Immediately after a Linux system boots, this buffer contains the bootup messages generated by drivers and major kernel subsystems. This buffer may be viewed with the `dmesg` command.

## L

**L2TP** See *Layer 2 Tunneling Protocol (L2TP)*.

**Layer 2 Tunneling Protocol (L2TP)** A method of passing multiple network protocols over a single connection, as in a VPN.

**LBA** See *linear block addressing (LBA)*.

**LDAP** See *Lightweight Directory Access Protocol (LDAP)*.

**libc** See *C library (libc)*.

**library** A collection of code that’s potentially useful to many programs. This code can be stored in files separate from the programs that use the library to save disk space and RAM when running those programs.

**Lightweight Directory Access Protocol (LDAP)** A tool for storing data in a type of database and accessing it over a network. LDAP is sometimes used as a form of network-based authentication.

**LILO** See *Linux Loader (LILO)*.

**linear block addressing (LBA)** A method of accessing data on a disk that uses a single sector number to retrieve data from that sector. LBA contrasts with cylinder/head/sector (CHS) addressing. Some sources refer to LBA as *logical* block addressing.

**Linux** 1. The open source kernel designed by Linus Torvalds as the core of a Unix-like operating system (OS). 2. A complete OS built around Linus Torvalds’s kernel. See also *GNU/Linux*.

**Linux Loader (LILO)** A popular Linux boot loader. LILO can boot a Linux kernel or redirect the boot process to another boot loader in a non-Linux partition, thus booting other OSs. LILO is similar to the competing Grand Unified Boot Loader (GRUB). See also *boot loader*.
