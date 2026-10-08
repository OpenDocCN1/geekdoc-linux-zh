# redhat

# Chapter 9.

# Network File System (NFS)

NFS (Network File System) allows to mount partitions on a remote system and use them as though they are local file systems. This allows the system administrator to store resources in a central location on the network, providing authorized users access to them.

Two versions of NFS are currently in use. NFS version 2 (NFSv2), has been around for several years, is widely supported by operating systems. NFS version 3 (NFSv3) has several features, including a variable file size and better error reporting. Red Hat Linux supports both NFS2 and NFSv3, and uses NFS3 by default when connecting to a server that supports it.

This chapter will focus on NFS version 2, though many of the concepts also apply to version 3. Additionally, only fundamental NFS concepts and supplemental information will be provided. For specific instructions regarding the configuration and operation of NFS on client or server machines, see the chapter titled Network File System (NFS) in the Red Hat Customization Guide.

# 9. Methodology

Linux uses a combination of kernel-level support and continuously running daemon processes to provide NFS file sharing, however NFS must be enabled in the Linux kernel in order to function. NFS uses Remote Procedure Calls (RPC) to route requests between clients and servers, meaning that the portmap service must be enabled and at the proper levels for NFS communication to occur. With portmap, the following processes ensure that a NFS connection is allowed and proceed without error.

+   * rpc.mountd — The running process that receives the mount request from an NFS client and checks if it matches a currently exported file system.
* rpc.nfsd — The process that implements the user-side components of the NFS service. It works with the Linux kernel to manage the dynamic demands of NFS clients, such as providing additional servers for NFS clients to use.
* rpc.lockd — A daemon that is not necessary with modern kernels. NFS file locking is now done by the kernel. It is included with the nfs-utils package for users of older kernels that do not include this functionality by default.
* rpc.statd — Implements the Network Status Monitor (NSM) RPC protocol. This provides notification when an NFS is restarted without being gracefully down.
* rpc.quota — An RPC server that provides user quota information.

Not all of them are required for NFS service. The only services that must be enabled are rpc.mountd, rpc.nfsd, and portmap. The other may provide additional functionality and should only be used if the server environment requires them.

NFS version 2 uses User Datagram Protocol (UDP) to provide a stateless network connection between the client and server. NFS version 3 can UDP or TCP running over an IP. The UDP connection minimizes network traffic, as the NFS server sends a cookie after the client is authorized to access the shared volume. This cookie is a random value on the server's side and is passed along RPC requests from the client. The NFS server can be restarted without affecting the clients and the cookie will remain intact.

NFS only performs authentication when a client system attempts to mount a remote file system. To limit access, the NFS server first employs TCP wrappers. TCP wrappers reads the /etc/hosts.allow and /etc/hosts.deny to determine if a particular client should be