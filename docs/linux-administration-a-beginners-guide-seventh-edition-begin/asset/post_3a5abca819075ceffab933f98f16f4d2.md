
# Summary

This chapter discussed the process of compiling, installing, and configuring Samba so that your Linux-based server can integrate with a Windows-based network. Samba is a powerful tool with the potential to replace Microsoft Windows servers dedicated to file and printer sharing and authentication services.

Reading through tons of documentation probably isn't your favorite way to pass the time, but you'll find the Samba documentation complete, helpful, and easy reading. At least skim through the files to see what's there, so you know where you can go to get additional information when you need it.

With all the Samba texts available today (some free, some not), you should have everything you need to configure even the most complex setup. Some excellent texts and resources dedicated to everything Samba immediately come to mind: The Official Samba-3 HOWTO and Reference Guide, Second Edition, by John Terpstra and Jelmr Vernooij (editors), published by Prentice Hall in 2005, is still relevant, and always relevant is the official Samba Wiki, located at https://wiki.samba.org.

# CHAPTER 25 | Distributed File Systems (DFS)

# Linux Administration: A Beginner's Guide

Chapters 23 and 24 discussed the venerable network file systems in the Linux/UNIX world. And both allow the sharing of file systems and other resources across a network of systems. This chapter covers another class of network file systems that aims to solve a slightly different set of problems in addition to the problems solved by traditional NFS and SMB network file systems. This class of network file systems is referred to as Distributed File Systems (DFS). DFS provides a mechanism to give you a unified view and access to file resources located on different servers. The operative word here is “distributed,” and it essentially means that the file system resources can be divided, shared, or distributed in a logical or physical manner across a network.

Plain vanilla network file systems do a wonderful job of making the storage on a single server available to other clients on a local area network (LAN). They often do not have the inherent ability to scale or grow beyond that single server or LAN. And they do not have the inherent ability to offer a unified (and consistent) view of a shared file system residing on multiple servers or across physically or geographically disparate locations—to make the data appear as a single resource to the end user.

> NOTE We say “inherent” here because, in truth, some solutions/hacks do exist that can make the plain network file systems mimic the behavior of fully-fledged DFS systems.

![](img/9f6657924397c33f088db5321b751a83_658_0.png)

# DFS Overview

“A picture,” they say “is worth a thousand words.” We’ll use a series of pictures to provide an overview of DFS. Suppose, for example, that we have a network of systems like the one depicted in Figure 25-1.

Our network consists of the following elements:

- * A massive set of DATA (files, directories, and so on). In this example, all the DATA in it is referred to as MASSIVE_DATA.
- * A traditional NFS or Common Internet File System (CIFS) server hosting MASSIVE_DATA. This is server-A.
- * A bunch of client systems and users that need to access MASSIVE_DATA hosted on server-A. These client systems are client-C, client-D, and client-F.
- * With everything else being, server-A is fine and up to the task of serving MASSIVE_DATA to the clients—provided that the clients are connected to it via some high-speed network, such as a LAN.

![](img/9f6657924397c33f088db5321b751a83_659_0.png)

**Figure 25-1** Traditional network file server and LAN clients

In Figure 25-2, things are switched around a little: We've added more client systems. In addition to the elements and conditions shown in Figure 25-1, our new scenario has the following elements:

- * A bunch of new client systems—client-G, client-H, client-I, and client-J—that need access to MASSIVE_DATA on server-A.
- * The new clients, are not directly connected to the LAN as server-A. Instead they are connected over a WAN (Internet).
- * The new clients are located in physically and geographically different locations.

Obviously, nothing has much changed as far as server-A is concerned—a bunch of new clients requiring access to MASSIVE_DATA.

However, a problem is created by the new requirements: even though server-A may still be up to the task of making its file system available to the new additional clients, the intervening network between the server and the new clients might not be up to

![](img/9f6657924397c33f088db5321b751a83_660_0.png)

Figure 25-2 Traditional network file server, LAN clients, and WAN clients

the task. The intervening network might be too slow, too congested, too unpredictable, and so on. It is also possible that server-A was simply not built to handle the additional demands and load of so many new clients.

The solution DFS offers to these problems is shown in Figure 25-3 and described in the following scenario:

- Place an additional file server (server-B) in physical proximity to the clients that require access to MASSIVE_DATA.
- Ensure that a copy of MASSIVE_DATA exists on all servers regardless of where they are located.
- Ensure that clients have fast, easy, and consistent access to MASSIVE_DATA.
- Ensure that bits and bytes that make up MASSIVE_DATA remain consistent and uncorrupted regardless of where the client is accessing or modifying the data.
- Ensure that any changes to MASSIVE_DATA are immediately reflected across all the copies, regardless of where they physically reside.

![](img/9f6657924397c33f088db5321b751a83_661_0.png)

Figure 25-3 Distributed File Systems network

# DFS Implementations

Numerous DFS solutions exist to tackle the scenarios described so far. These solutions vary in many sorts: they vary in complexity, ease of manageability, ease of configuration. Following are some DFS implementations:

- **GlusterFS (www.gluster.org)** This open source distributed system is frequently used for clustering. Its architecture makes it include these components: Metadata Server (MDS), Metadata Target (MDT).
- **Lustre (lustre.org)** This high-performance DFS requires a specially patched kernel to run. A standard Lustre setup includes these components: Object Storage Server (OSS), Object Storage Target (OST). 

# Linux Administration: A Beginner's Guide

**MooseFS (www.moosefs.org)** This simple-to-use, fault-tolerant DFS is relatively young. A typical MooseFS implementation consists of these components: master server, chunk servers, metalogger server.

**Microsoft DFS (MS-DFS)** Microsoft's implementation is a mature product that is relatively easy to install. The open source project Samba can emulate some of the features of MS-DFS.

**OpenAFS (www.openafs.org)** One of the older DFS implementations, OpenAFS is robust and well supported on multiple platforms—Windows, Linux, and OS. However, it is not easy to install and configure. It relies heavily on Kerberos.

**XtremeFS (www.extremefs.org)** This ambitious entrant into the DFS world is simple to set up and manage. It touts support for globally (WAN) distributed installations.

# DFS Terminology

Several concepts and terms are used in association with DFS:

- brick In DFS planning, a physical server/system whose local storage resource is contributing to the overall storage capacity of the DFS is often referred to as a "brick." Combining two or more bricks in different fashions forms the basics of DFS systems. Clients or hosts access the file system resources stored collectively and need not know that they are accessing the data on one or multiple bricks.
- metadata Refers to all the other characteristics of data (or a file) except the actual data. This can include the file size, the file permissions, timestamps, filename, and other attributes that can be used to describe the file. Different distributed file systems typically have a special manner with which they organize metadata information for the data they host. Some DFS implementations require a separate metadata server to be dedicated for the function of managing metadata information for the storage.
- fault tolerance This is a characteristic or feature that a DFS may or not provide. It allows transparent and continued access to the shared resource of the DFS in the event of a failure. Fault tolerance is akin to
