```
226 Transfer complete.
182828 bytes received in 1.59 secs (1.1e+02 Kbytes/sec)
```

+   3. Install the nfs-utils RPM package by running `rpm -ivh nfs-utils*`.

```
[root@rh7 nfs]# rpm -ivh nfs-utils*
nfs-utils
########################################
```

+   4. Edit the `/etc/exports` file and share out the `/home` directory. For example:

```
# /etc/exports: the access control list for filesystems which
may be exported
#		to NFS clients.  See exports(5).

/home		(rw)
```

+   5. Start the NFS server by running `/etc/init.d/nfs start`.

```
[root@rh7 /root]# /etc/init.d/nfs start
Starting NFS services: 		[ OK ]
Starting NFS mountd: 		[ OK ]
Starting NFS quota: 		[ OK ]
Starting NFS daemon: 		[ OK ]
```

+   6. Check to make sure the directory is being exported correctly by running `exportfs`.

```
[root@rh7 /root]# exportfs
/home			<world>
```

The next steps guide you through mounting an NFS share. If you have two systems you should mount the share across the network for practice. Be sure that the user and group IDs match between the two systems so that the permissions are correct. If you have to change the IDs on one system, be sure to reset the permissions to their home directory and other files using the `chown` command.

+   1. Create a directory to mount the export to.

```
[root@rh7 /mnt]# mkdir /mnt/nfs
[root@rh7 /mnt]# ls
cdrom		floppy	nfs
```

+   2. Mount the directory using the command `mount ip.address:/home /mnt/nfs`.

```
[root@rh7 /mnt]# mount 10.254.90.145:/home /mnt/nfs
```