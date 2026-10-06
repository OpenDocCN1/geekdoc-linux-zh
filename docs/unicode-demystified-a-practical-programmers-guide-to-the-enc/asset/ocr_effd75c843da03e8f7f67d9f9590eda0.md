# Chapter 17 Red Hat Linux Administration

```
Last mount time: Thu Dec 20 20:59:51 2001
Last write time: Thu Dec 20 20:59:51 2001
Mount count: 6
Maximum mount count: -1
Last checked: Thu Dec 6 09:23:23 2001
Check interval: 0 (<none>)
```

Set the filesystem parameters on your system so that they are appropriate to the way you use your computer. Using the -C option to stagger the checks ensures that all the checks do not occur at the same time. Always check and upgrade filesystems to make sure that they have checks scheduled as you desire.

To change an ext2 filesystem to an ext3 filesystem, you must put a journal (page 145) on the filesystem, and the kernel must support ext3 filesystems. Use the -j option to set a journal on an unmounted filesystem:

```
# tune2fs -j /dev/hdd3
tune2fs 1.27, (8-Mar-2002)
Creating journal: none
This filesystem will be automatically checked -1 mounts or 0 days, whichever comes first. Use tune2fs -c or -i to override.
```

Before you can use fstab (page 959) to mount the changed filesystem, you must modify its entry in the fstab file to reflect its new name. Change the third column to ext3. This command changes an unmounted ext3 किसे to an ext2 filesystem:

```
# tune2fs -O ^has_journal /dev/hdd3
tune2fs 1.27, (8-Mar-2002)
```

Refer to the tune2fs manual for more details.

# RAID Filesystem

RAID (Redundant Arrays of Inexpensive Disks) spreads information across several physical disks into one larger virtual device. RAID improves performance and provides redundancy. There are more than six types of RAID configurations. Using Red Hat tools, you can set up software RAID. Hardware RAID requires hardware that is designed to implement RAID and is not covered here.

# Do Not Replace Backups with RAID

Do not use RAID as a replacement for regular backups. If your system undergoes a catastrophic failure, RAID will be useless. Earthquake, fire, theft, and so on may leave your entire system inaccessible (if your hard drives are destroyed or missing). RAID does not take care of something as simple as deleting a file you need. In these cases a backup on removable media (that has been removed) is the only way you will be able to restore your filesystem.

26. As disk prices have dropped, the Inexpensive part no longer applies.