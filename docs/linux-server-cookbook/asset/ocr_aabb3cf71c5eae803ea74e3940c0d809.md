```
[root@rhel ~]# mount -t nfs4 192.168.122.43:/mnt
[root@rhel ~]# ls /mnt
storage
```

# *Figure 10.4: Example usage command mount with NFS*

The client can use the command **mount** with the following syntax to manually mount a shared directory to the local system:

```
mount -t nfs|nfs4 -o options remotserver::/shared /exported
```

The popular options that can be specified when mounting an NFS share are the following:

+   * *vers=n* (or *nfsvers*=): Specifies the NFS protocol version to be used. Modern systems are using, by default, version 4.2.
+   * *soft/hard*: Indicates the recovery behavior if the client loses communication with the server. If *hard* is chosen, the connection will be retried indefinitely, and this is the default option. If the option *soft* is specified, the connection is not retried.
+   * *rsize/wsize*: The size for the read request or the write request.
+   * *proto*: It specified the protocol transport to use *tcp* or *udp*. On version 4, it is recommended to use *tcp*.
+   * *port*: The port to be used, by default, is 2049.

Figure 10.5 shows an example of how to mount the exported directory previously shown and how the output of the command **mount** without any argument shows the default options:

```
[root@rhel ~]# mount -t nfs4 192.168.122.43:/storage /exported
[root@rhel ~]# mount | grep /exported
192.168.122.43:/storage on /exported type nfs4 (rw,relatime,vers=4.2,rsize=524288,wsize=524288,namlen=255,hard,proto=tcp,timeo=600,retrans=2,sec=sys,clientaddr=192.168.122.226,local_lock=none,addr=192.168.122.43)
```

# *Figure 10.5: Output example command mount*

By default, the directories are exported with the option *root_squash*, and this option does not allow *root* users in the client to write in the mounted directory. A regular user can always write in the directory when the *user id* or one of his *group ids* is allowed to write. Figure 10.6 illustrates the creation of a new file on a shared directory: