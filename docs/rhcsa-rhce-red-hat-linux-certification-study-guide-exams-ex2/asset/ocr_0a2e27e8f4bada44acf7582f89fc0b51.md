This line sets up a mount in read-only mode, does not try to mount it automatically during the boot process, and supports access by regular users.

As desired, similar options are possible for removable media such as USB keys. But that can be more problematic with multiple USB keys; one may be detected as /dev/sdc once, and then later detected as /dev/sdd, if there's a second USB key installed. However, if properly configured, each USB key should have unique UUIDs. As described earlier, UUIDs are the RHEL 6 way to identify different volumes to be mounted in /etc/fstab.

# Networked Filesystems

The /etc/fstab file can be used to automate mounts from shared directories. The two major sharing services of interest are NFS and Samba. This section provides only a brief overview to how such shared directories can be configured in the /etc/fstab file; for more information, see Chapters 15 and 16.

In general, shares from networked directories should be assumed to be unreliable. People step on power lines, on Ethernet cables, and so on. If your system uses a wireless network, that adds an additional level of unreliability. In other words, the settings in the /etc/fstab file should account for that. So if there's a problem either in the network connection, or perhaps a problem like a power failure on the remote NFS server, that problem should not lead to a "hang" of a client, where the terminal (or more) is frozen due to the lost connection. Similar issues do not apply to Samba.

A connection to a shared NFS directory is based on its hostname or IP address, along with the full path to the directory on the server. So to connect to a remote NFS server on system server1 that shares the /var/ftp/pub directory, you could mount that share with the following command (assuming the /share directory exists):

```
# mount -t nfs server1.example.com:/pub /share
```

But that mount has some risks. The Red Hat Storage Administration Guide suggests the following entry in /etc/fstab:

```
server1:/pub  /share  nfs  rsize=8192,wsize=8192,timeo=14,intr,udp  0  0
```

The rsize and wsize variables specify the size of the blocks of data to be read and written in bytes, respectively. The timeo=14 directive specifies that the client will wait 1.4 seconds for the connection request to be completed. The intr allows the client to interrupt a connection; that's useful when the NFS server is not responding. The udp specifies a connection using the User Datagram Protocol (UDP). If the connection is to a NFS version 4 server, substitute nfs4 for nfs in the third column.