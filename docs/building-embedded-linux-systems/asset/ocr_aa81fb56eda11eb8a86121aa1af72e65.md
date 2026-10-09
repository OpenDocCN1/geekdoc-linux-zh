```
cps
}
= 100 2
```

Regardless of the super-server in use on a host, the TFTP service is usually disabled by default. Hence, even if you use the default /tftpboot directory, you need to modify the super-server’s configuration files to enable TFTP.

# ## Mounting a Root Filesystem on an NFS Server

As we explained in Chapter 2, although the bootloader and Linux kernel must be stored locally or retrieved to local storage through one of the methods shown earlier, the target’s kernel can subsequently mount its root /filesystem from a remote NFS server. To this end, the NFS server must be properly installed and configured. Chapter 6 showed how to build your target’s root filesystem. If this filesystem is retrieved from an NFS server, the filesystem does not need any of the preparations described in Chapter 8.

The NFS server daemon is available in two flavors: as a standalone user application or as a part of the kernel. Besides being faster, the latter is also the standard configuration in most distributions. In addition to the NFS server itself, you need to have the NFS utilities installed. Usually, an nfs-utils package is part of your distribution. On an RPM-based distribution, use the following command to identify whether nfs-utils is installed:

```
$ rpm -q nfs-utils
nfs-utils-1.1.0-r6.fc8
```

With the nfs-utils package installed, you need to make sure that the appropriate configuration files are present and the corresponding services are started. The main file we need to configure for the NFS server is /etc/exports. Entries in this file describe the directories that each host or set of hosts can access. Here’s an example:

```
/data/root/virtex4 192.168.1.201(rw,no_root_squash)
```

This entry states that the machine with address 192.168.1.201 has read and write (rw) access to the /data/root/virtex4 directory, which is the path to a root filesystem similar to that which we built for the target in Chapter 6. In addition, the no_root_squash argument indicates that the server should allow the remote system to access the directory with its root privileges. There are very powerful rights that we are granting to the target. If we have total control over access to the device, as is the case in most development setups, there is obviously no security risk. If, however, the target’s location is less secure or if it is directly connected to the Internet (a configuration you really want to avoid with any NSF server), for example, you may prefer to use the default root_squash instead. Otherwise, it is trivial for others to forge access from the 192.168.1.201 address and trash, or otherwise compromise, your exported data. With root_squash in effect, the target will not be able to write to most of its own root filesystem, though it will still be able to read and write