# Linux Administration: A Beginner's Guide

Chapters 23 and 24 discussed the venerable network file systems in the Linux/UNIX world. And both allow the sharing of file systems and other resources across a network of systems. This chapter covers another class of network file systems that aims to solve a slightly different set of problems in addition to the problems solved by traditional NFS and SMB network file systems. This class of network file systems is referred to as Distributed File Systems (DFS). DFS provides a mechanism to give you a unified view and access to file resources located on different servers. The operative word here is “distributed,” and it essentially means that the file system resources can be divided, shared, or distributed in a logical or physical manner across a network.

Plain vanilla network file systems do a wonderful job of making the storage on a single server available to other clients on a local area network (LAN). They often, do not have the inherent ability to scale or grow beyond that single server or LAN. And they do not have the inherent ability to offer a unified (and consistent) view of a shared file system residing on multiple servers or across physically or geographically disparate locations—to make the data appear as a single resource to the end user.

> NOTE We say “inherent” here because, in truth, some solutions/hacks do exist that can make the plain network file systems mimic the behavior of fully-fledged DFS systems.

![](bbox=[0.085, 0.456, 0.143, 0.497])

# DFS Overview

“A picture,” they say “is worth a thousand words.” We’ll use a series of pictures to provide an overview of DFS. Suppose, for example, that we have a network of systems like the one depicted in Figure 25-1.

Our network consists of the following elements:

+   * A massive set of DATA (files, directories, and so on). In this example, all the DATA in it is referred to as MASSIVE_DATA.

+   * A traditional NFS or Common Internet File System (CIFS) server hosting MASSIVE_DATA. This is server-A.

+   * A bunch of client systems and users that need to access MASSIVE_DATA hosted on server-A. These client systems are client-C, client-D, and client-F.

+   * With everything else being, server-A is fine and up to the task of serving MASSIVE_DATA to the clients—provided that the clients are connected to it via some high-speed network, such as a LAN.