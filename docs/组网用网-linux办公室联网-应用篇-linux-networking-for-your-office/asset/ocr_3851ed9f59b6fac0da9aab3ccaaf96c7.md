# NOTE

> Although I’ve been referring to Linux functioning as a “backup server,” when Linux initiates the backup, it is technically the client computer. As far as the remote system is concerned, Linux is just a client system that happens to want to read a lot of files.

# Using tar to Back Up Mounted Filesystems

Just as tar is an effective means of backing up a single computer, it can back up an entire network, or just critical files from the network. In fact, there’s not a lot to be said about backing up a networked computer by using tar, although if the remote machine is a DOS, Windows, or OS/2 computer, you might want to look into a variant version of tar that’s included with the Samba package, as described in the next couple sections.

# Regular tar

One obvious and effective strategy for performing a server-initiated backup is to mount the remote filesystem and use tar or some other utility to back up the files. For instance, you could do something like this:

```
mount gingko:/ /mnt/gingko
cd /mnt/gingko
tar cvpf /dev/st0 ./
cd -
umount /mnt/gingko
```

This sequence backs up the root filesystem on the UNIX or Linux computer called gingko. If gingko’s NFS daemon exports mounted filesystems, this sequence backs up all of gingko’s filesystems. Of course, for this procedure to work, gingko must be configured to export filesystems to the backup server. You can perform a similar backup of Windows filesystems by using smbmount rather than mount.

# CAUTION

> Don’t attempt to back up a Linux or UNIX system via smbmount or smbtar. Doing so causes the loss of vital Linux/UNIX filesystem attributes, such as ownership and permissions. You can safely back up a shared FAT partition in this way, though, and this could be convenient if the system dual-boots between Linux and Windows: You can export the same partition under the same name in both OSs, and the backup server need not concern itself with which OS is in use at the time of the backup.