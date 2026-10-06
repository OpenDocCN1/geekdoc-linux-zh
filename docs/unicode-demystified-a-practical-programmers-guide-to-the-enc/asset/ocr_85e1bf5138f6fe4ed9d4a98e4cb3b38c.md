The common block devices on a Linux system are hard and floppy disks and CD-ROMs.

A character device is any device that is not a block device. Some examples of character devices are printers, terminals, tape drives, and modems.

The device driver for a character device determines how a program reads from and writes to the device. For example, the device driver for a terminal allows a program to read the information you type in the terminal in two ways. A program can read single characters from a terminal in raw mode (that is, without doing any interpretation of the characters). This mode has nothing to do with the raw device described in the following section. Alternatively, a program can read a line at a time. When a program reads a line at a, the driver handles the erase and kill characters so that the program never sees typing mistakes. In this case the program reads everything from the beginning of a line to the RETURN that ends a line; the number of characters in a line can vary.

# Raw Devices

Device driver programs for block devices usually have two entry points so they can be used in two ways: as block devices or character devices. The character device form of a block device is called a raw device. A raw device is characterized by

+   * Direct I/O (no buffering through the Linux kernel).
* A one-to-one correspondence between system calls and hardware requests.
* Device-dependent restrictions on I/O.

An example of a utility that uses a raw device is fck. It is more efficient for fck to operate on the disk as a raw device, not restricted by the fixed size of blocks in the block device interface. Because it has full knowledge of the underlying filesystem structure, fck can operate on the raw device by using the largest possible units. When a filesystem is mounted, processes normally access the disk through the block device interface. This explains why it is important to allow fck to modify only an unmounted filesystem. On a mounted filesystem there is the danger that, while fck is rearranging the underlying structure through the raw device, another process would change a disk block using the block device, resulting in a corrupted filesystem.

# Filesystems

Table 17-8 lists some of the types of filesystems available under GNU/Linux.