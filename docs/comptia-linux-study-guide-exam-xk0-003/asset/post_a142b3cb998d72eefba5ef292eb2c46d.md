
LVM also enables you to create a volume group from multiple partitions (known as *physical volumes* in LVM-speak), even across physical disks. This ability, which is similar to linear RAID, can help you create very large file systems—larger than any one disk supports. You can even stripe the volume group across multiple physical volumes, which can improve performance in a manner reminiscent of RAID 0.

Overall, LVM is a very useful tool on systems where storage needs are uncertain or likely to change. You can easily add disk space or rearrange how it’s allocated. LVM adds complexity, though, and if you create volume groups that span multiple disks, your data will become more vulnerable—if one disk fails, you may no longer be able to access any data from the volume group, even if it was actually stored on the good disk. You should also keep in mind that resizing a logical volume is useful only to the extent that you can resize the underlying file system. You can grow or shrink ReiserFS, ext2, ext3, and ext4 file systems; but JFS and XFS may only be grown, not shrunk. Swap space is best handled by using *swapoff* to disable it, resizing the logical volume, using *mkswap* to create a fresh swap area, and then reactivating it with *swapon*.

Ordinarily, a Linux system that uses LVM will still have at least one non-LVM partition. This partition holds the kernel so that your GRUB or Lilo boot loader can read it. Typically, */boot* is set aside for this purpose, although you can put the entire root (/) file system in a conventional partition, if you prefer. (In fact, you can use any mixture of conventional partitions and logical volumes that you like, so long as you can get the computer booted in some way.)

### Defining Physical Volumes

To implement an LVM, you begin by preparing your physical volumes—that is, your partitions. You should mark MBR partitions with the 0x8E partition type code using *fdisk*. If you use GNU Parted with MBR or GPT disks, set the LVM flag with the *set* command.

With the appropriate partition type code set, you can use the *pvcreate* command to set up the low-level physical volume data structures within a partition:

```
# pvcreate /dev/sda4
```

You can repeat this step with multiple partitions, if necessary.

Several additional commands, such as *pvdisplay*, *pvresize*, and *pvsplit*, enable you to perform further physical volume manipulations or to obtain data on your physical volumes.

### Defining Volume Groups

With one or more physical volumes defined, you can now create a volume group with the *vgcreate* command:

```
# vgcreate my_group /dev/sda4 /dev/sdb1
```

This command creates a volume group from */dev/sda4* and */dev/sdb1* and gives it the name *my_group*. If you already have a volume group and you want to extend it (say, with a new physical disk you’ve just added to the computer), you can do so with the *vgextend* command:

```
# vgextend my_group /dev/sdc1
```

This partition must have already been initialized with **pvcreate**. The **pvcreate** and **vgextend** commands both support a number of options; consult their man pages for details. Several additional commands, such as **vgremove**, **vgrename**, **vgdisplay**, **vgscan**, and **vgsplit**, enable you to view data about or manipulate your volume group. Consult these tools’ man pages for more information.

### Defining Logical Volumes

With your volume group created, you can begin creating logical volumes within it. This is done with the **lvcreate** command:

```bash
# lvcreate -i 3 -L 100G -n home my_group
```

This example creates a 100GB (-L 100G) logical volume called *home* (-n home) within the *my_group* volume group. This example is striped across three physical volumes (-i 3) for improved performance. You could omit the -i 3 option, but as a practical matter, you must specify the other options. The result of this command is a new Linux device file, /dev/mapper/my_group-home, which points to 100GB of disk space in the volume group. This device file may also be accessed as /dev/my_group/home, if you prefer.

Chances are you’ll want to run **lvcreate** multiple times to create several logical volumes—perhaps one each for /home, /usr, /usr/local, /var, and a few other filesystems that you might ordinarily put on separate partitions. If you use XFS or JFS, you may want to stop short of filling your volume group; that way, you’ll have unallocated space you can use to expand any logical volume if the need arises. With ReiserFS, ext2fs, ext3fs, or ext4fs, you can shrink an underutilized volume if you must make room for expanding another logical volume.

The **lvcreate** man page describes many more options for this command, but for the most part they’re very technical. There are also additional logical volume information and management commands, such as **lvdisplay**, **lvscan**, **lvresize**, and **lvremove**. Consult their man pages for more information.

### Working with Logical Volumes

Once your logical volumes are created, you can use them as if they were partitions: use their device filenames in place of partitions’ device filenames in commands such as **mkfs** and **mount**, and place references to these device filenames in */etc/fstab*. A logical volume can hold either a filesystem or swap space.

Non-Linux OSes can’t access Linux LVMs, so you shouldn’t use them to hold shared data on a computer that boots multiple OSes. There’s also little point in creating physical volumes on removable disks.

## Summary

Linux uses a unified filesystem, which means it doesn’t use drive letters as Windows does. Instead, partitions are mounted within a single directory structure, starting at the root (//) partition. You can create filesystems on partitions or removable disks, mount them, store files on them, and back them up individually or across partitions. You can mount partitions temporarily or create entries in /etc/fstab to make changes permanent, as you see fit. You might also want to create a RAID array or LVM configuration, which can improve reliability, speed, or flexibility.

## Exam Essentials

- **Summarize how Linux's filesystem (that is, its directory tree) is structured.** Linux's directory tree begins with the root ( / ) directory, which holds mostly other directories. Specific directories may hold specific types of information, such as user files in /home and configuration files in /etc. Some of these subdirectories and their subdirectories may in fact be separate partitions, which helps isolate data in the event of filesystem corruption.

- **Describe Linux's partitioning needs.** Linux requires a single root partition and generally uses a separate swap partition. Additional partitions, corresponding to directories such as /boot, /home, and /var, are desirable on some systems but aren't usually required.

- **Describe why you might pick particular filesystems for Linux installation.** Ext3fs is a popular choice and generally a good one. ReiserFS, XFS, and JFS are also good choices on distributions that support them, but many don't. The older ext2fs can be a good choice for small partitions but is better avoided for large partitions. The new ext4fs offers the advantages of many other filesystems.

- **Explain the operation of the mount command.** In its basic form, mount takes a device filename and directory and ties the two together so that files on the device may be accessed in the specified directory. A number of parameters and options can modify its function or how it treats the filesystem that it mounts.

- **Identify when swap space needs to be increased.** The output of the free command shows how much memory Linux is using—both RAM and swap space. When the amount of used swap space approaches available swap space, it's necessary to increase swap space or RAM.

- **Explain how Linux knows what partitions to mount when it boots.** Linux looks to the /etc/fstab file for information on the filesystems it should mount automatically (and perhaps some that it shouldn't mount automatically but that should be available for users to mount manually).

- **Know how to create a new filesystem on a disk or partition.** The mkfs program creates new filesystems on removable media drives or hard disk partitions. This program is actually a front-end to programs that do the actual work, such as mke2fs (aka mkfs.ext2 and mkfs.ext3) for ext2fs and ext3fs.

- **Describe how to check a filesystem for errors.** The fsck program checks a filesystem's internal consistency. Like mkfs, it's a front-end to filesystem-specific programs, such as e2fsck (aka fsck.ext2 and fsck.ext3) for ext2fs and ext3fs.
