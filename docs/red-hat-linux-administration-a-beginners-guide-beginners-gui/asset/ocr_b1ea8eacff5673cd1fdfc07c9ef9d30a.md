# # Ask the Expert

**Q:** So NFS is a user-space daemon, then? I thought I saw some kernel options for NFS?

**A:** The NFS server was originally a user-space process. That is, no special kernel support was necessary for it to work. With the introduction of the 2.2 kernel, an optional kernel mode NFS server was introduced, with critical parts of the process actually compiled into the kernel for performance reasons. Recently (particularly in 2.4 kernels) the user-space version of the NFS server has fallen by the wayside in favor of the kernel mode version. Because only critical parts of the server are compiled into the kernel, user-space daemons exist to handle the rest of the protocol.

# ## Progress Check

+   1. What is the command to stop NFS without shutting the server down?
+   2. When a request to mount a partition is made, which file is consulted to determine access to the requested directory?

CRITICAL SKILL 16.3

# # Configuring NFS Servers

Setting up an NFS server is a two-step process. The first step is to create the /etc/exports file. This file defines which parts of your server’s disk get shared with the rest of your network and the rules by which they get shared. (For example, is a client allowed only to read a partition or is it allowed to write to that partition?) The second step is to start the NFS server processes that read the /etc/exports file and follow the specifications. Pretty straightforward, isn’t it?

![](bbox=[0.12, 0.79, 0.72, 0.9])

+   1. /etc/init.d/nfs stop.
+   2. The permission is stored in the /etc/exports file.