
# Common Commands RC5

| Command | Description |
| --- | --- |
| quotaoff | Turn off file-system quotas. |
| quotaon | Turn on file-system quotas. |
| repquota | Summarize quotas for a file system. |
| rm | Remove files or directories. |
| rmdir | Remove empty directories. |
| route | Show or manipulate routing table. |
| rpcinfo | Report RPC (Remote Procedure Calls) information. |
| sed | Stream Editor. |
| setquota | Set disk quotas. |
| showmount | Show mount information for an NFS (Network File System). |
| shutdown | Bring the system down. |
| sleep | Delay for a specified amount of time. |
| sort | Sort lines of files. |
| strace | Trace system calls and signals. |
| strings | Print printable characters in files. |
| su | Run a shell with substitute user and group IDs. |
| tail | Output the last part of files. |
| tar | Archiving utility. |
| tcsh | C shell with filename completion and command editing. |
| telnet | Telnet client. |
| tftp | TFTP (Trivial File Transfer Protocol) client. |
| traceroute | Print the route that packets take to a destination host. |
| true | Exit with a status code indicating success. |
| umount | Unmount a file system. |
| uname | Print system information. |
| useradd | Create a new user. |
| userdel | Delete user account. |
| uptime | Print how long the system has been running. |
| vi | Text editor. |
| w | Show users that are logged on and what they are doing. |

Reference Center Common Commands

| Command | Description |
| --- | --- |
| wall | Send message to every user’s terminal. |
| wc | Print the number of bytes, words, and lines in files. |
| whereis | Locate the binary, source, and manual page files for a command. |
| which | Show the full path of commands. |
| who | Show users that are logged on. |
| whoami | Print effective user ID. |
| write | Send a message to another user. |
| ypdomainname | Show or set system’s NIS (Network Information System) or YP (Yellow Pages) domain name. |

# COMMON PORTS

What follows is a list of port names and services that correspond to the most commonly used Unix and Linux services.

> For a more comprehensive list, see the /etc/services file.

| Service | Port(s) |
| --- | --- |
| Echo | 7 |
| Daytime | 13 |
| qotd (Quote Of The Day) | 17 |
| FTP-data | 20 |
| FTP | 21 |
| SSH | 22 |
| Telnet | 23 |
| SMTP (Simple Mail Transfer Protocol) | 25 |
| Time server | 37 |
| Whois | 43 |
| DNS (Domain Name System) | 53 |
| TFTP (Trivial File Transfer Protocol) | 69 |
| Finger | 79 |
| HTTP (Hypertext Transfer Protocol) | 80 |
| POP2 (Post Office Protocol 2) | 109 |
| POP3 (Post Office Protocol 3) | 110 |
| Portmapper | 111 |
| Ident | 113 |
| NNTP (Network News Transfer Protocol) | 119 |
| NTP (Network Time Protocol) | 123 |
| Samba | 137–139 |
| IMAP2 (Internet Message Access Protocol) | 143 |
| SNMP (Simple Network Management Protocol) | 161 |

| Service | Port(s) |
| --- | --- |
| BGP (Border Gateway Protocol) | 179 |
| IMAP3 (Internet Message Access Protocol) | 220 |
| LDAP (Lightweight Directory Access Protocol) | 389 |
| HTTPS (Secure Hypertext Transfer Protocol) | 443 |
| rlogin | 513 |
| rsh | 514 |
| Line printer (lpr) spool | 515 |
| Talk | 517 |
| Time server | 525 |
| NNTP (Network News Transfer Protocol) | 563 |
| IPP (Internet Printing Protocol) | 631 |
| LDAPS (Secure Lightweight Directory Access Protocol) | 636 |
| IMAPS (Secure Message Access Protocol) | 993 |
| POP3 (Secure Post Office Protocol) | 995 |
| NFS (Network File System) | 2049 |
| MySQL | 3300 |
| VNC (Virtual Network Computing) | 5900 |
| SSH (Secure Shell) | 5900+ |
| X11 | 6063 |
| XFS (Secure File System) | 7100 |

# IP ADDRESSING

This section provides concise details about IP addressing such as protocol headers for TCP, and UDP.

# Dotted Decimal Notation

IP addresses are 32 bits in length, for example:
```
11000000 10101000 00000001 00000001
```
For ease of readability, IP addresses are denoted in dotted notation, for example:
```
192.168.1.1
```

# Classes

IP addresses have been classified into five classes in which allocate different sizes of networks.

# Class A

Class addresses have been assigned to very large organizations that have a large number of hosts on each network. Note that class A addresses are often wasted.

| Class | Bits |
| --- | --- |
| 0 | 8 |

- **First Octet**: The first bit is always 0.
- **Maximum Networks**: The network address is denoted by the first octet. Therefore $2^{24}-2=16,777,214$ hosts are possible.

# Class B

Class addresses are assigned to organizations that consist of a large number of networks and hosts. Therefore, many B addresses are assigned.

| Class | Bits |
| --- | --- |
| 01 | 16 |

- **First Octet**: The first two bits are 10.
- **Maximum Networks**: The network address is denoted by first and second octet. Therefore $2^{14}=16,384$ class B networks are possible.

# Class C

Class addresses are used by organizations consisting of a small number of hosts per network.

| Class | Bits |
| --- | --- |
| 010 | 24 |

- **First Octet**: The first three bits are 1, and 0.
- **Maximum Networks**: The network address is denoted by the first, second, and third octets. Therefore $2^{21}=2,097,152$ class C networks are possible.
- **Maximum Hosts per Network**: Hosts are denoted by the last octet. Therefore $2^8-2=254$ hosts are possible per network.

# Class D

Class D is a reserved class that was designed to be used to send multicast messages to a group of hosts.

| Class | Bits |
| --- | --- |
| 1110 | 4 |

- **First Octet**: Ranges from 224 to 239. The first four bits are 1, 1, 1, and 0.

# Class E

Class E is a reserved class. No IP addresses that fall under this class are assigned on the Internet.

| Class | Bits |
| --- | --- |
| 11110 | 5 |

- **First Octet**: Ranges from 240 to 255. The first five bits are 1, 1, 1, 1, and 0.

# Subnet Masks

Network addresses and host addresses are identified by the use of subnet masks. A subnet mask is a series of bits that match the network portion of a given address. For example, the following would be the network mask for a class B IP address:

```
11111111 11111111 00000000 00000000
```
The preceding mask would be 255.255.255.0 in dotted decimal notation.

# CIDR (Classless Inter-Domain Routing)

Because of the tremendous growth of the Internet, the five IP classes just listed were not sufficient to accommodate the many network schemes needed.

CIDR addresses, which were designed to meet this growing need, are denoted by the following notation:

```
PREFIX/mask
```

where PREFIX is the IP address prefix, and mask is the length of the mask. For example:

```
192.168.1.0/24
```

Here, the PREFIX is 24 bits long, while the suffix is the remaining 8 bits. Therefore, this CIDR class will include the following addresses: 192.168.1.0–192.168.1.255.

# Loopback

The following range is referred to as a “loopback” range:

```
127.0.0.0/8
```
This range is used to designate the loopback address of the local host. Any packet sent to an address in this range will revert back to the host. Note that packets destined for an address in the loopback range do not propagate to the hardware network device, and therefore are never placed on the physical network wire.

# Private Addresses

The Internet Assigned Numbers Authority (IANA) has reserved the following three IP blocks for privateets:
- 10.0.0.0–10.255.255.255 (CIDR Notation: 10.0.0.0/8)
- 172.16.0.0–172.31.255.255 (CIDR Notation: 172.16.0.0/16)
- 192.168.0.0–192.168.255.255 (CIDR Notation: 192.168.0.0/16)

# Protocol Headers

RFC (Request For Comments) documents provide detailed information on the implementation of TCP/IP protocols. These documents contain protocol header information, a few examples of which are listed here.

# IP (Internet Protocol) Header

The following represents the layout of the IP header. The digits on the top of the header represent a byte each.
