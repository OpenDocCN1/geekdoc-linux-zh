HPFS, NTFS, and DFS.

+   - The Microsoft *Distributed File System (DFS)* provides a means of organizing directory shares on multiple computers into a single directory tree.
+   - Print devices with an associated printer driver are represented as virtual printer objects and referenced by a queue name.
+   - Multiple physical print devices, called a *printer pool*, may be referenced by a single queue name.
+   - The *Local Security Authority (LSA)* and Net Login service are responsible for verifying access rights to resources and authenticating login requests respectively.
+   - Resource permissions are definedby *Access Control Lists (ACLs)*.
+   - Windows 2000 enhances the SAM/LSA mechanism by integrating Kerberos 5.0 for network authentication.

# Chapter 4: Samba Overview

# Overview

*Samba is a Portuguese word meaning a rhythm and a dance and is derived from the West African Bantu language term semba, meaning to pray or invoke the spirits of ancestors. As a Bantu verb semba means "to cry" or "the blues." In Brazil, a Samba is a woman who is a sacred dancer.*

In the world of UNIX, "Samba" is a software suite for remotely sharing UNIX files and printers with networked PCs via the *Server Message Block (SMB)* protocol. SMB is a NetBIOS-based protocol traditionally used in LAN Manager, Windows, and OS/2 networks for accessing remote files and printers, collectively known as *shares* (see Chapter 3). SMB provides a seamless interface between network resources and desktop applications that is often more tightly integrated and transparent than commonly used alternatives like PC-NFS, FTP, and LPR. Samba is a UNIX implementation of SMB-over-TCP/IP (NBT, see RFC 1001 and RFC 1002). From a Windows or LAN Manager desktop perspective, Samba-shared UNIX resources appear just as if they were residing on another Windows or LAN Manager server. No special desktop client software is required. Source code and binary distributions are free to anyone interested in the product. We will cover Samba distribution sites in the next chapter.