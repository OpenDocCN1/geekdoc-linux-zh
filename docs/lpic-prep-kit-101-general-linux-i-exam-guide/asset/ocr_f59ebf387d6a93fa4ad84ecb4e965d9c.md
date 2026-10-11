# QUESTIONS AND ANSWERS

1. After installing a new hard disk, what is your first step?
A. You first will need to partition the hard disk. You can create up to four partitions on a single hard disk.

2. Before installing Linux on your computer, what should you do to prepare the hard disk?
A. After partitions have been created, you must associate each one with the appropriate filesystem and format the partitions so you will be able to save files to it.

3. Although you have 2GB of free space on your hard disk, when you use fdisk to create the partition, you receive an error and the action fails. Why?
A. One of two things might be the problem. First, if you already have four partitions on the hard disk, you will not be able to create any more partitions no matter how much free space you have. The second possibility is that you are trying to create an extended partition and one already exists. You can have only one extended partition at a time.

4. What can you do if you want to install Linux on a computer that is running Windows 95 and does not have any free space?
A. You can shrink the partition by using the fips program, provided that not all the partition is occupied by files. This will work as long as the partition is formatted with FAT16.

5. What do the terms hda1 and sdc3 mean?
A. These are both names of partitions. The first example, hda1, refers to the first partition on the first IDE drive. The second example, sdc3, is the name of the third partition on the third SCSI disk.

6. After creating a new partition, what might keep you from installing a new application on it?
A. One potential problem would be if there were not enough unoccupied space on the partition to house the application. Also, you must format a partition before you can save files to it.