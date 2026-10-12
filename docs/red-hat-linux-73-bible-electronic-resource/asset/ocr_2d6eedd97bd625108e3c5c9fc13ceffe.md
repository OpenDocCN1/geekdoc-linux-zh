+   * **Device** — The device name is the name representing the hard disk partition in the `/dev` directory. Each disk partition device begins with two letters: hd for IDE disks, sd for SCSI disks, ed for ESDI disks, or xd for XT disks. After that is a single letter representing the number of the disk (disk 1 is a, disk 2 is b, disk 3 is c, and so on). The partition number for that disk (1, 2, 3, and so on) follows that.

+   * **Start/End** — Represents the partition's starting and ending cylinders on the hard disk.

+   * **Size (MB)** — The amount of disk space actually allocated for the partition. If you selected to let the partition grow to fill the existing space, this number may be much larger than the requested amount.

+   * **Type** — The type of file system that is installed on the disk partition. In most cases, the file system will be Linux (ext3), Win 95 FAT16 (fat), Win VFAT (vfat), or Linux swap. Table 2-1 lists the types of file systems that are available to assign to a disk partition. The number associated with each type of file system is what you would actually type if you were to assign that file system to a partition.

> **NOTE:** Not all file system types are supported in Red Hat Linux. Of those that are, some are not built into the kernel by default (such as NTFS). Even fewer are available to be created in Disk Druid. To see which file systems are built into the kernel, type `cat /proc/filesystems`. Accessing other file system types may require you to load the module using the `insmod` command (for example, `insmod minix`). Most of your needs should be served by `ext3` (Linux), `fat` and `vfat` (DOS/Windows), `swap` (Linux swap), and `iso9660` (CD-ROM). Those are all loaded automatically as they are needed.

+   * **Mount Point** — The directory where the partition is connected into the Linux file system (if it is). You must assign the root partition (`/`) to a native Linux partition before you can proceed.

+   * **Format** — Indicates whether (Yes) or not (No) the installation process should format the hard disk partition. Partitions marked `Yes` are erased! So, on a multiboot system, be sure to mark your Windows partitions, as well as other partitions containing data you want to keep, `No`!

# Table 2-1: File System Types and Numbers for Disk Partition

| Number | File System Type | Number | File System Type | Number | File System Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 01 | FAT12 | 42 | SFS | 87 | NTFS volume set |
| 02 | XENIX root | 4D | QNX4.x | 93 | Amoebe |
| 03 | XENIX usr | 4E | QNX4.x 2nd part | 94 | Amoebe BBT |
| 04 | FAT16 <32M | 4F | QNX4.x 3rd part | A0 | IBM Thinkpad hiberna |