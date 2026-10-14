Now, you can access your entire system and, for example, correct mistakes in configuration files such as `/etc/fstab`, `/etc/passwd`, and `/etc/inittab`. The configuration files are now located in the `/mnt/etc` directory instead of in `/etc`.

To recover even completely lost partitions with the fdisk program by simply setting it up again, determine where on the hard disk the partitions were previously located and make a printout of the `/etc/fstab` directory as well as the output of `fdisk`.

```
earth:  # fdisk -l /dev/(disk)
```

Instead of the `(disk)` variable, insert, in order, the device names of your hard disks, such as `hda`.

# Repairing File Systems

Damaged file systems are tricky problems for the rescue system. This could happen after an unscheduled shutdown caused by power failure or a system crash. Generally, file systems cannot be repaired on a running system. If you encounter really severe problems, you may not even be able to mount your root file system so the system boot ends in a "kernel panic". Here, the only chance is to repair the system from the "outside" using a rescue system.

The SuSE Linux rescue system contains the utilities e2fsck and dumpe2fs (for diagnosis). These should remedy most problems.

In an emergency, man pages often are not available. That is why we have included them in this manual in Appendix A on page 431.

Example: If mounting a file system fails due to an invalid superblock, the e2fsck program would probably fail, too. If this were the case, your superblock may be corrupted, too. There are copies of the superblock located every 8192 blocks (8193, 16385, etc.). If your superblock is corrupted, try one of the copies instead. This is accomplished by entering the command:

```
earth:  # e2fsck -f -b 8193 /dev/damaged_partition
```

The `-f` option forces the file system check and overrides e2fsck’s error so that — since the superblock copy is intact — everything is fine.

# Virtual Consoles

Linux is a multiuser and multitasking system. You will learn to appreciate the advantages of these features, even on a stand-alone PC system.