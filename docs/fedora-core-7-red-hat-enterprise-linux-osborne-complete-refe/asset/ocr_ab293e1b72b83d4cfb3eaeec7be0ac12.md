# Device Types

Linux implements several types of devices, the most common of which are block and character. A block device, such as a hard disk, transmits data a block at a time. A character device, such as a printer or modem, transmits data one character at a time, or rather as a continuous stream of data, not as separate blocks. Device driver files for character devices have a c as the first character in the permissions segment displayed by the ls command. Device driver files for block devices have a b. In the next example, lpo (the printer) is a character device and sda1 (the hard disk) is a block device:

```
# ls -1 sda1 lp0
brw-rw---- 1 root disk 3, 1 Jan 30 02:04 sda1
crw-rw---- 1 root lp  6, 0 Jan 30 02:04 lp0
```

The device type can be either b, c, p, or u. As already mentioned, the b indicates a block device, and c is for a character device. The u is for an unbuffered character device, and the p is for a FIFO (first in, first out) device. Devices of the same type often have the same name; for example, serial interfaces all have the name ttyS. Devices of the same type are then uniquely identified by a number attached to the name. This number has two components: the major number and the minor number. Devices may have the same major number, but if so, the minor number is always different. This major and minor structure is designed to deal with situations in which several devices may be dependent on one larger device, such as several modems connected to the same I/O card. All the modems would have the same major number that references the card, but each modem would have a unique minor number. Both the minor and major numbers are required for block and character devices (b, c, and u). They are not used for FIFO devices, however.

Valid device names along with their major and minor numbers are listed in the devices.txt file located in the /Documentation directory for the kernel source code, /usr/src/linux-xyz/Documentation. When you create a device, you use the major and minor numbers as well as the device name prefix for the particular kind of device you are creating. Most of these devices are already created for you and are listed in the /etc/dev directory.

# MAKEDev

You use MAKEDev to create device files. MAKEDev uses device configuration files located in the /etc/makedev.d directory to determine device options like the major or minor number of the device or any symbolic links that should be created for it. For example, the /etc/makedev.d/01sound file lists sound devices. A MAKEDev configuration file can have three different kinds of records, each beginning with a different operator:

+   - **b or c** Create a block (b) or character (c) device. These entries hold several options: mode (permissions), owner, group, major and minor numbers, inc, count (number of devices created), and fmt (the name of the device). The fmt option is technically a format string, which can include a format specifier for numerically incrementing names of the similar devices, such as cdrm%fd for cdrm0, cdrm1, and so on. The inc option sets an increment.

+   - **l** Creates a symbolic link for a device.

+   - **a** An alias applies the commands used for one device for those of another. This lets you create a sound device, which in turn automatically creates audio, midi, and mixer devices, and so on.