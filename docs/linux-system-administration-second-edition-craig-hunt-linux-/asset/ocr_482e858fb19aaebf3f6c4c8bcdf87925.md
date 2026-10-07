or you can back the partition up, resize it, and restore the backup. Some ext2fs partition resizers require that you separately resize a partition with fdisk and resize the filesystem with the partition resizer. Follow those tools' instructions, if you use them.

Once you've seen what (if anything) already exists on the disk, you can proceed to delete, add, and otherwise modify the partition table using fdisk's commands. Consider the following fdisk exchange:

```
Command (m for help): **p**

Disk /dev/hdb: 255 heads, 63 sectors, 1216 cylinders
Units = cylinders of 16065 * 512 bytes

Device    Boot     Start     End    Blocks Id System
/dev/hdl          257     1216   7711200  5 Extended
/dev/hdb2              1      192  1542208+ fb Unknown
/dev/hdb3            193      256    514080 17 Hidden HPFS/NTFS
/dev/hdb5            257      516  2088418+  6 FAT16
/dev/hdb6            517      717   1614501  7 HPFS/NTFS

Command (m for help): **n**
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
**1**
First cylinder (718-1216, default 718): **718**
Last cylinder or +size or +sizeM or +sizeK (718-1216, default 1216): **+400M**
```

In this situation, the initial configuration included five partitions, and the n command added a new one. fdisk gave the option of creating a *logical or primary* partition. The x86 partitioning scheme originally provided for only four partitions per disk, which soon became inadequate. The workaround was to use one of the original four *primary* partitions as a placeholder for a potentially large number of *logical* partitions. The "placeholder" primary partition is then referred to as an *extended* partition. In Linux, the primary partitions use numbers from 1 to 4; the logical partitions are numbered 5 and up. Linux doesn't care whether its partitions are primary or logical, so we recommend using mostly or exclusively logical partitions for Linux. This reserves primary partitions for OSSs that do need them, such as DOS, Windows, and FreeBSD.

Linux's fdisk lets you specify partition sizes either in terms of an ending cylinder number or in bytes, kilobytes, or megabytes. The preceding example specified a 400MB partition starting at cylinder 718.

> **Tip** For the final partition on a disk, enter the size by specifying an ending cylinder number that corresponds to the maximum available. This practice minimizes the amount of unused disk space.

By default, fdisk creates partitions that use the type code **0x83** (*Linux native*). Such partitions are suitable for holding Linux's ext2fs or any of the journaling filesystems available for Linux. If you want to create a Linux swap partition or a partition to be used in another OS, however, you must change its type code. You do this with the t command, which prompts you for a hexadecimal code. If you don't know the code, type L at this point for a list. (You can enter a code that's not on the list if you like, but fdisk won't be able to identify the associated OS if you do so.) You can use this feature to convert a partition created with another tool for use by Linux.

> **Note** Linux doesn't actually use the partition type codes except during installation. Instead, Linux relies on the –t parameter to mount, or on Linux's auto-detection algorithms, to determine the partition type. Many other OSSs, however, rely upon the partition type codes to determine what