
## Creating Partitions and Filesystems

ISO-9660 and other optical disc filesystems are created with special tools intended for this purpose. Specifically, mkfs creates an ISO-9660 filesystem (with Rock Ridge, Joliet, HFS, and UDF components added), while dcdrecord writes this to a blank CD-R. The growsfs program combines functions but works only on recordable DVD media.

## Creating a Filesystem

Most filesystems, all Linux-native filesystems, have Linux tools that can create the filesystem on a partition. Typically, these tools have filenames of the form mkfs.ctype, where ftype is the filesystem type code. These tools can also be called from a front-end tool called mkfs; you pass the filesystem type to mkfs using its -t option:

```
# mkfs -t ext3 /dev/sda
```

For ext2 and ext3 filesystems, the mke2fs program is often used instead of mkfs. The mke2fs program is just another name for mkfs.ext2.

This command creates an ext3 filesystem on /dev/sda. Depending on the speed of the disk, and the size of the partition, this process can take anywhere from a fraction of a second to a few seconds. Filesystem-build tools support additional options, of which can greatly increase the time required to build a filesystem. In particular, the -c option is supported by several filesystems. This option causes the tool to perform a block check—every sector in the partition is checked to be sure it reliably hold data. If it can't, the sector is marked as bad and isn't used.

If you perform a bad-block check and find that some sectors are bad, chances the entire hard disk doesn't have to live long. Sometimes the sort of problem can result from other issues, such as bad cables or SCSI termination problems.

Of the common filesystems, ext2fs, ext3fs, and ext4fs provide the most options in their mkfs tools. These tools are one and the same; the program simply creates a filesystem with the appropriate features for the name that's called it. You can man mkfs.ext2 to learn about these options, most of which deal with obscure and unimportant features. One option that deserves mention is -m percent, which sets the reserved-space percentage. The idea is that you don't want the disk to completely fill up with user files; if the disk starts getting close to fill, Linux should report that the disk is full before it really is, at least for ordinary users. This gives the root ability to log in and create new files, if necessary, to help recover the system.

The ext2fs/ext3fs/ext4 reserved-space percentage defaults to 5 percent, which translates to a lot of space on large disks. You may want to reduce this value (say, by passing -m 2 to reduce it to 2 percent) on your root (/) filesystem and perhaps lower (1 percent or 0 percent) on some, as /home. Setting -m 0 also makes sense on removable disks, which aren't likely to be critical for system recovery and may be a bit cramped to begin with.

In addition providing filesystem-creation tools for Linux-filesystems, Linux distributions usually provide tools for various non-Linux filesystems. The most important of these may be for FAT. The main tool for this task is called mkdosfs, but it's often linked to the mkfs.mdos and mkfs.vfat names. This program can automatically adjust the size of the FAT data structure to 2, 16, or 32 bits depending on the device size. You can override this with the -F fat-size option, where fat-size is the FAT size in bits--12, 16, or 32. No special options are required to create a FAT filesystem that can handle Windows-style (FAT) filenames; these are created by the OS.

In Exercise 3.1, you'll practice filesystems using mkfs and related utilities.

## Exercise 3.1

## Creating Filesystems

Try creating some filesystems on a spare partition or a removable disk. Even a floppy disk will do, although you won't be able to create journaling filesystems on a floppy disk. The following steps are using a USB flash drive, /dev/sdc; change the device specification as necessary. Be sure to use an empty partition! Accidentally entering the wrong device could wipe your entire system!

This exercise uses a few commands that are described in more detail later in this chapter. To create some filesystems, follow these steps:

- 1. Log in as root.
- 2. Use fdisk to verify the partitions on your target disk by typing fdisk -l /dev/sdc. You should see a list of partitions, including the one you use for your tests. If fdisk reports a single partition with ee the Id column, the disk is a GPT disk, and you should verify the disk's partitions with gdisk rather than fdisk.
- 3. Verify that the partition is not currently mounted. Type df to see the currently mounted partitions and verify /dev/sd1 is not among them.
- 4. Type mkfs -t ext2 /dev/sd1. You should see several lines of information appear.
- 5. Type mount /dev/sd1 /mnt to mount the new filesystem to /mnt. (You may use another mount point, if you like.)
- 6. Type df /mnt to see basic accounting information for the filesystem. On my test system with a /dev/sd1 that's precisely 1000MiB size, 1,007,896 blocks are present; 1,264 are used; and 955,432 blocks are available. Most of the difference between the present available blocks are caused by the 5 percent reserved space.
- 7. Type umount /mnt to unmount the filesystem.
- 8. Type mkfs -t ext2 -m 0 /dev/sdc to create a new ext2 filesystem on the device, but without any reserved space.
- 9. Repeat steps 5–7. Note that the available space has increased (to 1,006,632 blocks on my t disk). The available space plus the used space should not equal the total blocks.
- 10. Repeat steps 4–7, but use a filesystem type of ext 3 to create a journaling filesystems (This won't be possible if you use a floppy disk.) Note how much space is consumed by the journal.
- 11. Repeat steps 4–7, but use another filesystem, such as JFS or ReiserFS. Note how the filesystem-creation tools differ in the information they present and in their stated de-creation tools.

## Tuning Filesystems

Three tools are particularly important for tuning these filesystems: dump2fs, tune2fs, and debug3fs. The first of these tools provides information about the filesystem, and the other two enable you to tune changing options.

## Obtaining Filesystem Information

You can learn a lot about your ext2 or ext3 filesystem with the dump2fs command. command's syntax is fairly straightforward:

```
dump2fs [options] device
```
