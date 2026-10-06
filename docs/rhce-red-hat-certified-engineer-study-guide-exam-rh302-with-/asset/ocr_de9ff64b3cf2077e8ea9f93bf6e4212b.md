In the example, partitions hda5 and hda6 are Linux partitions that you'd want to check and possibly mount.

# The e2fsck Command

The e2fsck command checks a Linux file system for damage and, optionally, repairs simple damage. To check a file system, use a command of the form

```
e2fsck -y /dev/xxx
```

where xxx is the partition that contains the file system. The -y flag instructs e2fsck to automatically attempt to repair damage, rather than prompt you for each error found; without the flag, the command can become tiresome when a file system contains numerous errors.

Linux stores information about file systems in special areas called superblocks. If a file system is corrupt, you can sometimes recover it by instructing Linux to use an alternate superblock. To do so, you must know the location of the alternate superblock; usually they are written at intervals of 8192 blocks, so the first alternate superblock is likely to be located in 8193. To instruct e2fsck to attempt to recover a file system by using superblock 8193, issue a command of the form

```
e2fsck -b 8193 -y /dev/xxx
```

where xxx is the partition that contains the file system.

> Sparse superblocks are written at intervals of 32768 blocks. Therefore, the first alternate sparse superblock resides in 32769.

You can use the dumpefs to learn the location of alternate-blocks of an undamaged file system. If you're concerned about the possibility of file damage, you should run the command on each of your file systems and retain the output that it's available during recovery procedures. Here's typical output of the dumpefs command:

```
dumpefs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name: boot
Last mounted on: <not available>
Filesystem UUID: c10e5c68-d5a7-11d3-93c2-88a3fd607d
Filesystem magic number: 0xEF53
Filesystem revision #: 0 (original)
Filesystem features: (none)
```