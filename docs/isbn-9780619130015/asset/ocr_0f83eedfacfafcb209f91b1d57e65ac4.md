# # Using UNIX Partitions

The section of the disk that holds a file system is called a **partition**. One disk may have many partitions, each separated from the others so that it remains unaffected by external disturbances such as structural file problems associated with another partition. When you install UNIX on your computer, one of your first tasks is deciding how to partition your hard drive.

UNIX partitions are identified with names; for example, Linux uses “hda1” and “hda2.” In this case, the first two letters tell UNIX the device type: “hd,” for instance, means hard disk. The third letter, “a,” for instance, indicates whether the disk is the primary or secondary disk (a=primary, b=secondary). Partitions on a disk are numbered starting with 1. The name “hda1” tells UNIX that this is the first partition on the disk, and the name “hda2” indicates it is the second partition on the same disk. If you have a second hard disk with two partitions, the partitions are identified as “hdb1” and “hdb2.” Computer storage devices such as hard disks are called peripheral devices. Computer **peripherals**, like hard disks, connect to the computer through *electronic interfaces*. The two most popular hard disk interfaces are the **IDE** (Integrated Drive Electronics) and **SCSI** (Small Computer System Interfaces). On PCs, IDE hard disk drives are more common than SCSI (pronounced “scuzzy”). SCSI is faster and more reliable. It is used on large servers. If you have a primary SCSI hard disk with two partitions, the two partitions are named “sda1” and “sda2.” Figure 2-2 shows two partition tables: one with an IDE drive and the other with a SCSI drive.

```
Disk/dev/hda: 128 heads, 63 sectors, 767 cylinders
Units = cylinders of 8064 * 512 bytes

Device Boot Begin Start End Blocks Id System
/dev/hda1 * 1 1 242 975712+ 6 DOS 32-bit >=32M
/dev/hda2 243 243 767 2116899 5 Extended
/dev/hda3 243 243 275 127024+ 83 Linux native
/dev/hda6 276 276 750 1028224+ 83 Linux native
/dev/hda7 751 751 767 68512+ 82 Linux swap

Command (m for help): _
This partition table is from a Linux system with an IDE drive
```

```
Disk /dev/sda: 255 heads, 63 sectors, 1106 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Begin Start End Blocks Id System
/dev/sda1 1 1 64 514048+ 83 Linux native
/dev/sda2 65 65 1106 8369865 5 Extended
/dev/sda5 65 65 1084 8193118+ 83 Linux native
/dev/sda6 1085 1085 1100 128488+ 82 Linux swap

Command (m for help): _
This partition table is from a Linux system with a SCSI drive
```

![](bbox=[0.21, 0.91, 0.45, 0.94])