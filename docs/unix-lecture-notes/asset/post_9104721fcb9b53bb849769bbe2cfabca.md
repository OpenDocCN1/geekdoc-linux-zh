
```
total 0
crw-w---- 1 root     tty 136,  1 Oct 14 14:46 1
crw-w---- 1 lsmarque tty 136, 10 Sep 12 13:13 10
crw-w---- 1 lsmarque tty 136, 11 Sep 12 18:39 11
crw-w---- 1 chays   tty 136, 12 Sep 13 20:02 12
crw-w---- 1 chays   tty 136, 13 Sep 13 20:02 13
crw-w---- 1 lsmarque tty 136, 14 Oct  3 13:22 14
crw-w---- 1 lsmarque tty 136, 15 Sep 12 13:13 15
crw-w---- 1 shixon  tty 136, 19 Oct 14 15:19 19
crw-w---- 1 sweiss  tty 136, 20 Oct 14 15:23 20
```

Notice that the first line, which always reports the total number of blocks used by the files in the directory, shows that these files do not use any storage.

Next observe that the type designator of each file listed above is ‘c’, which represents the type character special file. The c indicates that this is a character device, as opposed to a block device. Every I/O device is accessed through either a block I/O interface or a character I/O interface. One major difference between them is that block I/O uses kernel buffering whereas character I/O does not. When a character I/O interface is used, the data flows in a character stream between the device and connected processes without using system buffers. In contrast, block devices use the kernel buffering system and transfer large chunks of data at a time. Some devices, such as disk partitions, may be accessed in block or character mode. Because each device file corresponds to a single access mode, devices that have more than one access mode have more than one device file.

Recall that the write command lets one user write to the terminal of another user, provided that the group write bit is set on the recipient’s pseudo-terminal device file. As a warm-up exercise, we will eventually write an implementation of write. First we will examine how device drivers work.

Notice in the listings of the /dev and /dev/pts directories that the size field consists of a pair of numbers. The first number is called the major device number and the second, the minor device number. For example, /dev/pts/12 has major device number 136 and minor device number 12. The major device number identifies the type of device, e.g., SCSI disk, pseudo-terminal, or mouse; the minor device number specifies which particular instance of this type of device is represented by the file, or the action associated with this particular interface to the device.

Each major device number is an index into the block or character device table maintained in the kernel. This table is used by the kernel to access the device drivers. Basically the table contains the address inside the kernel of the entry point into the device driver code. When a system call such as read() is invoked and the file descriptor passed to the read() system call is the file descriptor of a device file, the read() code ( inside the kernel) finds the i-node belonging to that descriptor. The i-node contains the type of the file, which will indicate that it is a device special file, and whether it is block or character. The kernel will look up the major and minor device numbers from inside the i-node. It will then use the major device number to locate the device driver code for the particular kind of device. For example, if the device file has major number 136 and is a character device file, it will search the character device table for index 136. An attempt to access /dev/pts/12 with major number 136 and minor number 12 will therefore result in execution of the driver whose index is 136.

> 6This is true in BSD and SunOS at least. In the Ext2 file system of Linux, there is more indirection, and the code that is executed might reside in a separate module. The device drivers are not necessarily part of a large executable image, but are instead in separate executable files, more like Windows, and the kernel contains stubs that are resolved dynamically at the time of the call, depending upon the type of file system on which the i-node resides.

numbers to devices. On many Linux systems, you can often find this mapping at

```
/usr/share/doc/kernel-doc-<kernel-version>/Documentation/devices.txt
```

where <kernel-version> is to be replaced by the version number, such as 2.6.9, as in

```
/usr/share/doc/kernel-doc-2.6.9/Documentation/devices.txt
```

If it is not there, then you can read the file /proc/devices, which contains the major device numbers for the various groups of devices.

Every I/O device with the same major device number uses the same driver. The minor device number is passed as a parameter to the device driver. The driver may use this number to select which unit of the device to use. Notice, for instance, that each of the pseudo-terminals in use in the above listing has the same major device number, 136, and a minor device number that corresponds to the name of the device file. As another example, if there are multiple disks, the minor device number would specify which disk is being accessed.

Sometimes the minor device number is used to distinguish different actions for the device to take. It is up to the device driver to decide how it will use the minor device number. The use of device numbers as indices into an array of drivers simplifies the customization of each system for the particular hardware configuration.

The device drivers in BSD UNIX, like the kernel itself, are divided into three sections:

- 1. Initialization and configuration routines
- 2. Routines to handle I/O service requests (upper half of the driver)
- 3. Interrupt service routines (lower half of the driver)

The lower half runs in an uninterruptible mode. The upper half runs synchronously and can block itself. They communicate through work queues. In Linux, although the terms "upper half" and "lower half" are not used explicitly, the device drivers work in a similar way. Sometimes they are called "master" and "slave" drivers.

## 4.3.4 Disk Drivers

An especially important group of drivers are the disk drivers. A disk driver is a software module that manages and controls the I/O that passes between a disk file and processes that have requested I/O to or from that file. This section briefly describes the role of disk drivers in handling I/O.

The purpose of a disk driver is to process requests for disk I/O. These requests are represented by transaction records, each of which consists of

- 1. a flag indicating whether to read or write data,
- 2. a primary memory address,
- 3. a secondary memory address, and
