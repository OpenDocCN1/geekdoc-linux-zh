# Figure 12.2

DOS boot sector.

![](bbox=[0.259, 0.075, 0.883, 0.346])

> **Caution**
> 
> Installing LILO to the boot sector of a DOS filesystem makes the DOS data files inaccessible. This is because disk parameters are stored as part of a DOS boot sector, and a LILO boot sector does not contain disk parameters. Without the disk parameters, a DOS filesystem becomes inaccessible.

The disk organization of a hard disk differs from that of a floppy because of partitioning. Figure 12.3 shows how a typical hard disk might look if partitioned using primary and extended partitions. Because of BIOS limitations, a hard disk can be divided only into four primary partitions. If more than four partitions are required, extended partitions must be used. The partition information for a given disk is contained in the partition boot sector. The partition boot sector is commonly called the *master boot record* (MBR).

# Figure 12.3

Typical partitioned hard disk.

![](bbox=[0.259, 0.64, 0.715, 0.954])