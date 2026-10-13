![](bbox=[0.156, 0.098, 0.244, 0.161])

You might wonder why some of the directories, files, and even commands associated with NFS use the phrase *dfs* or *df*. This usage comes from the System V (5) version of the UNIX operating system. Originally, Distributed File System (DFS) had two variations: NFS and the Remote File System (RFS). Directories, files, and commands containing the *dfs* phrase were used to manage and configure both types of file systems. Since then, RFS has disappeared, leaving behind the DFS legacy.

# The shareall and unshareall Commands

The **shareall** command shares one or more resources. If the **-F** fns command-line argument is not specified, the default file system type (NFS) is assumed. If the name of a file (that contains one or more **share** commands) is not specified as a command-line argument, the /etc/dfs/dfstab file is used by default.

The **unshareall** command unshares all currently shared resources. If the **-F nfs** command-line argument is not specified, the default file system type (NFS) is assumed.

# The dfshares Command

The **dfshares(1M)** command lists shared resources on the local or a remote system. If the hostname (or IP address) of a remote system is specified as a command-line argument, the resources shared on that system are listed.

In addition, two other command-line arguments are supported. The first is **-F nfs** (as previously described), and the other is **-h**. If specified, the header describing the columns of the resource listing is not displayed.

In addition, you can obtain information on locally shared resources from the /etc/dfs/sharetab file. This file is updated by the **share**, **shareall**, **unshare**, and **unshareall** commands to reflect the currently shared resources.

# Mounting NFS Resources

NFS resources that have been shared by an NFS server can be mounted by an NFS client using the **mount(1M)** command and unmounted using the **umount(1M)** command. In addition, any NFS resources identified in the /etc/vfstab file are automatically mounted at system boot or when the **mountall(1M)** command is used. Likewise, the NFS resources listed in the /etc/mnttab file are unmounted by using the **umountall(1M)** command.

# The mount Command

The **mount** command is used to mount NFS resources like any other standard Solaris file system so that NFS clients can mount and access them. For NFS, you specify the hostname (or IP address) and pathname of the