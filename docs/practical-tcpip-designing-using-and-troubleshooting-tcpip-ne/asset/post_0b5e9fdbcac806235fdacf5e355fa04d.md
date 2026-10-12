
Syslog can collect a huge amount of information, and to make the most of it you need some form of automatic processing, e.g. to raise an alert when a particular warning message occurs, or a specific type of event is logged. An easily configured tool of this type is **Xlogmaster**:

- http://www.gnu.org/software/xlogmaster/

While this is still available for download, it's not being developed further. Even so, it's very useful as it stands. A Windows version of the *syslog* server, with extra analysis features, is produced by:

- http://www.kiwi-enterprises.com

This is commercial software, but they also make a free version available.

Other log analysis tools:

- http://www.cert.dfni.de/eng/logsurfl Logsurfer Homepage
- http://www.counterpane.com/log-analysis.html Log Analysis Resources
- http://www.oit.ucsb.edu/~eta/swatchl SWATCH: The Simple WATCHer
- http://www.psionic.com/products/logsentry.html LogSentry (formerly Logcheck)

# Ipr

- RFC-1179 August 1990 Line Printer Daemon Protocol

Ipr is the standard printing system on Linux. It's also available on Windows-NT as the Microsoft TCP/IP Printing network service.

# NTP

The standards for NTP are:

- RFC-1305 March 1992 Network Time Protocol (Version 3) Specification, Implementation and Analysis

Some of the diagrams and tables are messed up in that text version. A more readable version is

- ftp://ftp.isi.edu/in-notes/rfc1305.pdf

A lighter-weight version of NTP, suitable for less demanding applications, is called *SNTP* (Simple Network Time Protocol), described in:

- RFC-2030 October 1996 Simple Network Time Protocol (SNTP) Version 4 for IPv4, IPv6 and OSI

Most of the work on NTP has been done by David Mills at the University of Delaware:

- http://www.eecs.udel.edu/~mills/database/brief/overview/overview.htm
- http://www.ntp.org

Alas, we find much of the documentation on NTP incomprehensible and have never come across a good tutorial or overview. However the above overview is reasonably understandable.

To find NTP servers that you're allowed use, ask your ISP or see http://www.ntp.org.

For other time-related information, including some live-time displays, see:

- http://tycho.usno.navy.mil Time Service Department U.S. Naval Observatory The Official Source of Time for the Department of Defense and the Standard of Time for the United States

For Windows systems only, you can synchronize one machine with another (masterbox, say) using the net time command. On the "client", enter the command

```
net time \\masterbox /set /yes
```

# NFS

The original RFC describing NFS gives some interesting background on its design:

- RFC-1094 March 1989 NFS: Network File System Protocol Specification
- RFC-3010 December 2000 NFS version 4 Protocol

For filehandles as a security hazard see the book:

- William Cheswick and Steven Bellovin Firewalls and Internet Security: Repelling the Wily Hacker (1994, Addison-Wesley)

To allow files to be updated in a controlled way, they must be "locked" while they are being updated. NFS uses the "NFS lock manager" server, usually called lockd or rpc.lockd to handle this.

NFS has been ported to a wide range of machines and operating systems, and around 1990 it was the way to share files and data across a heterogeneous network. On UNIX/Linux-only networks, NFS is still the shared file system of choice. However, to share files between Linux/UNIX and Windows, a free, and excellent, alternative is Samba (Module 22.4).

# Appendices

- Appendix 19: nc (netcat) manual page in full
- Appendix 20: controlling network services
- Web Appendix 22: the RPC portmapper service

# Part 3

# Microsoft Windows Networking on a TCP/IP network

# Introduction

Most real-world networks contain Microsoft Windows machines, and increasingly they contain Linux and UNIX machines too. Windows Networking is very different to the TCP/IP networking we've covered so far. It was developed separately and uses its own protocols and mechanisms, layered on top of and separate from TCP/IP, for much of its basic operation, including:

- 1. name resolution
- 2. logon and user authentication
- 3. “browsing” the network to automatically find lists of available machines and resources.

The challenge is to make these two very different worlds operate well on the same network, and to apply to Windows Networking the same investigative and diagnostic approach we've used for everything else.

In the five chapters in this part of the book, we give an overview of the major architectural features of Windows Networking, then cover in detail name resolution, authentication, and browsing, and finish off with a brief chapter on using Windows Networking in practice.

![](img/a2132b646d336d5f9a21102d6320e537_494_0.png)

# 18 MS-Windows Networking – introduction

- 18.1 An overview of Microsoft Windows Networking
- 18.2 Microsoft Windows Networking – architecture
- 18.3 Windows Networking implementation
- 18.4 Windows Networking implementation over TCP/IP
- 18.5 Windows Networking implementation – NT Services
- 18.6 Lab – the Windows Network Monitor, overview
- 18.7 Lab – Network Monitor – capture filter by protocol
- 18.8 Lab – Network Monitor – capture filter by address
- 18.9 Lab – Network Monitor – display filters
- 18.10 Windows Network Monitor – tips and tricks
- Summary

# Introduction

This chapter introduces Microsoft Windows Networking. Windows Networking was developed separately from TCP/IP, running on different network systems, and only relatively recently was it made to run over TCP/IP too. Consequently it’s architecture and how it’s implemented differ greatly from the “real” Internet protocols that we’ve seen elsewhere in the book. We also cover the Windows Network Monitor, a packet sniffer that’s very similar to *ethereal* and that comes as standard on NT.

![](img/a2132b646d336d5f9a21102d6320e537_496_0.png)

# 18.1 An overview of Microsoft Windows Networking

Microsoft Windows Networking is a specific set of protocols that Windows computers (and some others) use to share resources on a LAN or a WAN. It was developed in the early days of networking with the aim of making it easy for a small “workgroup” of users to:

- find out what resources (printers, file servers) are available on the network, by allowing users to “browse the network”
- share files and printers
- make all this happen without any pre-configuration or dedicated servers.

You should be able to install Windows on a PC and as soon as you connect it to the LAN the sharing mechanisms should work automatically. You don’t have to configure dedicated file servers: my desktop PC can share files with your desktop. The PCs on the LAN share resources as a *peer-to-peer network*, although with the advent of NT, dedicated file servers and a client/server oriented network architecture are used very widely.

# Windows Networking is different from other Internet protocols

Microsoft Windows Networking is a whole separate world from the other network protocols that we deal with in this book:

- it was originally developed on top of other network systems long before TCP/IP became dominant. It was made to run over TCP/IP afterwards
- it was developed commercially, without the wide exposure to comment, criticism, and improvement that is a feature of the Internet and its RFCs

Because it grew up in this self-contained way, separately from the “real” Internet protocols that evolved together on the Internet in a fairly consistent fashion, it has significant differences from TCP/IP:

- it doesn’t use different ports for different network operations; instead, almost everything works over ports 137, 138, and 139. As we’ll see, this makes deciphering what’s happening on the wire much more difficult
- names not IP numbers, are the primary reference for resources. This isn’t too surprising when you recall that Microsoft Windows Networking can operate over non-IP networks where there just aren’t any IP numbers
- it is still used over other, non-TCP/IP networks and therefore can’t rely on TCP/IP components, even when it’s running over TCP/IP. For example, to resolve names, Windows Networking can’t rely on DNS – it has to use some mechanism that works on non-TCP/IP networks too. (However, DNS is mandatory for Active Directory; Windows-2000 networking is now starting to abandon the non-TCP/IP networking systems!)
- documentation that describes how the Microsoft Windows Networking protocols evolved in the way they did, can be very hard to find. Very detailed system descriptions are almost non-existent. (Because of this we’ve included more detail in the chapters in this part of the book than we would otherwise have done, to make the information more accessible.)
