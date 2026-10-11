# Tip

If you have a SCSI hard disk and a parallel-port Iomega Zip drive, I recommend building the Iomega parallel-port drivers as a module and the driver for your main SCSI host adapter into the kernel. This guarantees that the kernel won't become confused and try to boot from the Zip drive instead of the SCSI boot disk.

When you use a parallel-interfaced device, how you access the drive depends on the subvariety of interface used, SCSI or IDE. An Iomega Zip drive turns up as an ordinary SCSI device, whereas the IDE drives use special device files. The file /usr/src/linux/Documentation/paride.txt contains a script you can run to create appropriate device files, if they don't already exist on your system. (Most distributions include these device files.)

# Kernel Options for USB Drives

USB kernel options are changing rapidly with the 2.3.x Linux kernels, and will probably vary somewhat from what I describe here for the 2.4.x kernels. If you want to use USB devices with a 2.2.x kernel, you must use a very recent 2.2.x kernel or apply a set of patches to add USB support to the older kernel. Options relevant to USB removable disks include

+   USB drivers, Support for USB  This option is required to use any USB devices.

+   USB chipsets  Two USB low-level drivers exist, UHCI and OHCI. You must select whichever one is appropriate for your computer.

+   USB drivers, USB SCSI (mass storage)  This option includes support for some USB disk devices, treating them as if they were SCSI disks.

+   SCSI options  The Linux USB support for disk devices relies upon SCSI drivers, so you must activate SCSI drivers as if you were using a SCSI host adapter. You don't need to use drivers in the SCSI menu for any particular SCSI host adapter, however.

Linux kernel support for USB storage devices is weak in the 2.2.x and 2.3.x kernels, but is rapidly improving. With any luck, the support will be reliable early in the 2.4.x series kernels. For the latest information, check http://www.linux-usb.org/.

# Using Appropriate Device Files

To access a removable medium device, you normally mount it somewhere in the Linux filesystem using the mount command. For example, mount /dev/fd0 /mnt/floppy mounts a floppy disk at /mnt/floppy. You can also use these device files to create a filesystem on a