First off, to enable quotas by user, you'll need to add usrquota to the list of mount options in the /etc/fstab file. For group-based quotas (that is, a configuration where all members of a group cannot collectively exceed a specific disk allocation) use grpquota, and, yes, you can specify both if you would like.

I have modified the mount entry for /disk2 because my intent is for this disk to be used for storing large media files like movies, MP3 music collections, tarballs, and so forth. Everyone will get a large quota, but I want to ensure that every user gets a fair shake at the disk space.

> As a reminder, a tarball is a cute name for an archive of files, usually a program and its supplemental docs, stored in compressed tar format. See Hour 7, "Large File Management and Backups," for more about this.

```
# cat /etc/fstab
LABEL=/          /          ext3   defaults       1 1
LABEL=/boot      /boot      ext3   defaults       1 2
none             /dev/pts   devpts gid=5,mode=620 0 0
none             /proc      proc   defaults       0 0
none             /dev/shm   tmpfs  defaults       0 0
/dev/hda3        swap       swap   defaults       0 0
/dev/hdcrom      /mnt/cdrom iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0         /mnt/floppy auto   noauto,owner,kudzu,ro 0 0
/dev/hdb         /disk2     ext2   defaults,usrquota 2 0
```

Note the addition of usrquota to the very last entry.

+   2. The next step is to create the two files: aquota.user and aquota.group.

> Different versions of Unix differ on the name of these two files. Newer Unixes use aquota.*, whereas other flavors use quota.*. Check the man page for the final verdict on your installation.

These two files have to go at the root of the disk in question, so we'll want to create them before we unmount and remount the disk.

```
# cd /disk2
# touch aquota.user aquota.group
# chmod 600 aquota.user aquota.group
# ls -l aquota.*
-rw------- 1 root root 0 Feb 22 10:10 aquota.group
-rw------- 1 root root 0 Feb 22 10:10 aquota.user
```