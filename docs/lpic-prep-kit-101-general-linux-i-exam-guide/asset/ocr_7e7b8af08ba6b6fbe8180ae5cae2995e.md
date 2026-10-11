Are there files that are not being used? Try compressing them and perhaps relocating them to another device. Directories also should not get too large because very large directories can affect system performance. Move files to several smaller directories.

One of the problems with directories is that they grow but do not shrink. So, if you move or delete a large number of files from a directory, you will not recover all the free space.

The only way to shrink the size of a directory is by deleting it. Therefore, copy the files you want to keep to another directory and then delete the original directory. After you’ve done this, you can re-create the directory with the same name and move the needed files to the new directory.

If you are outgrowing a partition, you have a couple choices for fixing the problem.

One possibility is to move some files to another partition and then place links to them on the original partition. See Chapter 6 for information on how to use links.

A better way would be to actually increase the size of the partition. However, this is also a more complex process. The first thing you must do is to make sure you have an up-to-date backup of the information on that partition. See Chapter 11, “Backup and Restore,” for information on performing backups.

Next, you must decide where the extra space will come from. You can use any free space that exists on the same hard disk or free space from another hard drive, or you can add another hard disk.

You must delete the old partition and then create a new partition to take its place. Partitions can’t be dynamically expanded under Linux; they must be deleted and re-created with a larger size. After you have created a larger partition, you will need to restore the original information. The restore operation is also covered in Chapter 11.

# ## Summary

In this chapter, we have covered the types of partitions you will create. A primary partition is necessary for an operating system to boot. An extended partition is a container for logical drives that are then used to store data. Linux also has a special type of partition called a swap partition, which are used as virtual memory.

The fdisk utility is used to create these partitions. When creating a new partition, you must designate the beginning and ending cylinders. After the partitions are created, you must create a filesystem by using the format command.

The fsck command is used to examine the filesystem for errors and can be used to repair any errors found. Other utilities you can use to monitor your disks’ health are the df and du commands, which are used to determine partition size and usage.