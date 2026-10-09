
## CHAPTER 15

### Distributed File System

In the late 1980s, the Open Software Foundation (OSF) went looking for a network-based filesystem architecture to overcome some of the limitations inherent in Sun NFS. The filesystem had to be stateful to support access control and locking better in a distributed environment. Improvements in caching, replication, and cloning were desired to improve performance and availability. A centrally managed directory structure was needed to enforce a common filesystem view between participating systems yet not restrict flexibility and access. All of these are features exhibited by the Andrew File System (AFS) architecture. So, the OSF selected AFS V4 from the Transarc Corporation as the basis for its Distributed Computing Environment (DCE) Distributed File System (DFS) technology.

Conceptually, DFS is enhanced AFS. The major differences involve the tight integration of DFS with the other DCE services, and the underlying DCE local file system (LFS). DFS requires a larger number of support daemons than are normally used with AFS and far more than with NFS. Users who are familiar with AFS will be able to adapt to DFS semantics easily. Systems Administrators will require a little more homework in order to configure and activate all the DCE services on which DFS depends, as well as manage the DFS environment itself. My intent in this chapter is to provide a cursory overview of AIX DFS. Proper treatment of the subjects of AIX DFS and AIX DCE easily requires an entire book in itself. I hope to at least get you started. Here is a bit of history first.

### Andrew File System

In order to impose additional levels of authentication and administration and to improve the scalability of NFS, Carnegie Mellon University developed the Andrew File System (AFS). AFS, now a product of the Transarc Corporation, uses a remote procedure call mechanism called Rx to support client/server interactions. AFS uses the Kerberos V4 authentication system to validate client access to remote filesystems. AFS introduces the notion of a cell, which defines the administrative domain over filesystems in the shared space. A consistent view of the shared filesystem space is provided using a common root tree, `/afs`. Subtrees for each cell follow the root using the cell name `/afs/cellname/*`. Note that no restriction is placed on mount points or naming under NFS. AFS cells are identified by a database called CellServDB.

AFS security is further enhanced through the use of Access Control Lists (ACLs). ACLs extend the standard UNIX file permissions to provide a finer degree of granularity on access rights. AFS uses the first four UNIX permission bits to define read, lookup, insert, write, delete, lock, and administrator (r/wlida) permissions. Note that AFS ACLs apply to only the directory levels of a filesystem. AFS also uses a UserList to define access rights and mapping. Users gain access to the AFS shared file space via the **klog** command, which grants them a Kerberos ticket for access. They can release their rights via the **unlog** command. Under AFS, the standard path can no longer be used to access files on the server.

Another important enhancement for distributed filesystems is that AFS separates the logical filesystem structure from the disk blocks used to contain the filesystem. AFS volumes may contain one or many filesystem hierarchies. The volumes are made up of partitions that are collections of disk blocks identified by the special name, /vicep[n] (N=a, b, c, . . . ). AFS also improves client cache consistency using a callback mechanism to invalidate data blocks that have been modified. Release-level filesystem replication is also supported by AFS.

### General Parallel File System

The General Parallel File System (GPFS) for AIX is a shared disk filesystem. It was released in 1998 as a software simulation storage area network under the name Virtual Shared Disk (VSD). GPFS is basically a parallel disk filesystem guaranteeing availability of the entire filesystem to all nodes within a cluster, allowing simultaneous write access to a single striped file from multiple nodes. This can provide major benefits for parallel and sequential programs. GPFS is distributed to all the nodes in a cluster, providing an extended kernel interface to AIX and the virtual filesystems. System calls to AIX, from the applications, are translated to GPFS, which uses local resources or transfers them to a daemon that completes the task with buffer and I/O management much like a filesystem. The primary environment for GPFS, which is highly scalable, is the RS / 6000 SP with a high-speed switch network and HACMP with shared clusters of concurrent direct attached disks. Many high performance computing facilities use GPFS for temporary storage in large parallel computation workspace. DFS now provides the kernel extensions that enable GPFS data to be exported. With DFS consistency protocols, a filesystem may be exported from only one node, whereas NFS can export the same NFS data from multiple nodes, possibly providing higher throughput.

### Distributed File Service

The Distributed File Service, a distributed filesystem, takes the features offered by AFS and marries them with other OSF DCE services to compose a tightly integrated client / server computing environment. DFS relies on other DCE services to coordinate communication, access control, and synchronization. These services include the DCE Remote Procedure Call (RPC), DCE Security Service, DCE Globall and DCE Directory Service, and DCE Distributed Time Service. These DCE servers must be configured and started before you can begin working with DFS. IBM’s DCE V3.1 and DFS V3.1 are now sold separately and come with subtle packaging changes that were needed to synchronize the AIX and Solaris distributions. Table 15-1 breaks down the DFS file sets to show some of the packaging changes.

> NOTE Throughout this chapter are references to “file sets” that are Licensed Program Products as in Table 15-1 and “filessets” that are components of the DFS Local File System. This confusion will only persist in this chapter.

| Application | DFS V3.1 | DCE/DFS V2.2 |
| :--- | :--- | :--- |
| DFS Client Services | dfs.client | dce.client.dfs.rt |
| DFS Server | dfs.server | dce.dfs.server.rt |
| Enhanced DFS with Local File System | dfs.server | dce.edfs.rt |
| NFS to DFS Authenticating Gateway | dfs.nfsauth | dce.dfsrts.rt |
| DFS GPFS for AIX Support | dfs.gpfs.rt | N/A |
| DFS Storage Management Runtime | dfs.srm.rt | N/A |
| DFS Privacy Level Protection Feature | dfs.priv | dce.priv |
| DFS HTML Documentation | dfs.html.en_US | dce.doc.en_US.html |

### Access Control

Administrative domains called DCE cells delegate access control. Principals in a cell authenticate themselves via the DCE security service based on MIT Kerberos v5. Unfortunately, the AFS Kerberos v4 security service and the DCE Kerberos v5-based security service are not interoperable, making migration from AFS to DFS a bit of a chore. ACLs are used in DFS and apply to both directories and files. DFS modifies the standard UNIX file permission bits to support read, write, execute, control, insert, and delete permissions (rwxcid). The UNIX permission bits reflect the ACL permissions when viewed with standard commands like `ls -l`. DFS users are identified uniquely and globally to the DCE environment, so problems with UID and GID collisions are eliminated.

### Filesystem Structure

DFS shared filesystem trees are also similar to AFS in that a common root is identified with the next lower level delimited by cell name. The DFS shared root is named "/...", and cell subtrees follow as "/.../cellname". The shorthand strings "/:" and "/::" indicate the local cell and root files respectively. Clients need only mount root "/::"-level DFS space to access all filesystems exported by DFS file servers in the cell space. The following compares AIX and DFS path syntax that refers to the same relative home/username/.kshrc file.

| AIX | DFS |
| :--- | :--- |
| /home/username/.kshrc | /.../cellname//s/home/username/.kshrc |
| /:;fs/home/username/.kshrc | /::home/username/.kshrc |
