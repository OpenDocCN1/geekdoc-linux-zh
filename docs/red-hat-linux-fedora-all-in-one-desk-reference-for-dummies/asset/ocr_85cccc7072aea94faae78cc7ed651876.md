You don't really have to know much about the device files and the device numbers, except to be aware of their existence.

# Block devices

The first letter in the listing of a device file also provides an important clue. For the /dev/hda device, the first letter is a b, which indicates that /dev/hda is a block device — one that can accept or provide data in chunks (typically 512 bytes or 1KB). By the way, /dev/hda refers to the first IDE hard drive on your system (the C drive in Windows). Hard drives, floppy drives, and CD-ROM drives are all examples of block devices.

# Character devices

If the first letter in the listing of a device file is a c, then the device is a character device — one that can receive and send data one character (one byte) at a time. For example, the serial ports and parallel port are character devices. To see the specific listing of a character device, type the following command in a terminal window:

```
ls -l /dev/ttyS0
```

The listing of this device should be similar to the following:

```
crw-rw--- 1 root uucp 4, 64 Jul 23 14:50 /dev/ttyS0
```

Notice that the very first letter is a c because /dev/ttyS0 — the first serial port — is a character device.

# Network devices

Network devices that enable your system to interact with a network — for example, Ethernet and dial-up point-to-point protocol (PPP) connections — are somewhat special because they need no file to correspond to the device. Instead, the kernel uses a special name for the device. For example, the Ethernet devices are named eth0 for the first Ethernet card, eth1 for the second one, and so on. PPP connections are named ppp0, ppp1, and so on.

Because network devices aren't mapped to device files, there are no files corresponding to these devices in the /dev directory.

# Managing Loadable Driver Modules

To use any device, the Linux kernel must contain the driver. If the driver code is linked into the kernel as a monolithic program (a program that's in the form of a single large file), then adding a new driver means rebuilding