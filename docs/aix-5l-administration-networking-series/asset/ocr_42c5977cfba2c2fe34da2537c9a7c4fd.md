A DFS filesystem mount point is similar in concept to a UNIX filesystem or NFS mount point. However, rather than using a directory as the mount point, DFS uses an object as the mount interface. To mount a DFS filesystem, use the **its crmount** command.

```
​ # fts crmount -dir [PathName] -fileset [FilesetName | FilesetID]
```

As an end user, you will not be able to tell the difference between a mount point directory and a mount point object. Use the **its lsmount** command to see if a directory serves as a mount point for a fileset.

```
​ # fts lsmount -dir /::/fs/home
```

DFS is a cached filesystem. Frequently accessed files and directories are cached on the client either in memory or on disk. Client cache consistency is maintained via a token-passing mechanism complete with callback for synchronizing shared access to file metadata. DFS servers control the rights to file access tokens that must be acquired by a client before modifying data. DFS also supports both scheduled and release (manual) filesystem replication.

You can also export an AIX CD-ROM filesystem from a DFS File Server. The exported CD-ROM filesystem can be mounted into the DFS file space and accessed from DFS client machines.

# Local File System

In order to gain the full benefit of DFS services and take advantage of access control lists, you must use the DCE Local File System (LFS) as the underlying physical filesystem for DFS. The LFS architecture and concepts of *aggregate* that are analogous to UNIX disk partitions and *filesets* that are collections of related files and directories. LFS directories are called containers, which hold other containers (subdirectories) and LFS objects, better known as files.

LFS is a log-based filesystem similar to the AIX Journaled File System (JFS). All filesystem metadata updates are grouped and logged as atomic transactions. Groups of transactions against a single object are also grouped into an equivalence class to facilitate recovery. The transaction equivalence class ensures that either all or none of the updates will be applied during system recovery.

DFS filesets may be moved between LFS aggregates while maintaining online access via a procedure called fileset cloning. Space must be available in the partition to build a copy of the fileset. The cloned fileset is marked "read only" and kept up to date via copy-on-write procedures until the move is complete. Filesets may also be replicated. Think of this as somewhat like cloning between computers over a network. Cloning and replication along with logging and dynamic aggregate sizing provide a highly available filesystem architecture that is quite easy to administer.

Table 15-2 is a comparison of Local File Systems and non-LFS.