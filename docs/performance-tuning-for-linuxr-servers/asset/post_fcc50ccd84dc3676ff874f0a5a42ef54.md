
## XFS Utilities

- xfs_logprint: Prints the log of an XFS file system.
- xfs_ncheck: Generates path names from inode numbers for an XFS file system.
- mkfs.xfs: Constructs an XFS file system.

The xfsdump package contains the following utilities:

- xfsdump: Examines files in a file system, determines which ones need to be backed up, and copies those files to a specified disk, tape, or other storage medium. It uses XFS-specific directives to optimize the dump of an XFS file system. It also knows how to back up XFS extended attributes.
- xfsrestore: Performs the inverse function of xfsdump; it can restore a full backup of a file system. Subsequent incremental backups can then be layered on top of the full backup. Single files and directory subtrees may be restored from full or partial backups.
- xfsdq, xfsrq: XFS dump and restore quotas.
- xfs_estimate: Estimates the space that an XFS file system needs.
- xfs_fsr: Reorganizes file systems for XFS.
- xfsinvutil: Checks and prunes the xfsdump inventory database.

Following are descriptions of some of the key file system utilities:

- xfs_db: Reports overall fragmentation of the file system. The following example shows overall fragmentation of file system /dev/hda9:

```
# xfs_db -r /dev/hda9
xfs_db: frag
 actual 408, ideal 408, fragmentation factor 0.00%

 actual/ideal are number of extents, factor is like
 (actual - ideal) / ideal
```

- xfs_bmap: Shows the number of extents in a file. The following example shows the number of extents in file vmlinuz:

```
# xfs_bmap vmlinuz
vmlinuz:
 0: [0..2295]: 96..2391
```

## Summary

Although some people believe that journaling file systems provide only fast restart times, this chapter has shown that not to be the case. Journaling file systems are scalable, reliable, and fast. Whether you are running an enterprise server, a cluster supercomputer, or a small web site, Ext3, XFS, JFS, and ReiserFS add credibility and performance improvements to Linux.

One of the great things about open source is that choice is looked on favorably. Linux is the only operating system with four journaling file systems in production. All four file system types have the GPL license, and source code is available at http://www.kernel.org or on each project's home page. Each of the journaling file system teams follows a community model and welcomes users and contributors. In fact, the teams share their best ideas, and competitive benchmarking encourages constant improvement of all the systems.

Table 11-1 summarizes the features and limits of the four Linux journaling file systems. The first section provides some history of when the journaling file systems were accepted into the kernel.org source trees. The next section lists some of the features of the file systems.

### Table 11-1. A Comparison of Journaling File Systems

| Kernel Support | Ext3 | ReiserFS | XFS | JFS |
| :--- | :--- | :--- | :--- | :--- |
| In kernel.org source tree 2.4.x | 2.4.15 | 2.4.1 | 2.4.25 | 2.4.20 |
| In kernel.org source tree 2.6.x | 2.5.0 | 2.5.0 | 2.5.36 | 2.5.6 |
| License | GPL | GPL | GPL | GPL |
| Features | | | | |
| Largest block size supported on IA32 | 4KB | 4KB | 4KB | 4KB |
| File system size maximum | 16384GB | 17592GB | 18,000Pb | 4Pb |
| File size maximum | 2048Gb | 1Eb* | 9,000Pb | 4Pb |
| Growing the file system size | Patch | Yes | Yes | Yes |
| Online snapshot | Yes | Yes | Yes | Yes |
| Access control lists | Yes | Yes | Yes | Yes |
| Extended attributes | Yes | Yes | Yes | Yes |
| Dynamic disk inode allocation | No | Yes | Yes | Yes |
| Data logging | Yes | Patch | No | No |
| Place log on an external device | Yes | Yes | Yes | Yes |

For complete feature lists of each journaling file system, see the respective project web pages.

Because the 2.4 kernel has a limit of 2 terabytes for a single block device, no file system larger than that can be created at this time. This restriction has been increased in the 2.6 kernel, and the limit has been raised to 16 terabytes.

## References

- [1] Andrew Morton’s web page has information about Ext3. http://www.zipworld.com.au/~akpm/linux/ext3.
- [2] The e2fsprogs package contains the utilities for the Ext2/Ext3 file systems and the home page for e2fsprogs. http://e2fsprogs.sourceforge.net/.
- [3] Card, R., T. Ts'o, and S. Tweedie. "Design and Implementation of the Second Extended Filesystem." http://web.mit.edu/tytso/www/linux/ext2intro.html.
- [4] For a more in-depth discussion of ReiserFS design features and instructions on how to use and manage ReiserFS, see http://www.namesys.com.
- [5] For a more in-depth discussion of the JFS design features and instructions on how to use and manage JFS on Linux, see http://oss.software.ibm.com/jfs.
- [6] For a more in-depth discussion of the design features of XFS Linux and instructions on how to use and manage the XFS file system, see http://oss.sgi.com/projects/xfs.

## Chapter Twelve. Network Tuning

By Nivedita Singhvi

### Introduction

The Linux kernel makes available a large set of kernel variables that can be tuned to configure the system for functionality and optimum performance. Additionally, the kernel makes a large amount of information about the system available to the user. Utilizing this information to ensure the system's health and detect problems in configuration and the network are critical performance tasks.

The predominant networking environment that applications run on is the TCP/IP (transport control protocol/Internet protocol) network protocol stack, with IP version 4 currently the standard. Linux is widely used as a platform to host network infrastructure services such as web servers, mail servers, and domain name system (DNS) servers, which makes networking performance an important consideration for system administrators.

Although this chapter covers the more important variables for network tuning, it is by no means exhaustive. Documentation available in the Documentation directory of the kernel source tree, as well as system man pages, can provide more information. The information provided here is applicable to the 2.4 through 2.6 Linux kernel versions unless otherwise noted.

Let's begin by examining the network protocol stack.

### The Network Protocol Stack

To understand the need for network tuning, it helps to have a picture of how the operating system takes data from the application and sends it to a remote host, and does the reverse: how it receives data from a remote host on the network and delivers it to a local application.

The parts of the operating system that handle networking operations are fairly modular in nature, with different layers handling clearly separated functions, implemented by various protocols. A collection of layers from the application interface down to the device interface is referred to as the *protocol stack*. The *TCP/IP protocol family* is the most widely used protocol suite. Together with the socket layer and the device driver, it makes up the typical network protocol stack.

The socket abstraction layer is the common kernel interface to the application. To open a communication channel with remote (or local) hosts, the application creates a socket, which contains, among other infrastructure, buffers used to hold the data that is read and written by the application.

The transport layer makes available two different protocols: TCP (transport control protocol) and UDP (user datagram protocol), which provide reliable, connection-oriented and unreliable, connectionless types of traffic, respectively. In the case of TCP sockets, the TCP protocol takes the data written to the socket by the application and ensures that the data is bundled into segments, sent reliably to the other end, retransmitting data that is lost, and maintaining control over the flow of data to minimize congestion on the network.

The transport layer then hands the segmented data to the IP layer, which implements typical network layer functions such as routing the data packets to the end point successfully. IP hands off the data packet to the network device driver, which ensures that the data is transferred to the hardware. Each layer encapsulates the data with its own headers containing protocol-specific information.

In the reverse direction, when a frame is received over the network, the network card generates an interrupt to the kernel, which then invokes an interrupt handler to transfer the packet from the card to kernel memory and schedules the packet to be processed by the network stack. The incoming packet is queued for delivery to the network layers in a device-specific queue. IP delivers a data packet for the application to the TCP layer, which places it in the correct socket read buffer if the packet is successfully validated at each stage.
