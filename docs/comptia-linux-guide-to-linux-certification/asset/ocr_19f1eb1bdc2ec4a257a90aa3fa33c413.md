| Description | Linux Name | Windows Name |
| --- | --- | --- |
| First primary partition on the first SATA/SCSI device | sda1 | C: |
| Second primary partition on the first SATA/SCSI device | sda2 | D: |
| Third primary partition on the first SATA/SCSI device | sda3 | E: |
| Fourth primary partition on the first SATA/SCSI device (EXTENDED) | sda4 | F: |
| First logical drive in the extended partition on the first SATA/SCSI device | sda5 | G: |
| Second logical drive in the extended partition on the first SATA/SCSI device | sda6 | H: |
| Third logical drive in the extended partition on the first SATA/SCSI device | sda7 | I: |

# Table 2-3 Example partitioning scheme for the first SATA/SCSI device

can automatically create partitions based on common configurations; however, it is generally good practice to manually partition to suit the needs of the specific Linux system.

At minimum, Linux typically requires only two partitions to be created: a partition that is mounted to the root directory in Linux ( / ) and that can contain all of the files used by the operating system, applications, and users, and a partition used for virtual memory (also known as swap memory). Virtual memory consists of an area on the hard disk or SSD that can be used to store information that would normally reside in physical memory (RAM) if the physical memory was being used excessively. When programs are executed that require a great deal of resources on the computer, information is continuously swapped from physical memory to virtual memory, and vice versa. Traditionally, Linux swap partitions were made to be at least the size of the physical RAM in the computer; however, they can be much larger if the Linux system is intended to run large applications. A swap partition does not contain a filesystem and is never mounted to a directory because the Linux operating system is ultimately responsible for swapping information.

Although you might choose to create only root and swap partitions, extra partitions make Linux more robust against filesystem errors. For example, if the filesystem on one partition encounters an error, only data on one part of the system is affected and not the entire system (i.e., other filesystems). Because there are some common directories in Linux that are used voraciously and as a result are more prone to failure, it is good practice to mount these directories to their own filesystems. Table 2-4 lists directories that are commonly mounted to separate partitions as well as their recommended sizes.

Each of these filesystems can be of different types. The most common types used today are the ext2, ext3, ext4, VFAT, and REISER filesystems, although Linux can support upward of 50 different filesystems. Each filesystem essentially performs the same function, which is to store files on a partition; however, each filesystem offers different features and is specialized for different uses. The ext2 filesystem is the traditional filesystem, and the Virtual File Allocation Table (VFAT) filesystem is compatible with the FAT and FAT32 filesystems in Windows. The ext3, ext4, and REISER filesystems, however, are much more robust than the ext2 and VFAT filesystems, as they perform a function called journaling. A journaling filesystem keeps track of the information written to the hard disk in a journal. If you copy a file on the hard disk from one directory to another, that file must pass into RAM and then be written to the new location