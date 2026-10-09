
# GLOSSARY

time the inode was last modified, owner and group IDs, access privileges, number of links, and pointers to the data blocks that contain the file itself. Each directory entry associates a filename with an inode. Although a single file might have several filenames (one for each link), it has only one inode.

## input
Information that is fed to a program from a terminal or other file. See *standard input* on page 1274.

## installation
A computer at a specific location. Some aspects of the Linux system are installation dependent. Also *site*.

## interactive
A program that allows ongoing dialog with the user. When you give commands in response to shell prompts, you are using the shell interactively. Also, when you give commands to utilities, such as vim and mail, you are using the utilities interactively.

## interface
The meeting point of two subsystems. When two programs work together, their interface includes every aspect of either program that the other deals with. The *user interface* (page 1279) of a program includes every program aspect the user comes into contact with: the syntax and semantics involved in invoking the program, the input and output of the program, and its error and informational messages. The shell and each of the utilities and built-in commands have a user interface.

## International Organization for Standardization
See *ISO* on the next page.

## internet
A large network that encompasses other, smaller networks.

## Internet
The largest internet in the world. The Internet (uppercase “I”) is a multilevel hierarchy composed of backbone networks (ARPANET, NSFNET, MILNET, and others), midlevel networks, and stub networks. These include commercial (.com or .co), university (.ac or .edu), research (.org or .net), and military (.mil) networks and span many different physical networks around the world with various protocols, including the Internet Protocol (IP). Outside the United States, country code domains are popular (.us, .es, .mx, .de, and so forth), although you will see them used within the United States as well. See *IP*.

## Internet Protocol
See *ISP* on the next page.

## Internet service provider
An inhouse network designed to serve a group of people such as a corporation or school. The general public on the Internet does not have access to an intranet. See page 281.

## invisible file
See *hidden filename* on page 1253.

## IP
Internet Protocol. The network layer for TCP/IP. IP is a best-effort, packet-switching, connectionless protocol (page 1244) that provides packet routing, fragmentation, and reassembly through the data link layer. *IPv4* is slowly giving way to *IPv6*.

## IP address
Internet Protocol address. A four-part address associated with a particular network connection for a system using the Internet Protocol (IP). A system that is attached to multiple networks that use the IP will have a different IP address for each network interface. See *multicast* on page 1262.

## IP multicast

## IP spoofing
A technique used to gain unauthorized access to a computer. The would-be intruder sends messages to the target machine. These messages contain an IP address indicating that the messages are coming from a trusted host. The target machine responds to the messages, giving the intruder (privilegied) access to the target.

## IPC
Interprocess communication. A method to communicate specific information between programs.

## IPv4
*IP* version 4. See *IP* and *IPv6*.

## IPv6
*IP* version 6. The next generation of Internet Protocol, which provides a much larger address space (2$^{128}$ bits versus 2$^{32}$ bits for IPv4) that is designed to accommodate the rapidly growing number of Internet addressable devices. IPv6 also has built-in autoconfiguration, enhanced security, better multicast support, and many other features.

## iSCSI
Internet Small Computer System Interface. A network storage protocol that encapsulates SCSI data into TCP packets. You can use this protocol to connect a system to a storage array using an Ethernet connection.

## ISDN
Integrated Services Digital Network. A set of communications standards that allows a single pair of digital or standard telephone wires to carry voice, data, and video at a rate of 64 kilobits per second.

## ISO
International Organization for Standardization. A voluntary, nontreaty organization founded in 1946. It is responsible for creating international standards in many areas, including computers and communications. Its members are the national standards organizations of 89 countries, including the American National Standards Institute.

## ISO 9660
The *ISO* standard defining a filesystem for CD-ROMs.

## ISP
Internet service provider. Provides Internet access to its customers.

## job control
A facility that enables you to move commands from the foreground to the background, and vice versa. Job control enables you to stop commands temporarily.

## journaling filesystem
A filesystem that maintains a noncached log file, or journal, which records all transactions involving the filesystem. When a transaction is complete, it is marked as complete in the log file. The log file results in greatly reduced time spent recovering a filesystem after a crash, making it particularly valuable in systems where high availability is an issue.

## JPEG
Joint Photographic Experts Group. This committee designed the standard image-compression algorithm. JPEG is intended for compressing either full-color or gray-scale digital images of natural, real-world scenes and does not work as well on nonrealistic images, such as cartoons or line drawings. Filename extensions: .jpg, .jpeg.

## justify
To expand a line of type in the process of formatting text. A justified line has even margins. A line is justified by increasing the space between words and sometimes between letters on the line.

## Kerberos
An MIT-developed security system that authenticates users and machines. It does not provide authorization to services or databases; it establishes identity at logon, which is used throughout the session. Once you are authenticated, you can open as many terminals, windows, services, or other network accesses as you like until your session expires.

## kernel
The part of the operating system that allocates machine resources, including memory, disk space, and CPU (page 1244) cycles, to all other programs that run on a computer. The kernel includes the low-level hardware interfaces (drivers) and manages processes (page 1267), the means by which Linux executes programs. The kernel is the part of the Linux system that Linus Torvalds originally wrote (see the beginning of Chapter 1).

## kernel space
The part of memory (RAM) where the kernel resides. Code running in kernel space has full access to hardware and all other processes in memory. See the Kernel Analysis-HOWTO.

## key binding
A key board key is said to be bound to the action that results from pressing it. Typically keys are bound to the letters that appear on the keycaps: When you press A, an A appears on the screen. Key binding usually refers to what happens when you press a combination of keys, one of which is CONTROL, ALT, META, or SHIFT, or when you press a series of keys, the first of which is typically ESCAPE.

## keyboard
A hardware input device consisting of a number of mechanical buttons (keys) that the user presses to input characters to a computer. By default a keyboard is connected to standard input of a shell.

## kilo-
In the binary system, the prefix *kilo-* multiplies by 2$^{10}$ (i.e., 1,024). Kilobit and kilobyte are common uses of this prefix. Abbreviated as *k*.

## Korn Shell
*ksh*. A command processor, developed by David Korn at AT&T Bell Laboratories, that is compatible with the Bourne Shell but includes many extensions. See also *shell* on page 1272.

## I10n
Localization. An abbreviation of the word *localization*: the letter *l* followed by 10 letters (*ocalizatio*) followed by the letter *n*.

## LAN
Local area network. A network that connects computers within a localized area (such as a single site, building, or department).

## large number
Visit mathworld.wolfram.com/LargeNumber.html for a comprehensive list.

## LDAP
Lightweight Directory Access Protocol. A simple protocol for accessing online directory services. LDAP is a lightweight alternative to the X.500 Directory Access Protocol (DAP). It can be used to access information about people, system users, network devices, email directories, and systems. In some cases, it can be used as an alternative for services such as NIS. Given a name, many mail clients can use LDAP to discover the corresponding email address. See *directory service* on page 1247.

## leaf
In a tree structure, the end of a branch that cannot support other branches. When the Linux filesystem hierarchy is conceptualized as a tree, files that are not directories are leaves. See *node* on page 1264.
