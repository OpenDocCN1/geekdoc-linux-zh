# Device Files (/dev)

Each hardware component (such as hard drive partitions, CD drives, printer, and mouse) existing in the system is represented as a file in the /dev directory.

The hardware components are addressed via these files by writing to or reading from one of these files. Two kinds of device files are included:

+   - Character-oriented device files (for devices working sequentially, such as printer, mouse, or tape drive)
+   - Block-oriented device files (such as floppy disks and hard drives)

The connection to device drivers in the kernel is implemented via numbered channels, which correspond to the number of the device driver in question. These are referred to as *major device numbers*.

A driver might be responsible for several devices of the same type. To distinguish between these devices, the *minor device number* is used.

Instead of the size of the files, these two numbers are displayed (the files do not occupy any space on the hard drive anyway):

```
da10:~ #    ls -l /dev/hda*
brw-rw---- 1 root disk 3, 0 Mar 22 06:12 /dev/hda
brw-rw---- 1 root disk 3, 1 Mar 22 06:12 /dev/hda1
```

In this example, the major device number 3 is listed for all files. This refers to the driver for IDE hard drives. The minor device numbers run from 1 to 15 (for SCSI hard drives) and up to 63 (for IDE hard drives) and refer to the various possible partitions.

Most device files are created dynamically by udev in /dev when the corresponding hardware is detected during the boot process. If udev does not create special device files for hardware, device files can be generated with the mknod command in the /lib/udev/devices/ directory. The necessary parameters must be provided by the hardware manufacturer. Device files in /lib/udev/devices/ are copied to /dev during the boot process.

The null device /dev/null is also located in this directory. Program output that would normally be sent to the screen can be redirected to this device (using redirects, for example). The redirected data will be deleted.