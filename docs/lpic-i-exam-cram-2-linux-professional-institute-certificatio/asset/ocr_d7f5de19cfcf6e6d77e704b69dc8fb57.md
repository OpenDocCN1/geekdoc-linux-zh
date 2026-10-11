A quick way to see whether the USB drivers are loaded properly is to run `lsmod` and see whether they show up in the output. If they are present, and other devices are dependent on them, this is shown in the rightmost column.

Linux and USB have a different relationship from other operating systems and USB. For example, every object on a Linux system is a file and everything that is organized under a single path hierarchy. This leads to the next point, that USB devices are organized under a USB device file system that appears under the /proc abstracted file system.

The USB device file system is usually mounted at system initialization on /proc/bus/usb. This directory always contains two subdirectories called /drivers and /devices. When a device is attached to the file system, the first device is numbered 001, then 002, and so on.

# # USB and Storage Devices

USB storage devices (such as detachable hard disk enclosures) show up as SCSI devices in the configuration for the system because they could be any type of device and the SCSI drivers present the most flexible set of options.

Run the mount command string to search the output for the characters usb:

```
mount | grep usb
```

This shows the following output:

```
usbdevfs on /proc/bus/usb type usbdevfs (rw)
```

The output shows the USB device file system mounted at the expected location. Other commands you can use to view USB devices include scsi_info, which is designed to enumerate both SCSI and USB devices. For example, if a mass storage device such as a disk is located on /dev/sda, you would use the following command:

```
scsi_info /dev/sda
```

In addition, if the device were a storage device, you could use fdisk -1 to see which /dev file it was mapped to. Then you can either map it manually or insert it as an entry in the /etc/fstab file.

Finally, for the graphically oriented crowd, you can use the usbview command, which shows the USB devices and configuration in a two-paned view.