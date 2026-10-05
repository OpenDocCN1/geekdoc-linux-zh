
ing that the messages are coming from a trusted host (page 391). The target machine responds to the messages, giving the intruder (privileged) access to the target.

IPC Interprocess communication. A method to communicate specific information between programs.

IPv4 IP version 4. See IP and IPv4.

IPv6 IP version 6. The next generation of Internet Protocol, which provides a much larger address space (2^128 bits vs 2^32 for IPv4) that is designed to accommodate the rapidly growing number of Internet addresses. IPv6 also has built-in configuration, enhanced security, better multicast support, and many other features.

iSCSI Small Computer System Interface. A network storage protocol that encapsulates data into TCP packets. You can use this protocol to connect a system to a storage array using an Ethernet connection.

ISDN Integrated Services Digital Network. A set of communications standards that allows a single pair of digital or telephone wires to carry voice, data, and video at a rate of 64 kilobits per second.

ISO International Organization for Standardization. A voluntary, nonprofit-organization founded in 1946. It is responsible for creating international standards in many areas, including computers and communications. Its members are the national standards organizations of 89 countries, including the American National Standards Institute.

ISO9660 The ISO standard defining a filesystem for CD-ROMs.

ISP Internet service provider. Provides Internet access to its customers.

job control A facility that enables you to move commands from the foreground to the background and vice versa. Job control enables you to stop commands temporarily.

journaling filesystem A filesystem that maintains a noncached log file, or journal, which records all transactions involving the filesystem. When a transaction is committed, it is marked as complete in the log file.

The log file results in reduced time spent recovering a filesystem after a crash, making it particularly valuable in systems where high availability is an issue.

JPEG Joint Photographic Experts Group. This committee designed the standard image-compression algorithm. JPEG is intended for compressing full-color or gray-scale digital images of natural, real-world scenes and does not work well on nonrealistic images, such as cartoons or line drawings. Filename extensions: .jpg, .jpeg

justify To expand a line of type in the process of formatting text. A line is justified by increasing the space between words and sometimes between letters on the line.

## Kerberos

An MIT-developed security system that authenticates users and machines. It does not provide authorization to services or databases; it establishes identity at logon, which is used throughout the session. Once you are authenticated, you can open any terminals, windows, services, or other network accesses as you can like until your session expires.

## kernel

The part of the operating system that allocates machine resources, including memory, disk space, and CPU (page 1143), to all other processes that run on a computer. The kernel includes the low-level hardware interfaces (drivers) and manages processes (page 1166), the means by which Linux executes programs. The kernel is part of the Linux system that Lin Torvalds originally wrote (see the beginning of Chapter 1).

## kernelspace

The memory (RAM) where the kernel resides. Code running in kernelspace has full access to hardware and all other processes in memory. See the KernelAnalysis-HOWTO.

## key binding

A keyboard is said to be bound to the action that results from input. Typically keys are bound to the letters that appear on the keyscaps: when you press A, A appears on the screen. The binding usually refers to what happens when you press a combination of keys, one of which is CONTROL, ALT, META, or SHIFT, when you press a series of keys, the first of which is typically ESCAPE.

## keyboard

A hardware input device consisting of a number of mechanical buttons (keys) that the user presses to input characters to a computer. By default a keyboard is connected to standard input of a shell.

## kilo-

In the binary system, the prefix kilo multiplies by 2^10 (i.c., 1,024). Kilobit and kilobyte are common units of this prefix. Abbreviated as k.

## Korn Shell

ksh. A command processor, developed by David Korn at AT&T Bell Laboratories, that is compatible with the Bourne shell but includes many extensions. See also on page 1171.

## LAN

Local area network. A network that connects computers within a localized area (such as a single site, building, or department).

## large number

Visit mathworld.wolfram.com/LargeNumber.html for a comprehensive list.

## LDAP

Lightweight Directory Access Protocol. A simple protocol for accessing online directory services. LDAP is a lightweight alternative to the X.500 Directory Access Protocol (DAP). It can be used to access information about people, systems, network devices, email directories, and systems. In some cases, it can be used as an alternative for services such as NIS. Given a name, many clients can use LDAP to discover the corresponding email address. See directory service on page 1145.

## leaf

In a tree structure, the end of a branch that cannot support other branches. The Linux filesystem hierarchy is conceptualized as a tree, files that are not leaves. See node on page 1162.

## GLOSSARY 1157

least privilege, concept of Mistakes made by a user working with root privileges can be much more devastating than those made by an ordinary user. When you are working on the computer, especially when you are working as the system administrator, perform any task using the logged as an ordinary user, do if you work with root privileges, do as much as you can as an ordinary user, log in as root or give an su or sudo command.

## 1158 GLOSSARY

log inTo gain access to a computer by responding to the login: Also Pass-word.

log out

To end your session by exiting from the shell. Also log off.

logical expression

A collection of strings separated by logical operators (>, >=, !=, <=) can be evaluated as true or false. Also Boolean (1138) expression.

.log file

A file in a user's home directory that the TC Shell executes when you log in. You can use this file to set environment variables and run commands at the beginning of each session.

login name

See username on page 179.

login shell

The shell that you are using when you in. The login shell can fork others, utilities, and programs.

.logout file

A file in a user's home directory that the TC Shell executes when you log out, assuming that the TC Shell is your login shell. You can put in the logout file commands that you want each time you log out.

MAC address

Media Access Control address. The unique hardware address of a device connected to a shared medium. Each network adapter has a globally MAC address that it stores in ROM. MAC addresses are 6 bytes long, enabling 2^46 (about 300 trillion) possible addresses or 65,536 addresses for each IPv4 address.

A MAC address performs the same role for Ethernet as an IP address performs for TCP/IP: It provides a unique way to identify a host.

machine collating sequence

The sequence in which the computer orders characters. The machine collating sequence affects the outcome of sorts and other procedures that put lists in alphabetical order. Many computers use ASCII codes so their machine collating sequences correspond to the ordering of the ASCII codes for characters.

macro

A single instruction that program replaces by several (usually more complex) instructions. The C compiler recognizes macros, which are defined using a #define instruction to the preprocessor.

magic number

A number, which occurs in the first 512 bytes of a binary file, is a 1-, 2-, or 4-byte numeric value or string that uniquely identifies the type of file (like a DOS-3 filename extension). See /usr/share/magic and the magic page for more information.

main memory

Random access memory (RAM), an integral part of the computer. Although disk storage is sometimes referred to memory, it is never referred as main memory.

major device number

A number assigned to a class of devices, such as terminals, printers, or disks. Using the ls utility with the -l option to list the contents of the /dev directory displays the major and minor device numbers of many devices (as major, minor).
