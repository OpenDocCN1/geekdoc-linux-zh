
## What Is NNLS?

Since the 1980s, Novell has been *the* leader in the network operating system (NOS) industry. In the early days, this leadership was established with the NetWare OS, which provided mainly file and print services on local area networks (LANs). Prior to this time, these types of services were provided mostly by expensive Unix systems.

Novell took the innovative approach of creating an NOS that ran on the x86 Intel CPU. This allowed businesses to provide file and print services using relatively inexpensive server hardware. In fact, you didn't even need to buy server hardware; you could grab any desktop system with a networking board and install NetWare on it. NetWare was such an efficient operating system that you could get reasonable performance from off-the-shelf desktop systems. Even today, you may run into an organization, from time to time, that still has a NetWare server running on an old 80486 system.

There was, however, one glaring problem in the early days of NetWare. User accounts were local to each server. If your organization only implemented one server, this wasn't a problem. It was, however, a serious impediment for larger institutions that may have hundreds of servers. To use the services provided by a particular server, you had to have a user account on that server.

That doesn't sound too bad on a small scale, but imagine the administrative nightmare associated with a company that has thousands of users and hundreds of servers. In that world, you had to manage duplicate user accounts, passwords, and rights on multiple servers.

Believe me, it could become very cumbersome. The first network administration job I had back in the early 1990s involved this very situation. My organization had four LANs connected by routers; each was serviced by its own NetWare 3.1 server. That doesn't sound too bad, but I also had over a thousand users who needed access to each server. Maintaining consistent user accounts and passwords was difficult.

It was also difficult for the end users. If they were logged in to one particular server, but then needed to access files they had saved in their home directory on a different server or print to a printer serviced by a different server, they had to reauthenticate to each one.

> Linux/Unix systems still face a similar quandary today. Many administrators use the Linux Network Information Service (NIS) to eliminate the need to maintain duplicate user accounts. For more information on NIS, visit http://www.linux-nis.org/.

Novell revolutionized the industry in the mid 1990s when it introduced Novell Directory Services (now called eDirectory) for the NetWare platform. Directory Services provided a directory tree that contained all user accounts, servers, printers, and other network resources.

Each user had only one user account in the tree and was granted rights to other network resources. With Directory Services, administrators only had to worry about a single user account for each user. In addition, users only had to authenticate once to use network resources.

In the late 1990s and early 2000s, Novell enhanced NetWare by providing a number of directory-enabled products and services that significantly enhanced end users' productivity. These included products such as iFolder, iPrint, Native File Access Protocol (NFAP), NetDrive, NetStorage, eGuide, GroupWise, ZENworks, Virtual Office, and NetMail.

If you've ever used any of these services, you know how powerful they are. Users can access their work files from home using only a dial-up connection and a web browser. They can use a web-based interface to select the printer they want to print to and have it automatically download the correct drivers to their workstation.

Users can also use eGuide to view company contact information in a web browser and send email messages.

In 2003, Novell once again made an innovative move and began porting these services to run on the Linux platform as well as its venerable NetWare operating system. This is all part of Novell's oneNet strategy, announced in 1999.

> Ever since oneNet was announced, everyone keeps asking, “Does this mean Novell is getting rid of NetWare?” According to the latest Novell press releases posted at the time this book was written, Novell plans to continue to develop NetWare. This only makes sense because Novell has a very large installed NetWare base. Porting its most popular services over to Linux serves to broaden the potential installed base. As you will see later in this book, a Linux server with NNLS installed can be configured to work with NetWare servers in the same eDirectory tree.

One of the main goals of the oneNet strategy is to make network services available to users no matter where they are. If an executive is preparing a presentation in a remote city, she should be able to access her company's network resources from her hotel room as if she were back at her desk.

If a user is at home in the evening and receives an emergency request for information, he shouldn't have to drive back to work. He should be able to access network resources from home and complete the assignment from there.

The oneNet strategy is composed of the following services and products:

- **Novell Nterprise**—A key component of the oneNet strategy is the Nterpise product line. These products, of which NNLS is a part, provide the services discussed earlier that supply “anywhere” access to an organization's network resources.
- **Novell Nsure**—The Nsure family is composed of products that provide identity security management services.
- **Novell exteNd**—Novell's exteNd product line provides a development platform for web-based applications.
- **Novell Ngage**—Novell also provides Ngage consulting and training services to deploy oneNet products.

As we work through the remaining chapters in this book, you will see how NNLS on Linux fits the goals of Novell's oneNet strategy.

## NNLS Components

**Test Objective Covered:**

- Describe Novell Nterpise Linux Services (NNLS).

Let's now turn to a discussion of the individual components included in NNLS to provide these services. Before doing so, you need to know that NNLS 1.0 isn't currently supported on all Linux distributions. The distributions that are supported include the following:

- Red Hat Enterprise Linux AS 2.1
- Red Hat Enterprise Linux ES 2.1
- SUSE Linux Enterprise Server 8

The fact that NNLS isn't supported for a particular distribution doesn't necessarily mean that it isn't compatible. I've found that it runs very well on Red Hat 7.3, Red Hat 9, and SUSE 8.2. I have experienced problems, however, when installing on Red Hat 8.

If you have a particular distribution you are partial to, feel free to give NNLS a try on it. Be aware, however, that if you experience a problem and try to call Novell's Technical Support number, you will be told to install NNLS only on a supported distribution.

The individual components that comprise NNLS are discussed in the following sections.

### Identity Management

To manage your network and keep it secure, NNLS provides eDirectory 8.7.3 for your Linux server. As mentioned earlier, eDirectory is the latest version of Novell Directory Services (NDS). With eDirectory, you can assign rights that control the level of access individual users have to network resources.

> Unlike many other network operating systems, eDirectory is extremely difficult to hack into. If you read the various hacker websites, you'll see that to hack eDirectory, you have to get an actual copy of the eDirectory database files. This is not any easy thing to do without having physical access to the server hardware.

NNLS also includes eGuide 2.12. eGuide is a web-based application that allows you to query any LDAP-compliant database and display the resulting information. eGuide is most frequently implemented with eDirectory to create a web-based organization directory of users and resources.

In addition to these two products, NNLS includes the Starter Pack version of the powerful Novell DirXML product. DirXML can synchronize your eDirectory database with other directory services and databases, such as Windows NT Domains and Active Directory. It can even be used to synchronize your eDirectory database with another eDirectory database.

DirXML is frequently implemented such that eDirectory is configured as the central, authoritative source for network information. When you make a change in eDirectory, such as creating a new user, DirXML replicates the change in the synchronized application.

NNLS also includes the Linux User Management 2.1 (LUM) product. LUM is a powerful service that allows you to redirect authentication from the standard Linux authentication mechanisms to eDirectory.
