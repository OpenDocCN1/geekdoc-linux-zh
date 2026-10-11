
# Samba Security

This is the third chapter that discusses security at the application layer. This chapter focuses on a well-known network application that makes files on Linux servers available to Windows clients: Samba. As the Linux operating system continues to make inroads in the Microsoft-dominated world of local area file servers, it’s important to offer an alternative that can leverage the robustness and security of a Linux server, and at the same time offer file services to the ever-ubiquitous Windows desktop.

The Samba software addresses this need by providing a Linux-based server application capable of sharing files and printers transparently with Windows clients, using the Server Message Block (SMB) and NetBIOS protocols. Along with electronic mail and Web services, Samba is part of the essential suite of applications found in most Linux-based network installations.

Files are the most fundamental view of data stored on any server, and as such, they are the main targets of intruders looking for inside information. You need to ensure the availability and accessibility of these files to your users, while enforcing access controls via authentication and authorization. The good news is that Samba was first released in 1992, a year during which security was already a hot topic of discussion among designers of network applications. As such, Samba offers configuration parameters that allow the network administrator to easily control host and user authentication, access control, and the privacy of the file-sharing communication.

This chapter starts off by looking at the origins of the Samba server. It then goes on to describe a typical Samba installation procedure, including detailed information about the configuration parameters that directly affect the security of your server. Finally, this chapter explains how to add Secure Socket Layer (SSL) support to the standard Samba package, and it closes the discussion by looking at Samba’s ability to operate as a primary domain controller (PDC) in a Windows NT environment.

## The Samba Server

Samba is a full-featured implementation of a Server Message Block (SMB) server, which can offer transparent file services to Windows (95, 98, NT, 2000) clients, as well as to OS/2 clients. The brain child of LinuxCare’s Andrew Tridgell back in 1992, Samba is now widely used and updated with help from programmers from all over the world.

Samba allows network administrators to use a Linux server’s ability to store and manage a large number of files, while still preserving the use of Windows-based desktop clients. In addition to file services, Samba offers the following features:

- Print services, by making a Linux-controlled printer available from Windows desktops as a standard network printer
- Authentication and authorization services, where access to network shares is granted only after the appropriate username and password is provided
- Name resolution, by mapping network share (NetBIOS) names into standard IP addresses
- The ability to announce its existence in a “browse” list

Samba’s popularity stems from the fact that Linux shares are viewed on a Windows client exactly as other Windows-based drives and printers are viewed, which makes the fact that Linux is being used totally transparent to the end user.

Another selling feature of Samba is its performance. Independent tests have shown that, as of version 2, the Samba server is nearly twice as fast as an equivalent Windows NT 4.0 server using the same hardware.

Samba is an implementation of IBM’s Network Basic Input Output System (NetBIOS) protocol, which runs over TCP in order to traverse IP routers and to extend the reach of NetBIOS beyond the LAN environment for which it was originally designed. The SMB blocks are transported inside NetBIOS data units, which make up the payload of the TCP packet. Figure 8.1 illustrates the composition of a typical SMB packet, starting with the data link layer at the bottom (Ethernet), and going up the stack with the IP, TCP, and NetBIOS layers.

### Figure 8.1 Samba's SMB transport over NetBIOS

| Layer | Protocol |
| :--- | :--- |
| Application | SMB |
| Presentation | |
| Session | NetBIOS |
| Transport | TCP / UDP |
| Network | IP |
| Data Link | Ethernet |

The original Microsoft LAN Manager implementation of file and printer sharing over a local area network did not use NetBIOS or TCP/IP as the underlying protocol. Instead, it used the special-purpose NetBEUI (NetBIOS Extended User Interface) protocol for this purpose (see Figure 8.2). The NetBEUI protocol makes up the network, transport, and session OSI layers. Due to NetBEUI's lack of WAN-routing abilities, the original LAN Manager implementation was not able to share files and printers over the Internet, just over the local network. This essentially eliminated security as a concern, but reduced its usefulness, since you couldn't share resources with remote offices connected via routed IP networks.

### Figure 8.2 LAN Manager's SMB transport over NetBEUI

| Layer | Protocol |
| :--- | :--- |
| Application | SMB |
| Presentation | |
| Session | |
| Transport | NetBEUI |
| Network | |
| Data Link | Ethernet |

Samba is offered under GNU’s General Public License (GPL), which allows for the free use and distribution of the package, as long as the full source code is also made available.

This section of the book shows you how to install and configure the Samba server with security in mind. For a complete reference on the installation, configuration, and administration of the Samba server on a Linux server, please refer to *Linux Samba Server Administration*, by Roderick Smith (Sybex, 2000), part of the Craig Hunt Linux Library series.

The Samba home page (Figure 8.3) contains valuable information about the ongoing development of Samba. It includes the following information:

- News about the latest Samba release
- Resources for Samba developers
- Documentation, including the latest books on Samba
- Downloads of Samba source code for various operating system platforms
- Downloads of plug-ins for your Samba server
- Downloads and information about several graphical user interfaces (GUIs) that can simplify the configuration and management of your Samba server
- Information about Samba-related mailing lists

To get to the Samba home page, go to www.samba.org and choose the Web mirror site closest to your geographic location.

![](img/3258bbaf790525f8c4eb25fabff7844a_236_0.png)

## Installing Samba

Most recent Linux distributions include the Samba server right out of the box. Here's how you can make sure Samba is installed on Red Hat 7.0:

```bash
[ramon]$ rpm -q samba samba-common
samba-2.0.7-21ss1
samba-common-2.0.7-21ss1
```

Two packages make up a complete Samba installation:

- **samba-2.0.7-21ss1**: This is the base Samba server package and it includes the following files:
    - Server executable
    - Startup scripts
    - Manual pages
    - Text and HTML documentation
    - Samba Web Administration Tool (SWAT)
- **samba-common-2.0.7-21ss1**: This is the set of utilities and configuration files that are common to both the server and the client and that need to be installed to provide the service. This package includes the Samba codepages, the `smb.conf` configuration file, and several utilities to test the configuration before the server goes in production.

> **NOTE** A Samba codepage definition file is a description that tells Samba how to map from uppercase to lowercase for characters greater than ASCII 127 in the specified DOS codepage.

If you are not running the latest version of these two packages, you can download them from your favorite repository. I recommend that you use a reputable, well-known archive such as www.rpmfind.net to minimize the risk that legitimate packages are replaced by Trojan horses.

Once you have obtained the RPM packages, install them using the following commands:

```bash
[ramon]$ sudo rpm -U samba-2.0.7-21ss1-i386.rpm
[ramon]$ sudo rpm -U samba-common-2.0.7-21ss1-i386.rpm
```
