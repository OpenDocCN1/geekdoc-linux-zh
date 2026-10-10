control to the user. Although this has the potential of causing data loss, it allows clients to handle failed NFS servers more gracefully.

# SUMMARY

In this chapter, we discussed the process of setting up an NFS server and client. This requires very little change, so sharing your disks this way should be relatively pain free. Some key points to remember:

+   - NFS is a stateless protocol. Clients can't tell the difference between a crashed server and a slow server; thus recovery is automatic when the server comes back up. (In the reverse situation, when the client crashes and the server stays up, recovery is also automatic.)
+   - The key server processes in NFS are rpc.statd, rpc.quotad, rpc.mountd, and rpc.nfsd.
+   - Use rpcinfo -p to view all the RPC services on your system.
+   - Use exportfs -a to export all the file systems specified in the /etc/exports file.

NFS is a powerful tool for sharing disks. Be sure to spend some time experimenting with it to meet your system's resource-sharing needs.