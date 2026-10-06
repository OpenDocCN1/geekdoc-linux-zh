Command (m for help): d
Partition number (1-5): 2

Command (m for help): d
Selected partition 1

Command (m for help): n
Partition type:

+   - primary (primary, 0 extended, 4 free)
- extended

Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-3981311, default 2048): 2048
Last sector, +sectors or +size(K,M,G) (2048-3981311, default 3981311):
Using default value 3981311

Command (m for help): w
The partition table has been alerted!

Calling ioctl(1) to re-read partition table.
Syncing disks.

This process begins with a p command to verify that the program is operating on the correct disk. With this information in hand, the three existing partitions are deleted. Note that the first two deletions ask for a partition, but the third doesn't, because one partition is left. Once it is done, n is used to create a new partition. Once the task is complete, the w command is used to write the changes to disk and exit the program. The result of this sequence is a disk with a single partition (/dev/sdc1) marked as Linux filesystem.

To work on a gdisk, you can use gdisk in the same way you use fdisk. From some details, such as the lack of a prompt to create extended, logical partitions, gdisk uses the same basic commands as fdisk.

# GNU Parted

GNU Parted (http://www.gnu.org/software/parted/) is a partitioning tool that works with MBR, GPT, ASM, BSD and other disk types. It also supports more features than fdisk and is easier to use in some cases. On the other hand, GNU Parted uses its own way of referring to partitions, which can be confusing. It's also finicky about minor disk partitioning quirks and errors than fdisk. Although GNU Parted isn't on the exam, knowing a bit about it can be handy.

You start GNU Parted much as you start fdisk, by typing your name followed by the device you want to modify, as in parted /dev/hda for partition /dev/hda. The result is