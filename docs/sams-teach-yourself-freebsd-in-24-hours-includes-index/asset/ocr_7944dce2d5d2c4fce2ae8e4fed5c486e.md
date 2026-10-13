into the background and returns you to the command prompt. The following is the output you would get when trying to mount the share specified in the preceding example /etc/fstab line after trying for 60 seconds:

```
# mount /home2
spots:/home: nfsd: RPCPROG_NFS: RPC: Port mapper failure - RPC: Timed out

nfs: Cannot immediately mount spots:/home, backgrounding
```

The background mount_nfs process will keep trying to mount the share until it's successful. This method is particularly useful in computing clusters or labs in which NFS-mounted resources are nice to have but not required for correct operation—for example, a cluster in which an NFS mount contains popular user programs or games, but all critical system functions are available on disks on the local system.

# Samba and Windows File Sharing

FTP and NFS are good for communicating and sharing files between two UNIX machines. But the fact is that this is a Windows world, and no matter what kind of network environment your machine will be in, it will probably be surrounded by Windows machines. If you want to share files with your Windows using friends, you're going to have to play by their rules.

Fortunately, FreeBSD has the capability to do Windows-style file sharing with all the functionality that a Windows machine would have. Specifically, it has Samba, a software package that allows a UNIX machine to appear to be just another Windows machine on the local network; Windows machines can connect to it just as they would to another Windows machine. Samba even handles printer sharing and domain logins, and can act as a Windows domain controller in its own right.

An advantage that Windows NetBIOS/SMB protocol has over systems such as NFS is that it supports automatic server discovery, or browsing. In Windows, if you open the Network Neighborhood or My Network Places window, it will display the names of all available SMB servers on the local network. This way, you know which servers you can connect to without having to know their names in advance.

The name of each machine, as it appears in the network browser window (as shown in Figure 24.4), is its NetBIOS name, a designation that Windows allows to be up to 15 characters long. Although Windows requires you to input a NetBIOS name in uppercase, it shows up in the network browser window in initially capitalized, lowercase form. Under other operating systems (such as FreeBSD), the NetBIOS name is the same as the machine's hostname, truncated to 15 characters if necessary.