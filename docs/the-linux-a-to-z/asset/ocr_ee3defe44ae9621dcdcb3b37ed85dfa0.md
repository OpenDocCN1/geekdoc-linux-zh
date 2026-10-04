A good tip at this point is to make a note of the numbers of blocks in the Linux partitions for later operations (16640 and 147200 here). Using the 'w' command we will now write this new partition table back to the disk and then quit from fdisk. While using fdisk, if something should go horribly wrong, you can use the 'q' command to quit from the program without making any changes to the original partition table on disk.

To make sure that the changes to the partition table take effect with all versions of fdisk you should now reboot the machine with the boot and root disks again. Once you have done this and logged back in as root again, you are ready to continue.

# 7.3.2 Creating Filesystems

Having now created the partitions for Linux, the next task is to make the filesystem structures within those partitions. This is just the Linux equivalent of the DOS format operation. Working on the swap partition first, you use two commands: mkswap to prepare the partition and swapon to tell Linux to bring the partition into use:

```
# mkswap -c /dev/hda2 16640
# swapon /dev/hda2
```

The -c switch to mkswap forces a check for bad data blocks in the partition. Obviously, if your swap partition is not hda2, then you would substitute the name of yours in the command. The number at the end of the line is just the block count of the swap partition, which you noted when you created the partitions. Again, you will substitute your own value in place of the 16640. The swapon command just takes a single parameter which is the name of the partition to use (hda2 here).

Before you can create the filesystems on the Linux native partitions, you have to choose which filesystem type to use. In fact, even though Linux supports several different filesystem structures, the best one all round is called the Second Extended Filesystem and it is the one to use. To make a second extended filesystem on a Linux native partition you use the mke2fs command:

```
# mke2fs -c /dev/hda3 147200
```

The parameters specify the partition to use and its size in blocks. Again, the -c switch forces a bad block check. If you have more than one Linux native partition then you will need to use mke2fs on each of them.

# 7.3.3 Installing Packages

Having prepared the disk partitions, you are now ready to load the Linux software into them. Each different Linux distribution has a different method for performing