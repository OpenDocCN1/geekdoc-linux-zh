|Device File|Description|Block or Character|
|/dev/fd0|First floppy disk on the system|Block|
|/dev/fd1|Second floppy disk on the system|Block|
|/dev/hda1|First primary partition on the first PATA hard disk drive (primary master)|Block|
|/dev/hdb1|First primary partition on the second PATA hard disk drive (primary slave)|Block|
|/dev/hdc1|First primary partition on the third PATA hard disk drive (secondary master)|Block|
|/dev/hdd1|First primary partition on the fourth PATA hard disk drive (secondary slave)|Block|
|/dev/sda1|First primary partition on the first SATA/SCSI hard disk drive|Block|
|/dev/sdb1|First primary partition on the second SATA/SCSI hard disk drive|Block|
|/dev/loop0|First loopback interface|Block|
|/dev/tty1|First local terminal on the system (Ctrl+Alt+F1)|Character|
|/dev/tty2|Second local terminal on the system (Ctrl+Alt+F2)|Character|
|/dev/ttyS0|First serial port on the system (COM1)|Character|
|/dev/ttyS1|Second serial port on the system (COM2)|Character|
|/dev/psaux|PS/2 mouse port|Character|
|/dev/lp0|First parallel port on the system (LPT1)|Character|
|/dev/null|Device file that represents nothing; any data sent to this device is discarded|Character|
|/dev/st0|First SCSI tape device in the system|Character|
|/dev/bus/usb/*|USB device files|Character|

# Table 5-1 Common device files

From the leftmost character in the preceding output, you can see that the /dev/fd0 file is a block device file. Table 5-1 provides a list of some common device files that you may find on your Linux system and their types.

After a typical Fedora Linux installation, you will find several hundred different device files in the /dev directory that represent devices on the system. This large number of device files on a Linux system does not require much disk space because all device files consist of inodes and no data blocks; as a result, the entire contents of the /dev directory is usually less than 100 kilobytes in size. When using the ls -l command to view device files, the portion of the listing describing the file size in kilobytes is replaced by two numbers: the major number and the minor number. The major number of a device file points to the device driver for the device in the Linux kernel; several different devices can share the same major number if they are of the same general type (that is, two different floppy disk drives might share the same major number). The minor number indicates the particular device itself; the first floppy disk drive in the computer will have a different minor number than the second floppy disk drive in the