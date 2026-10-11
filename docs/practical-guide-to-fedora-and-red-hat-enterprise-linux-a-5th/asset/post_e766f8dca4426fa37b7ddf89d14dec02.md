
## stylesheet
See CSS on page 1077.

## subdirectory
A directory that is located within another directory. Every directory except the root directory is a subdirectory.

## subnet
Subnetwork. A portion of a network, which may be a physically independent network segment, that shares a network address with other portions of the network and is distinguished by a subnet number. A subnet is to a network as a network is to an internet.

## subnet address
The subnet portion of an IP address. In a subnetted network, the host portion of an IP address is split into a subnet portion and a host portion using a subnet mask (also address mask). See also *subnet number*.

## subnet mask
A bit mask used to identify which bits in an IP address correspond to the network address and subnet portions of the address. Called a subnet mask because the network portion of the address is determined by the number of bits that are set in the mask. The subnet mask has ones in positions corresponding to the network and subnet numbers and zeros in the host number positions. Also *address mask*.

## subnet number
The subnet portion of an IP address. In a subnetted network, the host portion of an IP address is split into a subnet portion and a host portion using a *subnet mask*. Also *address mask*. See also *subnet address*.

## subpixel hinting
Similar to *anti-aliasing* (page 1069) but takes advantage of colors to do the anti-aliasing. Particularly useful on LCD screens.

## subroutine
See *procedure* on page 1100.

## subshell
A shell that is forked as a duplicate of its parent shell. When you run an executable file that contains a shell script by using its filename on the command line, the shell forks a subshell to run the script. Also, commands surrounded with parentheses are run in a subshell.

## superblock
A block that contains control information for a filesystem. The superblock contains housekeeping information, such as the number of inodes in the filesystem and free list information.

## superserver
The extended Internet services daemon.

## Superuser
A user working with **root** privileges. This user has access to anything any other system user has access to and more. The system administrator must be able to become Superuser (work with **root** privileges) to establish new accounts, change passwords, and perform other administrative tasks. The username of Superuser is usually **root**. Also *root or root user*.

## swap
The operating system moving a process from main memory to a disk, or vice versa. Swapping a process to the disk allows another process to begin or continue execution.

## swap space
An area of a disk (that is, a swap file) used to store the portion of a process's memory that has been paged out. Under a virtual memory system, the amount of swap space—rather than the amount of physical memory—determines the maximum size of a single process and the maximum total size of all active processes. Also *swap area* or *swapping area*.

## switch
See *network switch* on page 1096.

## symlink
A directory entry that points to the pathname of another file. In most cases a symlink link to a file can be used in the same way a hard link can be used. Unlike a hard link, a symlink link can span file systems and can connect to a directory.

## system administrator
The person responsible for the upkeep of the system. The system administrator has the ability to log in as root or use sudo to work with root privileges. See also *Superuser*.

## system console
See *console* on page 1076.

## system mode
The designation for the state of the system while it is doing system work. Some examples are making system calls, running NFS and autofs, processing network traffic, and performing kernel operations on behalf of the system. Contrast with *user mode* (page 1113).

## System V
One of the two major versions of the UNIX system.

## TC Shell
tesh. An enhanced but completely compatible version of the BSD UNIX C shell, *csh*.

## TCP
Transmission Control Protocol. The most common transport layer protocol used on the Internet. This connection-oriented protocol is built on top of *IP* (page 1088) and is nearly always seen in the combination *TCP/IP* (TCP over *IP*). TCP adds reliable communication, sequencing, and flow control and provides full-duplex, process-to-process connections. UDP (page 1112), although connectionless, is the other protocol that runs on top of IP.

## tera-
In the binary system, the prefix *tera-* multiplies by $2^{40}$ (1,099,511,627,776). Tera-byte is a common use of this prefix. Abbreviated as T. See also *large number* on page 1090.

## termcap
Terminal capability. On older systems, the */etc/termcap* file contained a list of various types of terminals and their characteristics. *System V* replaced the function of this file with the *term info* system.

## terminal
Differentiated from a *workstation* (page 1116) by its lack of intelligence, a terminal connects to a computer that runs Linux. A workstation runs Linux on itself.

## term info
Terminal information. The */usr/lib/term info* directory contains many subdirectories, each containing several files. Each of those files is named for and holds a summary of the functional characteristics of a particular terminal. Visually oriented textual programs, such as vim, use these files. An alternative to the *term cap* file.

## text box
A GUI widget (page 1115) that allows a user to enter text.

## theme
Defined as an implicit or recurrent idea, *theme* is used in a GUI to describe a look that is consistent for all elements of a desktop. Go to themes.freshmeat.net for examples.

## thicknet
A type of coaxial cable (thick) used for an Ethernet network. Devices are attached to thicknet by taping the cable at fixed points.

## thinnet
A type of coaxial cable (thin) used for an Ethernet network. Thinnet cable is smaller in diameter and more flexible than *thicknet* cable. Each device is typically attached to two separate cable segments by using a T-shaped connector; one segment leads to the device ahead of it on the network and one to the device that follows it. See *reentrant* on page 1102.

## thread-safe

## thumb
The movable button on the *scrollbar* (page 1105) that positions the image in the window. The size of the thumb reflects the amount of information in the buffer. Also *bubble*.

## tick
A mark, usually in a *check box* (page 1074), that indicates a positive response. The mark can be a check mark (v) or an x. Also *check mark* or *check*.

## TIFF
Tagged Image File Format. A file format used for still-image bitmaps, stored in tagged fields. Application programs can use the tags to accept or ignore fields, depending on their capabilities.

## tiled windows
An arrangement of windows such that no window overlaps another. The opposite of *cascading windows* (page 1073).

## time to live
See *TTL*.

## toggle
To switch between one of two positions. For example, the *ftp glob* command toggles the *glob* feature: Give the command once, and it turns the feature on or off; give the command again, and it sets the feature back to its original state.

## token
A basic, grammatically indivisible unit of a language, such as a keyword, operator, or identifier.

## token ring
A type of *LAN* (page 1090) in which computers are attached to a ring of cable. A token packet circulates continuously around the ring. A computer can transmit information only when it holds the token.

## tooltip
A minicontext help system that a user activates by allowing the mouse pointer to *hover* (page 1086) over an object (such as those on a panel).

## transient window
A dialog or other window that is displayed for only a short time.

## Transmission Control Protocol
See *TCP* on page 1110.

## 1112 GLOSSARY

## Trojan horse

A program that does something destructive or disruptive to your system. Its action is not documented, and the system administrator would not approve of it if she were aware of it.

The term *Trojan horse* was coined by MIT-hacker-turned-NSA-spook Dan Edwards. It refers to a malicious security-breaking program that is disguised as something benign, such as a directory *lister*, archive utility, game, or (in one notorious 1990 case on the Mac) a program to find and destroy viruses. Similar to *back door* (page 1070).

## TTL

Time to live.

- All DNS records specify how long they are good for—usually up to a week at most. This time is called the record’s *time to live*. When a DNS server or an application stores this record in *cache* (page 1073), it decrements the TTL value and removes the record from cache when the value reaches zero. A DNS server passes a cached record to another server with the current (decremented) TTL, guaranteeing the proper TTL, no matter how many servers the record passes through.
- In the IP header, a field that indicates how many more hops the packet should be allowed to make before being discarded or returned.

## TTY

Teletypewriter. The terminal device that UNIX was first run from. Today TTY refers to the screen (or window, in the case of a terminal emulator), keyboard, and mouse that are connected to a computer. This term appears in UNIX, and Linux has kept the term for the sake of consistency and tradition.

## tunneling

Encapsulation of protocol A within packets carried by protocol B, such that A treats B as though it were a data link layer. Tunneling is used to transfer data between administrative domains that use a protocol not supported by the internet connecting those domains. It can also be used to encrypt data sent over a public internet, as when you use *ssh* to tunnel a protocol over the Internet. See also *VPN* (page 1114) and *port forwarding* (page 1099).

## UDP

User Datagram Protocol. The Internet standard transport layer protocol that provides simple but unreliable datagram services. UDP is a *connectionless protocol* (page 1076) that, like *TCP* (page 1110), is layered on top of *IP* (page 1088).

Unlike *TCP*, UDP neither guarantees delivery nor requires a connection. As a result it is lightweight and efficient, but the application program must handle all error processing and retransmission. UDP is often used for sending time-sensitive data that is not particularly sensitive to minor loss, such as audio and video data.

## UID

User ID. A number that the *passwd* database associates with a username.
