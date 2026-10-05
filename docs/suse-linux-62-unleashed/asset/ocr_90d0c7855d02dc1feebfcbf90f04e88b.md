# Networking and Internet Services
PART II

The Network Filesystem, or NFS, is the means by which UNIX systems share their disk resources. NFS allows one to mount directories of another host and have it appear as though they were the client host's directories. What makes NFS really useful is its capability to function in a heterogeneous environment. Most UNIX variants, if not all, support NFS, and you can find NFS support for Microsoft Windows expensively, making it a good choice for sharing disks.

NFS was originally developed by Sun Microsystems during the 1980s. Sun shared its design and made the protocol standard, which eliminated any interoperability conflicts with other operating systems. Linux supported NFS before version 1.0 was released.

A key feature of NFS is its robust nature. It is a stateless protocol, meaning that each request made between the client and server is complete in itself and does not require knowledge of previous transactions. Because of this, NFS cannot tell the difference between a very slow host and a host that has failed altogether. This allows servers to go down and come back up without having to reboot the clients. If this doesn't make much sense, don't worry about it. Understanding the underlying protocol is not necessary for you to set up and successfully run an NFS server.

> In Chapter 16, "SAMBA," you'll read about how Linux can share its disks with Windows machines. NFS and Samba are not the same. They are two different protocols with two fundamentally views on how disks should be shared. One of the many things that makes Linux great is its capability to support both means of sharing disks at the same time. In fact, it's common for Linux servers to share disks with each other through NFS and with Windows-based clients with Samba at the same time.

> If you are granting write access, you should not grant write access to both Samba and NFS for the same directories. Samba uses a caching method known as "oplocking" that can mean that the current version of the NFS client sees different from the version of the file that all the Samba clients see.