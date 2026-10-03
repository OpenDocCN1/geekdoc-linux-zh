> NOTE
When using NFS, make sure that the systems you'll be connecting to are all at the same version of NFS. You might experience problems if your system is at NFS version 2 and the system to which you are trying to connect is at NFS 3.0.

# NFS Daemons

NFS uses a number of daemons to handle its services. These services are initialized at startup from the /etc/init.d/nfs.server and /etc/init.d/nfs.clients startup scripts. The most important NFS daemons are outlined in Table 17.1.

# TABLE 17.1

# NFS DAEMONS

| Daemon | Description |
|---|---|
| nfsd | An NFS server daemon that handles file system exporting and file access requests from remote systems. An NFS server runs multiple instances of this daemon. This daemon is usually invoked at run level 3 and is started by the /etc/init.d/nfs.server startup script. |
| mountd | An NFS server daemon that handles mount requests from NFS clients. This daemon also provides information about which file systems are mounted by which clients. Use the showmount command, described later in this chapter, to view this information. This daemon is usually invoked at run level 3 and is started by the /etc/init.d/nfs.server startup script. |
| lockd | This daemon runs on the NFS server and NFS client and provides file locking services in NFS. This daemon is started by the /etc/init.d/nfs.client script at run level 2. |
| statd | This daemon runs on the NFS server and NFS client and interacts with lockd to provide the crash and recovery functions for the locking services on NFS. This daemon is started by the /etc/init.d/nfs.client script at run level 2. |
| rpcbind | Facilitates the initial connection between the client and the server. |
| nfslogd | The nfslogd daemon provides operational logging to the Solaris NFS server. nfslogd is described later in this chapter. |

# Setting Up NFS

Servers let other systems access their file systems by sharing them over the NFS environment. A shared file system is referred to as a shared resource. You specify which file systems are to be shared by entering the information in a file called /etc/dfs/dfstab. Entries in