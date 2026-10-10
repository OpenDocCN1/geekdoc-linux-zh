
This command creates an ext3 filesystem on `/dev/hda6`. Depending on the filesystem, the speed of the disk, and the size of the partition, this process can take anywhere from a fraction of a second to a few seconds. Most filesystem-build tools support additional options, some of which can greatly increase the time required to build a filesystem. In particular, the `-c` option is supported by several filesystems. This option causes the tool to perform a bad-block check—every sector in the partition is checked to be sure it can reliably hold data. If it can't, the sector is marked as bad and isn't used.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_204_0.png)

If you perform a bad-block check and find that some sectors are bad, chances are the entire hard disk doesn't have long to live. Sometimes this sort of problem can result from other issues, though, such as bad cables or SCSI termination problems.

Of the common Linux filesystems, ext2fs, ext3fs, and ext4fs provide the most options in their `mkfs` tools. (In fact, these tools are one and the same; the program simply creates a filesystem with the appropriate features for the name that's used to call it.) You can type `man mkfs.ext2` to learn about these options, most of which deal with obscure and unimportant features. One obscure option that does deserve mention is `-m percent`, which sets the reserved-space percentage. The idea is that you don't want the disk to completely fill up with user files; if the disk starts getting close to full, Linux should report that the disk *is full* before it really is, at least for ordinary users. This gives the `root` user the ability to log in and create new files, if necessary, to help recover the system.

The ext2fs/ext3fs/ext4fs reserved-space percentage defaults to 5 percent, which translates to quite a lot of space on large disks. You may want to reduce this value (say, by passing `-m 2` to reduce it to 2 percent) on your root (`/`) filesystem and perhaps even lower (1 percent or 0 percent) on some, such as `/home`. Setting `-m 0` also makes sense on removable disks, which aren't likely to be critical for system recovery and may be a bit cramped to begin with.

In addition to providing filesystem-creation tools for Linux-native filesystems, Linux distributions usually provide such tools for various non-Linux filesystems. The most important of these may be for FAT. The main tool for this task is called `mkdosfs`, but it's often linked to the `mkfs.msdos` and `mkfs.vfat` names, as well. This program can automatically adjust the size of the FAT data structure to 12 or 16 bits depending on the device size. You can override this option with the `-F fat-size` option, where `fat-size` is the FAT size in bits—12, 16, or 32. In fact, this option is *required* if you want to create a FAT-32 partition, which is a practical necessity for any partition over 2GB in size and is usually desirable for partitions over 512MB in size. No special options are required to create a FAT filesystem that can handle Windows-style (VFAT) long filenames; these are created by the OS.

In Exercise 3.1, you'll practice creating filesystems using `mkfs` and related utilities.

## EXERCISE 3.1

### Creating Filesystems

Try creating some filesystems on a spare partition or a removable disk. Even a floppy disk will do, although you won't be able to create journaling filesystems on a floppy disk. The following steps assume you're using a Zip disk, `/dev/sda4`; change the device specification as necessary. *Be sure to use an empty partition!* Accidentally entering the wrong device filename could wipe out your entire system!

This exercise uses a few commands that are described in more detail later in this chapter. To create some filesystems, follow these steps:

- 1. Log in as root.
- 2. Use `fdisk` to verify the partitions on your target disk by typing `fdisk -l /dev/sda`. You should see a list of partitions, including the one you'll use for your tests.
- 3. Verify that your test partition is not currently mounted. Type `df` to see the currently mounted partitions and verify that `/dev/sda4` is not among them.
- 4. Type `mkfs -t ext2 /dev/sda4`. You should see several lines of status information appear.
- 5. Type `mount /dev/sda4 /mnt` to mount the new filesystem to `/mnt`. (You may use another mount point, if you like.)
- 6. Type `df /mnt` to see basic accounting information for the filesystem. On a 100MB Zip disk, you should see that 95,171 blocks are present, 13 blocks are used, and 90,244 blocks are available. The difference between the present and available blocks is caused by the 5 percent reserved space.
- 7. Type `umount /mnt` to unmount the filesystem.
- 8. Type `mkfs -t ext2 -m 0` to create a new ext2 filesystem on the device, but without any reserved space.
- 9. Repeat steps 5–7. Note that the available space has increased (to 95,158 blocks on a Zip disk). The available space plus the used space should now equal the total blocks.
- 10. Repeat steps 4–7, but use a filesystem type code of ext3 to create a journaling filesystem. (This won't be possible if you use a floppy disk.) Note how much space is consumed by the journal.
- 11. Repeat steps 4–7, but use another filesystem, such as JFS or ReiserFS. Note how the filesystem-creation tools differ in the information they present and in their stated amounts of available space.

Be aware that, because of differences in how filesystems store files and allocate space, a greater amount of available space when a filesystem is created may not translate into a greater capacity to store files.

## Creating Swap Space

Some partitions don't hold files. Most notably, Linux can use a *swap partition*, which is a partition that Linux treats as an extension of memory. (Linux can also use a *swap file*, which is a file that works in the same way. Both are examples of *swap space*.) Linux uses the MBR partition type code of 0x82 to identify swap space, but as with other partitions, this code is mostly a convenience to keep other OSs from trying to access Linux swap partitions; Linux uses `/etc/fstab` to define which partitions to use as swap space, as described in Chapter 4, “Managing Files.”

![](img/f339a9f48c4b443e61c74acb4c9c3da4_206_0.png)

> Solaris for x86 also uses an MBR partition type code of 0x82, but in Solaris, this code refers to a Solaris partition. If you dual-boot between Solaris and Linux, this double meaning of the 0x82 partition type code can cause confusion. This is particularly true when installing the OSs. You may need to use Linux's fdisk to temporarily change the partition type codes to keep Linux from trying to use a Solaris partition as swap space or to keep Solaris from trying to interpret Linux swap space as a data partition.

Although swap space doesn't hold a filesystem *per se* and isn't mounted in the way that filesystem partitions are mounted, swap space does require preparation similar to that for creation of a filesystem. This task is accomplished with the **mkswap** command, which you can generally use by passing it nothing but the device identifier:

```bash
# mkswap /dev/hda7
```

This example turns `/dev/hda7` into swap space. To use the swap space, you must activate it with the **swapon** command:

```bash
# swapon /dev/hda7
```

To permanently activate swap space, you must create an entry for it in `/etc/fstab`, as described in Chapter 4.

## Maintaining Filesystem Health

Filesystems can become “sick” in a variety of ways. They can become overloaded with too much data, they can be tuned inappropriately for your system, or they can become corrupted because of buggy drivers, buggy utilities, or hardware errors. Fortunately, Linux provides a variety of utilities that can help you keep an eye on the status of your filesystems, tune their performance, and fix them.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_207_0.png)

Many of Linux's filesystem maintenance tools should be run when the filesystem is not mounted. Changes made by maintenance utilities while the filesystem is mounted can confuse the kernel's filesystem drivers, resulting in data corruption. In the following pages, I mention when utilities can and can't be used with mounted file systems.

## Tuning Filesystems

Filesystems are basically just big data structures—they're a means of storing data on disk in an indexed method that makes it easy to locate the data at a later time. Like all data structures, filesystems include design compromises. For instance, a design feature may enable you to store more small files on disk but might chew up disk space, thus reducing the total capacity available for storage of larger files. In many cases, you have no choice concerning these compromises, but some filesystems include tools that enable you to set filesystem options that affect performance. This is particularly true of ext2fs and the related ext3fs and ext4fs. Three tools are particularly important for tuning these filesystems: dumpe2fs, tune2fs, and debugfs. The first of these tools provides information about the filesystem, and the other two enable you to change tuning options.

### Obtaining Filesystem Information

You can learn a lot about your ext2 or ext3 filesystem with the dumpe2fs command. This command's syntax is fairly straightforward:

```
dumpe2fs [options] device
```

The device is the filesystem device file, such as /dev/hda2 or /dev/sdb7. This command accepts several options, most of which are rather obscure. The most important option is probably -h, which causes the utility to omit information about group descriptors. (This information is helpful in very advanced filesystem debugging but not for basic filesystem tuning.) For information about additional options, consult the man page for dumpe2fs.

Unless you're a filesystem expert and need to debug a corrupted filesystem, you're most likely to want to use dumpe2fs with the -h option. The result is about three dozen lines of output, each specifying a particular filesystem option, like these:

```
Last mounted on:       <not available>
Filesystem features:  has_journal filetype sparse_super
Filesystem state:     clean
Inode count:          657312
Block count:          1313305
Last checked:         Thu Jul  3 12:32:23 2008
Check interval:       15552000 (6 months)
```
