tty* virtual terminals in text mode
ttyp* terminal slaves under X
tsys* serial interfaces

Some devices have a special function: thus, /dev/null serves as a 'black hole' where data can be placed and made to disappear for good (for example, to-route command output that is not to be displayed). /dev/zero is an inexhaustible source of 0-bytes, which is sometimes used to fill files with zeros until they reach a specific size.

If you can access specific devices only as root, a likely cause is that only root has access privileges for the device in question. To allow other users access to these devices, you can register them in /etc/group in the group to which the device belongs (you can determine this with ls -l /dev/...). On single user systems, you can also open up access with chmod +rw device- however this will create a safety gap!

In older Linux systems, serial interfaces were addressed via the device files /dev/cua*. Since kernel version 2.2, these devices no longer exist, and the device name tty* (which has been around as an alternative for quite some time) must be used.

You will find a complete description of all devices currently known in Linux, together with their device numbers, in the file /usr/src/linux/Documentation/devices.txt.

# Information about process administration in the /proc directory

Information about processes is managed by Linux internally. In order to offer users easy access to such data, the process administration information is mapped in the /proc directory: each process is assigned its own subdirectory in /proc. This process directory contains some files with various management data.

| Important /proc files |
| /proc/bus/pci* | PCI information (kernel 2.2) |
| /proc/cpuinfo | CPU information |
| /proc/ide* | IDE drives and controllers |
| /proc/interrupts | interrupt usage |
| /proc/ports | I/O port usage |
| /proc/ndstat | RAID state |
| /proc/modules | active modules |
| /proc/net* | network state and usage |
| /proc/partitions | hard disk partitions |
| /proc/pci | PCI informationen (kernel 2.0) |
| /proc/scsi* | SCSI drives and controllers |