
8. For each of the umasks in Question 7, list the umasks that are reasonable to use to increase security on your Linux system and explain why.

9. Starting from the Linux default permissions for file and directories, what umask would you use to ensure that for all new:
   - a. directories, the owner would have read, write, and execute; members of the group would have read and execute; and others would have read
   - b. files, the owner would have read and execute; the group would have read, write, and execute; and others would have execute
   - c. files, the owner would have write; the group would have read, write, and execute; and others would have read and write
   - d. directories, the owner would have read, write, and execute; the group would have read, write, and execute; and others would have read, write, and execute
   - e. directories, the owner would have execute; the group would have read, write, and execute; and others would have no permissions
   - f. files, the owner would have read and write; the group would have no permissions; and others would have write
   - g. directories, the owner would have read, write, and execute; the group would have read; and others would have read and execute
   - h. directories, the owner would have write; the group would have read, write, and execute; and others would have read, write, and execute
   - i. files, the owner would have no permissions; the group would have no permissions; and others would have no permissions

10. What chmod command would you use to impose the following permissions?
   - a. on a directory such that: the owner would have read, write, and execute; the group would have read and execute; and others would have read
   - b. on a file such that: the owner would have read and write; the group would have no permissions; and others would have write
   - c. on a file such that: the owner would have write; the group would have read, write, and execute; and others would have read and write
   - d. on a file such that: the owner would have read and execute; the group would have read, write, and execute; and others would have execute
   - e. on a directory such that: the owner would have execute; the group would have read, write, and execute; and others would have no permissions
   - f. on a directory such that: the owner would have write; the group would have read, write, and execute; and others would have read, write, and execute
   - g. on a directory such that: the owner would have read, write, and execute; the group would have read; and others would have read and execute
   - h. on a directory such that: the owner would have read, write, and execute; the group would have read, write, and execute; and others would have read, write, and execute
   - i. on a file such that: the owner would have no permissions; the group would have no permissions; and others would have no permissions

## Linux Filesystem Administration

After completing this chapter, you will be able to:

- Identify the structure and types of device files in the /dev directory
- Understand common filesystem types and their features
- Mount and unmount filesystems to and from the Linux directory tree
- Create and manage filesystems on floppy disks, CDs, DVDs, USB storage devices, Firewire storage devices, and hard disk partitions
- Create and use ISO images
- Use the LVM to create and manage logical volumes
- Monitor free space on mounted filesystems
- Check filesystems for errors
- Use hard disk quotas to limit user space usage

**Navigating the Linux directory tree and manipulating files are common tasks** that are performed on a daily basis by all users. However, administrators must provide this directory tree for users, as well as manage and fix the disk devices that support it. In this chapter, you learn about the various device files that represent disk devices and the different filesystems that can be placed on those devices. Next, you learn how to create and manage filesystems on a wide variety of different storage devices, as well as learn standard hard disk partitioning, LVM configuration, and filesystem management. The chapter concludes with a discussion of disk usage, filesystem errors, and restricting the ability for users to store files.

### The /dev Directory

Fundamental to administering the disks used to store information is an understanding of how these disks are specified by the Linux operating system. Most devices on a Linux system (such as disks, terminals, and serial ports) are represented by a file on the hard disk called a device file. There is one file per device, and these files are typically created by the udev system and found in the /dev directory. This allows you to specify devices on the system by using the pathname to the file that represents it in the /dev directory.

Perhaps the simplest example of a disk device is a floppy disk, which was primarily used on legacy Linux systems to transfer small amounts of data before the advent of USB flash drives. To specify the first floppy disk in the Linux system, you can type the pathname /dev/fd0 (floppy disk 0) in the appropriate section of a command, and to represent the second floppy disk in the Linux system, you can specify the pathname to the file /dev/fd1 (floppy disk 1).

Furthermore, each device file specifies how data should be transferred to and from the device. You have two methods for transferring data to and from a device. The first method involves transferring information character-by-character to and from the device. Devices that transfer data in this fashion are referred to as character devices. The second method transfers chunks or blocks of information at a time by using physical memory to buffer the transfer. Devices that use this method of transfer are called block devices; they can transfer information much faster than character devices. Device files that represent disks, such as floppy disks, CDs, DVDs, USB flash drives, and hard disks, are typically block device files because a fast data transfer rate is preferred. Tape drives and most other devices, however, are typically represented by character device files.

To see whether a particular device transfers data character-by-character or block-by-block, recall that the `ls -l` command displays a c or b character in the type column indicating the type of device file. To view the type of the file /dev/fd0, you can use the following command:

```bash
[root@server1 ~]# ls -l /dev/fd0
brw-rw---- 1 root floppy 2, 0 Feb 23 16:02 /dev/fd0
[root@server1 ~]#
```

![](img/c27875544958897d817484d558c208c8_217_0.png)

Floppy disk drives are not standard on newer computers today. As a result, Fedora 20 does not load the floppy driver and create the /dev/fd0 device file by default. To load the floppy driver manually (which also creates the /dev/fd0 device file), you can type `modprobe floppy` at a command prompt as the root user.

| Device File | Description | Block or Character |
| :--- | :--- | :--- |
| /dev/fd0 | First floppy disk on the system | Block |
| /dev/fd1 | Second floppy disk on the system | Block |
| /dev/hda1 | First primary partition on the first PATA hard disk drive (primary master) | Block |
| /dev/hdb1 | First primary partition on the second PATA hard disk drive (primary slave) | Block |
| /dev/hdc1 | First primary partition on the third PATA hard disk drive (secondary master) | Block |
| /dev/hdd1 | First primary partition on the fourth PATA hard disk drive (secondary slave) | Block |
| /dev/sda1 | First primary partition on the first SATA/SCSI hard disk drive | Block |
| /dev/sdb1 | First primary partition on the second SATA/SCSI hard disk drive | Block |
| /dev/loop0 | First loopback interface | Block |
| /dev/tty1 | First local terminal on the system (Ctrl+Alt+F1) | Character |
| /dev/tty2 | Second local terminal on the system (Ctrl+Alt+F2) | Character |
| /dev/ttyS0 | First serial port on the system (COM1) | Character |
| /dev/ttyS1 | Second serial port on the system (COM2) | Character |
| /dev/psaux | PS/2 mouse port | Character |
| /dev/lp0 | First parallel port on the system (LPT1) | Character |
| /dev/null | Device file that represents nothing; any data sent to this device is discarded | Character |
| /dev/st0 | First SCSI tape device in the system | Character |
| /dev/bus/usb/* | USB device files | Character |

**Table 5-1 Common device files**

From the leftmost character in the preceding output, you can see that the /dev/fd0 file is a block device file. Table 5-1 provides a list of some common device files that you may find on your Linux system and their types.

After a typical Fedora Linux installation, you will find several hundred different device files in the /dev directory that represent devices on the system. This large number of device files on a Linux system does not require much disk space because all device files consist of inodes and no data blocks; as a result, the entire contents of the /dev directory is usually less than 100 kilobytes in size. When using the `ls -l` command to view device files, the portion of the listing describing the file size in kilobytes is replaced by two numbers: the major number and the minor number. The major number of a device file points to the device driver for the device in the Linux kernel; several different devices can share the same major number if they are of the same general type (that is, two different floppy disk drives might share the same major number). The minor number indicates the particular device itself; the first floppy disk drive in the computer will have a different minor number than the second floppy disk drive in the
