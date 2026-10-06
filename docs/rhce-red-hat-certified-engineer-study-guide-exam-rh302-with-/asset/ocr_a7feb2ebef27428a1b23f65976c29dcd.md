# NFS

The Network File System (NFS) provides shared access to files and directories. In operation, an NFS server designates one or more directories available to clients. The designated directories are referred to as shares, which are said to have been exported by the server. Once exported by an NFS server, an NFS share can be mounted by a client system in the same way that a local file system is mounted. The Linux implementation is functionally similar to NFS implementations available on other Unix systems, and its client is largely compatible with NFS version 3.0.

An NFS server runs three NFS-related daemons:

+   - portmap, which forwards client requests to the correct NFS process access requests
- rpc.nfsd, which translates remote file access requests to local file requests
- rpc.mountd, which mounts and unmounts file systems

A host may be both NFS server and client, in case it runs all three daemons.

# Installation

Under Hat Linux 6.2, much of the NFS code has been incorporated in the Linux kernel. To use NFS, you'll require only these packages:

+   - nfs-utils, which contains utilities needed for using NFS
- portmap, which contains files related to portmap and is used by NFS servers

To install NFS, move to the directory containing the packages and issue the command
rpm -Uvh nfs-utils-*.rpm portmap-*.rpm

# Server Configuration

The NFS server configuration file is /etc/exports, each line of which is a directive that specifies a share (that is, an exported directory) and the associated access permissions. Here is a line from a typical /etc/exports file:

```
/exports/database free.azusapacific.com bob.azusapacific.com
```

The general format of the directive:

```
path host_list
```