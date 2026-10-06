
# Chapter 26: Running a Printer Server 713

The example settings are the result of configuring Samba from the Samba Server Configuration window in Fedora Linux. The lines show that printers from /etc/printcap were loaded and the CUPS service is being used. Password encryption is on, and the /etc/samba/smpasswd file stores the encrypted passwords. Because password sync is on, each user's Samba password is synchronized with the user's local UNIX password.

The last few lines are the actual printers' definition. It shows that users can print to all printers (printable=yes).

## Setting Up SMB Clients

Chances are good if you are configuring a Samba printer on your Linux computer, you want to share it with Windows clients. If Samba is set up properly on your computer and the client computers can reach you over your network, finding and using your printer should be straightforward.

The first place a client looks for your shared Samba printer is in Network Neighborhood (or My Places, for Windows 2000). From the Windows 9x desktop, double-click the Network Neighborhood icon. From Windows 2000 or XP, double-click the My Network Places icon. The name of your host computer (the NetBIOS name, which is your TCP/IP name) appears on the screen or within a workgroup folder of the screen. The icon that represents your computer shows your shared printers and folders.

If your computer's icon doesn't appear in Network Neighborhood or My Network Places, try using the Search window. From Windows XP, choose Start ⮕ Search ⮕ Computer or People A Window on the Network. Type your computer's name into the Computer Name box and click search. Double-click your computer in the search results panel. A window displaying the shared printers and folders from your computer appears (see Figure 26-4).

![](img/a2d958d7eab32ca5b89b2b8af808aa70_744_0.png)

Figure 26-4: You can search for your computer's printers.

After your shared printer appears in the window, configure a pointer to that by opening (double-clicking) the printer icon. A message tells you that you must set up the printer before you can use it. Click Yes to proceed to configure the printer for local use. The Add Printer Wizard appears. Answer the questions that ask you how you intend to use the printer, and add the appropriate drivers. When you are done, the printer appears in your printer window.

Another way to configure an SMB printer from a Windows XP operating system is to go to Start ➔ Printers and Faxes. In the Printers and Faxes window that appears, click the Add Printer icon in the upper-left portion of the window, and then select Network Printer from the first window. From there you can browse and configure your SMB printer.

## Summary

Providing networked printing services is an essential efficiency on today's business network. With the use of a few network-attached devices, you can focus your printer spending on a few high-quality devices that multiple users can share numerous lower-cost devices. In addition, a centrally located printer can make it easier to maintain the printer, while still enabling everyone to get his or her printing jobs done.

The default printing service in nearly every major Linux distribution today is the Common UNIX Printing Service (CUPS). Any Linux system that includes CUPS offers the CUPS Web-based administrative interface for configuring CUPS printing. It also offers configuration files in the `/etc/cups` directory for configuring printers and the CUPS service (cups daemon).

In Fedora and other Red Hat Linux systems, you can configure your printer with the Printer Configuration windows available in both K Desktop and GNOME environments. A variety of filters makes it possible to print different kinds of printers, as well as printers that are connected to computers on the network.

You can set up your computer as a Linux print server, and you can also have your computer emulate an SMB (Windows) print server. After your network is configured properly and a local printer is installed, sharing that printer over the network as a UNIX or SMB print server is not very complicated.

# Running a File Server

## In This Chapter

Most networked computers are on the network in the first place so that users can share information. Some users need to collectively edit documents for a project, share access to spreadsheets and forms used in the daily operation of a company, or perform any similar file-sharing activities. It can also be efficient for groups of people on a computer network to share common applications and directions of information needed to do their jobs. By far the best way to accomplish the centralized sharing of data is through a file server.

A centralized file server can be backed up, preserving all stored data in one swoop. It can focus on the tasks of getting files to users, rather than running applications that use client resources. A centralized file server can be used to control access to information—security settings can dictate who can access what.

Linux systems include support for each of the most common file server protocols in use today. Among the most common file server types used are the Network File System (NFS), which has always been the file-sharing protocol of choice for Linux and other UNIX systems, and Samba (SMB protocol), which is often used by networks with Windows and OS/2 computers.

This chapter describes how to set up file servers and clients associated with NFS and Samba.

When selecting file services to provide, keep in mind that less is more. If your clients and servers support multiple file access capabilities (both NFS and SMB, for example), pick the service that lends itself to making the task complicated. In many cases, NFS is supported by clients and servers regardless of the operating system they use. It’s rare that you would need to enable more than one of the file services discussed in this chapter.

## Setting Up an NFS File Server

Instead of representing storage devices as drive letters (A, B, C, and so on, as they are in Microsoft operating systems, Linux systems connect file systems with hard disks, floppy disks, CD-ROMs, and other local devices to form a single file system. The Network File System (NFS) facility enables you to extend your Linux file system to connect file systems on other computers.

An NFS file server provides an easy way to share large amounts of data among the users and computers. An administrator of a Linux system that is configured to share its file systems with NFS has to perform the following tasks to set up NFS:

- Set up the network. If a LAN or other network link is already connecting the computers on which you want to use NFS, you have the network you need.
- Choose what to share on the server. Decide which file systems on your Linux server to make available to other computers. You can choose any point in the file system and make all files and directories below that point accessible to other computers.
- Set up the security on the server. You can use several different security features to suit the level of security with you are comfortable. Mount-security restricts the computers that can mount it, lets specify whether it can be mounted read/write or read-only. With your user-level security, you can manage permissions from the client systems to the NFS server so that they can rely on standard Linux read/write/execute permissions, file ownership, and group permissions to access and protect files. Linux systems that support Security Enhanced Linux (SELinux) offer other means of restricting or sharing NFS file directories.
- Mount the file system on the client. Each client that allowed access to the server's NFS shared file system can mount anywhere the client chooses. For example, you may mount a file system from a computer called maple on the /mnt/maple directory in your local file system. After it is mounted, you can view the contents of that directory by typing ls /mnt/maple.

Figure 27-1 illustrates a Linux file server using NFS to share (export) a file system and a client computer mounting the file system to make it available to its local users.
