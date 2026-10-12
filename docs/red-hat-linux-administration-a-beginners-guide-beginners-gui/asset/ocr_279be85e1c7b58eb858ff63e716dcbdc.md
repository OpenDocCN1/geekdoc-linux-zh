On an NFS file system that is *hard-mounted*, the client must commit all changes to the server before allowing other operations. The client will continue trying to contact the server, until the server sends back an acknowledgment. From the user's perspective, it may look like the client system has crashed when it hasn't.

The purpose of configuring a file system as hard-mounted is to make sure that data being accessed via NFS does not get lost. For crucial file systems (such as the mail spool), this is a very important attribute.

*Soft mounts*, on the other hand, aren't quite as persistent about getting data written to the NFS server's disk. The client will try to access the server and commit unwritten data, but after a specified timeout period (number of retries), the client will give up and return control to the user. Although this has the potential of causing data loss, it allows clients to handle failed NFS servers more gracefully.

# ## Module Summary

In this module, we discussed the process of setting up an NFS server and client. This requires very little change, so sharing your disks this way should be relatively painless. Some key points to remember:

+   -   NFS is a stateless protocol (although work is being done to change this in future versions). Clients can't tell the difference between a crashed server and a slow server; thus recovery is automatic when the server comes back up. (In the reverse situation, when the client crashes and the server stays up, recovery is also automatic.)
+   -   The key server processes in NFS are `rpc.statd`, `rpc.quoted`, `rpc.mountd`, and `rpc.nfsd`.
+   -   Use `rpcinfo -p` to view all the RPC services on your system.
+   -   Use `exportfs -a` to export all the file systems specified in the `/etc/exports` file. (Use `exportfs -ra` after making changes.)

NFS is a powerful tool for sharing disks. Be sure to spend some time experimenting with it to meet your system's resource-sharing needs.

# ## Module 16 Mastery Check

+   1.  What is NFS?
+   2.  What does portmapper do?
+   3.  Is notification to the server necessary after mounting?