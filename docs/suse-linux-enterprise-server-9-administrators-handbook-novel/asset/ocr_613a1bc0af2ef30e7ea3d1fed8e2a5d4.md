DOS, Windows, and OS/2 operating systems. Today, Microsoft Windows uses SMB, better known as the *Common Internet File System* (CIFS), which utilizes NetBEUI (NetBIOS Enhanced User Interface) over TCP, as the standard network file sharing mechanism. Like NFS, a number of CIFS implementations are available for a wide variety of operating systems, including NetWare. Samba is an open source implementation of CIFS that runs on Unix/Linux platforms but speaks to Windows clients like a native. It allows a Unix/Linux system to move into a Windows “Network Neighborhood” without causing a stir. Windows users can happily access file and print services without knowing or caring that a Unix/Linux host instead of a Windows server is offering those services. In short, NFS and Samba are two different methods in which you can share your server’s disk storage with other systems over the network. The choice of which package to use depends on your network environment. If you have Windows workstations and servers, Samba would be a good choice. Or if you mostly have Unix/Linux-based systems, NFS would be a good option.

As mentioned at the beginning of this chapter, because of the complexity of NFS and Samba, rather than delving into the details, we simply supply the bare essentials you need to quickly set up a simple NFS server and Samba server. You can learn more about each of these protocols from other published documents, such as

+   - RFC 3530: Network File System (NFS) version 4 Protocol
+   - RFC 2624: NFS Version 4 Design Considerations
+   - RFC 2224: NFS URL Scheme
+   - *NFS Illustrated* (ISBN 0201325705)
+   - *The Definitive Guide to Samba 3* (ISBN 1590592778)
+   - *The Official Samba-3 HOWTO and Reference Guide* (ISBN 0131453556)

# Setting Up an NFS Server

A computer can be both an NFS server and an NFS client. Here, we concentrate on the NFS server aspect where your SLES server will make available (export) its files and directories over the network (via port 2049) to NFS clients.

The NFS daemon is integrated into the SLES kernel, so no installation is required; all you need to do is configure and then activate it. The main functionality is handled by the *nfsd.o* kernel module, and */usr/sbin/rpc.nfsd* is the user-space application that is treated as a “filesystem” and initiates the NFS server process; the */usr/sbin/rpc.mountd* application is used for NFS client operations.