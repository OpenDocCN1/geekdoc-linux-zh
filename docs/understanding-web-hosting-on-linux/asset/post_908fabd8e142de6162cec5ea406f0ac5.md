
IBM (www.ibm.com/linux), which spent $1 billion on Linux development in 2001 alone. IBM can work with any size company and provides Internet and voice technical support 24 hours a day, seven days a week.

## Stability

Two other questions need to be answered before IT directors agree to deploy a Web site on a new platform:

- 1. Is the platform stable?
- 2. Is the platform secure?

A company that expects to derive revenues from a Web site can't have revenue disrupted. Even if the Web server goes down for a short time, the Web loses credibility, and customers might opt to click over to a competitive site to purchase the product.

UNIX systems in general are highly stable, and Linux platforms have been known to run for years without crashing. One of the authors of this book, as the systems manager for a large OS/400 shop, installed Linux on an outdated Intel 486 machine to provide a Domain Name Service for his OS/400-managed network (before OS/400 provided a DNS product). The system ran uninterrupted for over a year before its disk crashed. Linux was simply moved to another outdated machine, and the DNS server is still running today.

Windows administrators will tell you that the most stable way to run an NT network is to use one machine per server to avoid crashes. In contrast, one Linux server can host all the TCP/IP services required for a network and a Web site without conflicts. More recent versions of Windows are much stable than NT, but it seems a little late for Microsoft to come with stable operating systems. This is especially true when you consider that in 1994, when Windows 3.1 was the best system offered by Microsoft, Linux users were exploiting the full multitasking, 32-bit, virtual memory capacities of processors.

There is no need to compare Linux's stability with other UNIX systems because they all benefit from UNIX technologies, so they all have comparable stability ratings. However, Linux is not as stable as IBM's OS/400 or iSeries/390 operating systems. The question of whether to use OS/400 or 390 to host your Web site, is not a question of stability, but of technical support. There are far more networking experts available for Linux than for OS/400 and S/390, and the number of Linux experts is growing every day.

## Security

Many layers of security need to be in place for a Web site. Internet users must go through these layers to get to the application software and data files. One of the first layers of security, known as a firewall, is designed to block destructive attempts to enter an area. Firewall does such things as exclude users who attempt to access a machine using well-known entry points like File Transfer Protocol (FTP) and terminal emulation (telnet). On most operating systems, firewall software must be properly secured, installed and configured. Linux has an integrated firewall.

Most operating systems use user profiles set up, so that a person cannot access a platform without entering a user name and password. Linux has a robust security mechanism, where users are added to the system by a network administrator. The administrator assigns an initial password for the user (which can be later by the user). Even after the user is logged into the system, Linux has another level of security: file-level security.

Each file on the Linux machine is qualified to be accessed by three types of users: owner, group, and user. The owner profile associated with a file is typically that of the user who created the file (although this can be changed). The group profile associated with a file is that of a namelist set to simplify application security into groups of users. The user profile, which is not special like owner or group, basically means everybody other than the file and the namelist associated with the group profile.

Permissions to read, write, and execute a file are assigned for each of these three user types. For instance, a Web page stated as a text-based HTML file on disk might have the name Denouncourt and the name webpmgr assigned to it. The group and read have write and privileges assigned, while the user has only read privileges. If a user not in the group of programmers attempts to modify or delete that file (maliciously or otherwise), the attempt will fail.

There is one other special security level known as the root user. The system administrator (and his backup) should know, and use the root password because someone logged into that profile can do absolutely anything with the system.

Many other operating systems have similar file- or object-level security, but Linux has something that no other operating system can boast: daily kernel updates with security bug fixes. Because the complete source for Linux is available to all users, when a security breach is found, anybody with the appropriate technical skill can fix that breach and make that available to the Linux community.

In the Torrent of crackers, there's a big philosophical difference between cracking open-source Linux code and cracking closed-source code like Windows. The crackers tend to fix the breaches discovered in Linux and publish those fixes, while with Windows, they simply publish how they cracked the system. After all, they can fix (Windows—they don't have the code. Plus, some crackers resent Microsoft's dominant position in the market, preferring the freedom associated with Linux. They are truly, then, for more developers working improving Linux security than Microsoft working on its system. As a result, Linux security fixes are published daily.

## Linux Software

The wide variety of software for Linux can be divided into two groups: open-source and commercial. The various Linux distributions bundle many of the open-source products on their installation CDs. They even have options during the installation process to load the various products. We've already introduced sendmail, the Apache Web server, and Apache's Tomcat Web application server, but there are...

## Why Linux 9

... (text continues from previous pages) ...
