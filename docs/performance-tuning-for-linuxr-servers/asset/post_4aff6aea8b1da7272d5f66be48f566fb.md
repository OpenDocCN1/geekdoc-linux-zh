
itself), including the popular smbclient utility program, which includes an FTP-like option for retrieving files via the SMB protocol.

The Linux 2.6 kernel also has been helpful for SMB servers. The popular open-source Samba SMB server performs up to 50% faster on the Linux 2.6 kernel than on Linux 2.4. Samba also has been ported to many other UNIX and UNIX-like operating systems. The CIFS protocol, which the Samba server and the CIFS client implement, can be used reasonably securely, and it is very rich in function due to many optional extensions. However, CIFS itself is not considered a formal standard in the sense that NFS version 4 (IETF RFC 3010) and HTTP (IETF RFC 2616) are. The Storage Network Industry Association (SNIA) does document the core CIFS protocol, and Linux/UNIX extensions to the CIFS network protocol are also standardized by SNIA. Standards proposals on additional "CIFS POSIX extensions" are in progress.

Network protocols are often described in terms of an abstract layered model called the ISO/OSI model. This model, when applied to CIFS, can be used to represent the implementation in the layers, as shown in Figure 16-1.

### Figure 16-1. The ISO/OSI model applied to NFS.

![](img/08b574e80eed8279bfda286dbd25d40d_436_0.png)

- **NFS.** Since 2003, NFS version 4 (NFSv4) has become the official Internet Engineering Task Force (IETF) network file system standard. However, more widely deployed are systems based on the much more primitive NFS versions 2 and 3, which are commonly used for UNIX-to-UNIX network file system access. NFS version 3, although it performs reasonably well in Linux-to-Linux (and UNIX-to-UNIX) environments, does not handle distributed caching as safely as some other protocols. It is also prone to security problems because of its primitive design. NFSv4, which includes many CIFS-like features, addresses many of the functional and security deficiencies of version 3, but it often shows worse performance than CIFS.

The ISO/OSI model, when applied to NFS, divides the implementation into the layers shown in Figure 16-1.

- **WebDAV (HTTP extensions).** The WebDAV extensions to HTTP can be used to mount (NET USE) from newer Windows clients to many popular web servers when DAV extensions are enabled on the server. WebDAV, sometimes described as Web Folders, also has been included in applications such as web browsers. The Internet Explorer (IE) browser has included WebDAV support since IE version 5.5. WebDAV is not optimized for performance, and Linux does not include a client file system for it in the kernel at this time (although some distributions include a user-space implementation of a Linux WebDAV client). Various popular Linux applications are WebDAV-enabled.

- **AFS/DIFS.** During the mid-1990s, these were the most sophisticated of the commonly deployed network file systems and commonly were used on mid- to high-end UNIX systems. AFS (and the loosely related DCE/DFS) is gradually fading in importance as IBM and others have announced plans to eventually discontinue support for them. An open full function implementation of AFS client and server, OpenAFS exists for Linux, as well as a second, more primitive AFS client, which has been accepted into the 2.6 kernel.

- **AFP.** Older Apple Macintosh operating systems (prior to OS X) used a filing protocol called AFP by default, instead of CIFS or NFS, although third-party CIFS clients for these systems were available from companies such as Thursby. Some Linux distributions include the open-source Netatalk server for handling requests from AFP clients, and at least one commercial AFP server is available (from Helios). AFP is quickly fading in importance as these clients become less common. No AFP file system client is included in the Linux kernel.

- *Specialized network file system protocols*, such as Coda and Intermezzo, and also various hybrid (some proprietary) SAN/NAS protocols, are less widely deployed. The most popular protocol from the early days of network file systems, Novell's NCP, is fading in popularity. NCP's current installed base is hard to measure, and NCP servers are rarely deployed on Linux.

- **Cluster file systems.** A battle is looming over the best Linux cluster file system. Lustre and GFS (from Red Hat/Susina) are the early leaders in this race to get accepted into the 2.6 kernel. Cluster file systems can be thought of as network file systems that support strict POSIX file system semantics (just like local file systems) designed for use by groups of homogeneous systems coupled by high-speed networks. In addition, some of the SAN file systems, such as IBM's StorageTank and GPFS, have similar characteristics and goals. None of these have been accepted into the Linux kernel as yet, but pressure is mounting to include at least one, and they are likely to become important for supercomputer clusters in particular.

We have discussed multiple popular network file systems (including NFSv3, NFSv4, CIFS, HTTP/WebDAV, and AFS). Because network file systems have been around for almost 20 years, as can be seen from the history mentioned here, why haven't we converged on one dominant network file system (as we have converged on TCP/IP for the lower layers)? Because network and SAN file systems present unique design problems that are not perfectly addressed by any one network file system. Why are network file systems so hard to design? The following are some reasons:

- Network file systems, unlike local file systems, have to manage two views of the same data/metadata (local and server).
- They should implement distributed cache coherence over multiple machines in order to guarantee POSIX file API semantics and preserve the integrity of the following:
  - File data
  - File metadata (date/timestamps, ACLs)
  - Directory data
- Network file systems have to work around the potential for "redundant" locks being enforced in conflicting ways on client and server.
- Network file systems have to adjust to transient identifiers for files and differing inode numbering on client and server.
- Network file systems cannot assume that the file namespace is the same on server and client, or even that the code page (the character set used for converting language characters and displaying filenames) is the same on client and server.
- Network file systems must compensate for holes, omissions, and errors in the network protocol design and/or server operating system. The NFS network file system when running on Windows, for example, has to be able to translate to UNIX-like NFS protocol frames (which were designed to map to Solaris, Linux, and similar operating system functions) from Windows file requests. This is difficult because the Windows file API is so much bigger than the POSIX file API and includes flags that have no POSIX counterpart.
- Most network file systems implement various network security features, such as those in the following list, to provide safer transfer of data across potentially hostile routers:
  - Distributed authorization
  - Access control
  - PDU integrity
- Network file systems deal with much more exotic, multiple-machine, network-failure scenarios, which are complex to analyze. Network file systems also have a harder time than local file systems in implementing file and server "migration" (movement/replication of data from one volume to another) and transparent recovery.

NFS version 4 and CIFS/Samba (CIFS kernel client and Samba server) on Linux address most of the issues listed here and are commonly used. But is one clearly better? Is NFS better than CIFS? Not always. The trade-offs to consider are as follows:

- NFS version 3, although quite fast, is less secure than SMB/CIFS.
- NFS maps slightly better than SMB/CIFS maps to the internal Linux VFS file system kernel API, although the CIFS VFS provides excellent POSIX semantics when mounted to a Samba server, which has enabled the optional CIFS UNIX Extensions (available in Samba version 3 or later).
- The Linux NFS client lacks support for Linux xattrs (which the CIFS client does provide) but the NFS client can handle direct I/O (which the Linux CIFS implementation currently does not).
- The CIFS mount protocol (SMB SessionSetupAndX and SMB TreeConnectAndX) does not require use of a UNIX UID, which is helpful in heterogeneous networks. UID mapping in networks that include Windows and Linux servers can be difficult. Therefore, having consistent UID mapping among servers and clients is helpful when using NFS versions 2 and 3.

Note that NFS is not popular on Windows, because most Windows versions do not include an NFS server or client in the operating system itself, and the NFS protocol maps better to the simpler UNIX VFS interface than to the complex, functionally rich Windows IFS. Microsoft does offer a simple NFS (version 2 and 3) server as a free download as part of its Services for UNIX.

NFS version 4, due to new security and caching features, will be appealing in the future, especially for Linux-to-Linux network file system access, but because it is not well supported on most Windows clients and servers, its adoption has been slow. Its Linux implementation in the 2.6 kernel is as yet unproven and is missing some optional features. NFSv3 performance from Linux clients over Gigabit Ethernet can be spectacular, especially to NFS servers based on the 2.6 kernel. NFS version 3 (over UDP, at least) receives the most testing and is most likely the most stable choice for network file systems when mounting from Linux clients to Linux servers.

## Client and Server Implementation Choices

For NFS, the implementation choice is simple: The most popular client and server implementation is the one available in the kernel itself. However, there are choices for the RPC (SunRPC) daemon. The choices available when building the Linux 2.6 kernel are whether to enable support for the following:
