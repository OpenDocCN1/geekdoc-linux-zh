
![](img/840007e8f98ea6653e5877e945c27dc6_45_0.png)

**Figure 1-13** An Active Directory forest

Users log in to a forest, which allows them to access any shared resources on the servers in that forest they have been given right to. Some differences between Active Directory and eDirectory include the following:

- Active Directory allows Windows client computers using Windows XP or Windows 2000 Professional to be members of Active Directory. Being a member of Active Directory allows users to log on to the domain and makes it possible for administrative users to manage client computer data and configuration from a centralized site.
- Active Directory is a proprietary system that doesn't run on other OSs except Windows 2000 Server and Windows Server 2003.
- Active Directory requires servers to be upgraded to domain controllers to store a copy of the domain database, which is a more complex process than adding a partition to a Novell eDirectory server. After a server has been promoted to a domain controller, it can't be renamed. Removing the Active Directory database requires demoting the server to a member server.
- Active Directory relies on the use of DNS to find domain controllers.

## Novell NetWare

Novell NetWare has been a leader in microcomputer-based NOSs, starting with NetWare 2 in the early 1980s. Because Novell was not in the business of producing desktop operating systems and application software, NetWare was designed from early versions to integrate with different desktop systems. NetWare has a proven history in providing high-speed, reliable, and secure network operating system environments for file and printer sharing. Today, Novell offers a wide range of NOS products and services that help organizations implement secure, high-speed network systems in a variety of client environments. In this section, you learn about the major versions of NetWare and the latest product features.

## NetWare Versions

Although NetWare 6.5 is now Novell's flagship NOS, earlier versions of NetWare are highly stable network platforms that network administrators still depend on for consistent performance.

The primary difference between NetWare 3.0 and later versions is the introduction of Novell Directory Services (NDS), which was upgraded in NetWare 6.0 to become eDirectory. Both NetWare 2.0 and NetWare 3.0 had a flat database, called the binder, that stored information about network objects, such as users, groups, and printers. A separate binary database was stored on each NetWare 2.0 or 3.0 server, requiring users to have an account on every server containing resources they needed to access. Although the binary system worked well in networks of one or two servers, when networks began to include a dozen or more servers and hundreds of users, maintaining user accounts on multiple servers became a bottleneck for administration. With the binder, users had to log in to each server because the binder database was not shared among servers.

NetWare 3.0 was server-centric, meaning each server managed its network objects individually. NetWare 4.0 and later are network-centric, meaning that all network objects are stored and administered through a centralized directory database system (NDS, later called eDirectory). Following is a brief summary of some important enhancements in NetWare versions.

Features introduced with NetWare 4.0 include the following:

- Novell Directory Services (NDS) is an immensely scalable directory service that can support more than a million objects on the network. NDS is shared among all servers, so users logging in can do so from any computer and be recognized.
- NetWare Administrator, a Windows graphical administration utility, is the network administrator's main tool for managing the network; the enhancements include a Windows version, a configurable toolbar, and the capability to manage multiple networks simultaneously.
- NetWare Client 32 is a client software product that integrates with Windows 98 through XP and provides enhanced access to network services, including printing, application management, and administration.

Features introduced with NetWare 5.0 include the following:

- The ConsoleOne administrative tool is a Java-based utility that performs most administrative functions from a variety of OS environments, including Windows, the NetWare server console, and Linux systems.
- X Windows GUI server console interface enables administrators to run GUI-based server applications, including ConsoleOne.
- Novell Distributed Print Services (NDPS) allows network-attached printers to be shared and managed using Novell Client or the Internet Printing Protocol (IPP). In Chapter 8, you learn how to use NDPS to set up shared printers on a network.
- TCP/IP is the default protocol for communications to the NetWare services. Previously, the SPX/IPX protocol was necessary to communicate with NetWare services.
- Novell Storage Services (enhances volume and disk management) are available for user data volumes only.

New features of NetWare 6.0 include the following:

- The One:Net strategy to make data access and network administration independent of computer operating systems and network configurations
- New One:Net administrative utilities, such as iManager, Remote Manager, and iMonitor, that enable administrators to manage the network through a Web browser, independent of client OSs or network configuration
- Provides the following OneNet tools to enable users to access data via a Web browser, independent of client OSs or network configuration:
  - NetStorage Service, which allows access to network files from remote locations using a Web browser
  - iFolder service, which enables mobile computers to synchronize files with a central server automatically
  - Native File Access Protocol, which allows non-Novell clients to access a NetWare server's shared directories and files
- Internet Printing Protocol, which makes it possible to use and manage network printers across the Internet

The NetWare 6.5 network operating system includes all the features of NetWare 6.0 plus the following new features:

- Upgraded version of the iManager utility that enables network administrators to perform most administrative tasks, such as creating users and groups, through a Web browser
- Virtual Office client environment that makes it easier for users to access and use NetWare services
- New pattern-based installation options that enable you to create specialized and task-oriented servers, such as a server that's specialized to support Web applications
- New open-source development tools to help programmers develop applications without the cost of proprietary software development tools

## Novell Open Enterprise Server

Open Enterprise Server is Novell's latest version of the NetWare 6.5 NOS combined with SUSE Linux 10. Enhancements released with Open Enterprise Server include the following:

- NetWare 6.5 operating system
- SUSE Linux 10 (described in the following section)
- Enterprise Services for Linux that enable the SUSE Linux 10 server to use Novell's eDirectory service and other Novell services, including iFolder, iPrint, NetStorage, and Virtual Office

The features of Novell Open Enterprise Server are discussed in more depth in subsequent chapters. The many added improvements, the acknowledged stability, and the increased need for Internet services in the industry will lead many organizations to upgrade their NetWare servers to Open Enterprise Server's NetWare 6.5. In Chapter 2, you learn how to install NetWare 6.5 on your computer.

## Novell SUSE Linux 10

The Linux OS is based on UNIX and was first developed in the early 1990s at the University of Helsinki in Finland by a student named Linus Torvalds. Torvalds studied a freeware version of UNIX called Minix and used his knowledge to develop a new OS he named "Linux." UNIX was developed for use on large-scale computers, but Linux was designed for use on microcomputer-based systems. Because Linux was developed under the General Public License (GPL), the source code is freely available, so developers can modify the Linux system to meet their needs.

Linux is proving to be a viable enterprise-wide NOS that can help organizations reduce costs yet still provide robust and secure network services. As a result of this track record, there's a growing demand for Linux in almost every area of the IT industry, including Web servers, e-mail servers, application servers, and user desktops. To meet the growing demand for Linux services and support, Novell and other leading vendors are bringing many new services and support to the Linux environment. In Chapter 14, you learn about the growing demand for Linux and how Novell is helping meet these demands by providing services, support, and certification.
