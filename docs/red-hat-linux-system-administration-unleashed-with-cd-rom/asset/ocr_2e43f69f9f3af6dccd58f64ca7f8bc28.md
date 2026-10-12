# Loopback Devices

Loopback devices allow you to create files and then treat them as a filesystem. For example, you can create an image of a floppy disk or create a CD-ROM image from a filesystem and then use the loopback device to mount it as a regular filesystem and make changes before committing the image to a disk or CD-R. The loopback device is also used in some of the available schemes for encrypting filesystems as outlined in the Loopback Encrypted Filesystem HOWTO, which can be found at http://www.linux.com/Loopback-Encrypted-Filesystem-HOWTO.html. In order to take advantage of the loopback device, you must have an up-to-date util-linux package. To determine the correct version to support your kernel, refer to the Changes file in the /usr/src/linux/Documentation directory.

# Support for Network Block Devices

An experimental option that can be selected under block devices is support for network block devices. Network block devices allow the client system to access a block device on a remote system transparently over TCP/IP. This is different from NFS or Coda in that the block devices accessed in this manner can be used for any type of filesystem, including swap devices.

# Linux Software RAID

One of the major features you can select under block devices is support for software RAID. This software RAID is fully described in Chapter 9 along with utilities required to manipulate RAID arrays under Linux.

# Parallel Port IDE Devices

Support for parallel port IDE devices is included here as well. This option allows you to use devices such as external hard drives and other IDE/ATAPI devices that connect to your computer via the parallel port. One caveat is that if you compile this option as a module, you must also compile the parport option as a module.

# Networking Options

Just like UNIX, Linux is a network operating system and the Linux system that stands alone is rare. Even the workstation in the home office is typically connected to the Internet via the PPP network protocol. A Linux workstation without network services is like a car on blocks. It has a powerful engine and lot's of cool buttons and knobs, but...