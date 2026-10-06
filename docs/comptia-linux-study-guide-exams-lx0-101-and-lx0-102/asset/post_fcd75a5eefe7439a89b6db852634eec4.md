
# Configuring USB Devices

![](img/35f616c7eba4e79e12bfd762129c5d27_179_0.png)

If you have an older computer that lacks USB 3.0 support and you want to connect a high-speed USB 3.0 device, you can buy a separate USB 3.0 board. You can continue to use the computer's built-in USB ports for slower devices.

# Linux USB Drivers

Several USB controllers are available, with names as UHCI, OHCI, EHCI, and R8A6659. Modern Linux distributions ship the drivers for the common USB controllers enabled, so your USB port should be activated automatically when you boot the computer. The UHCI and OHCI controllers handle USB 1.x devices, but other controllers can handle USB 2.0 devices. You need a 2.6.31 or newer kernel to use USB 3.0 hardware. While these basics merely provide means to access the actual hardware and address the devices in a low-level manner. You will need additional software—either drivers or specialized software packages—to make practical use of the devices.

You can learn great about your devices by using the lsusb utility. A simple use of this program with no options reveals basic information about your USB devices:

```
$ lsusb
Bus 003 Device 008: ID 0686:400e Minolta Co., Ltd
Bus 003 Device 001: ID 0000:0000
Bus 002 Device 002: ID 046d:c401 Logitech, Inc. TrackMan Marble Wheel
Bus 002 Device 001: ID 0000:0000
```

In this example, three USB buses are detected (001, 002, and 003). The first bus has no devices, but the second and third have one device—a Logitech TrackMan Marble Wheel trackball and a Minolta DIMAGE Scan 5400 scanner. The scanner's name isn't fully identified by this output, except as the ID number indicates. You can gather additional information by using various options to lsusb:

- **Verbose** The -v option produces extended information about each product.
- **Restrict Bus and Device** Using the -s [[bus]:[devnum]] option restricts output to the specified bus and device number.
- **Restrict Vendor and Product** You can limit output to a particular vendor and product by using the -d [vendor]:[product] option. The *vendor* and *product* are the codes after ID on each line of the *lsusb*.
- **Display by Filename** Using -O *filename* displays information about the device's accessible via *filename*, which should be a file in the /proc/bus/usb device tree. This directory provides a low-level interface to USB devices, as described.
- **Tree View** The -t option displays the device list as a tree so that you can more easily what devices are connected to specific controllers.
- **Version** The -V or --version option displays the version of the lsusb utility and exits.

# 126 Chapter 3 • Configuring Hardware

Early USB implementations required a separate driver for every USB device. Many of these devices remain in the kernel, and some software relies on them. For instance, USB disk storage devices use USB storage devices that interface with Linux's SCSI support, making USB hard drives, removable disks, and so on look like SCSI devices.

Linux provides a USB filesystem that provides access to USB devices in a generic manner. This filesystem appears as part of the /proc virtual filesystem. In particular, USB device information is accessible from /proc/bus/usb. Subdirectories of /proc/bus/usb are given numbered names based on the USB controllers installed on the computer, as in /proc/bus/usb/001 for the first USB controller. Software can access files in these directories rather than device files in /dev as most hardware devices. Tools such scanner and the Linux printing system can automatically locate compatible USB devices and use.

# USB Manager Applications

USB can be challenging for OSes because it was designed as a hot-plugable technology. The Linux kernel wasn't originally designed with this sort of activity in mind, so the kernel relies on external utilities to manage them. Two tools in particular are useful for managing USB devices: usbmgr and hotplug.

The usbmgr package (located at http://freecode.org/projects/usbmgr) is a program that runs in kernel to detect changes on the bus. When it detects, it loads or unloads the kernel modules that are required to handle the devices. For instance, if you plug in a USB drive, usbmgr load the necessary USB and SCSI modules. This package uses configuration files in /etc/usbmgr to manage specific devices and /etc/usbmgr/usbmgr.conf to control the overall configuration.

With the shift from in-kernel device-specific USB drivers to the USB device filesystem (/proc/bus/usb), usbmgr has been declining in importance. In fact, it may not be installed on your system. Instead, most distributions rely on Hotplug package (http://linux-hotplug.sourceforge.net), which has kernel support added with the 2.4.x kernel series. This system uses files stored in /etc/hotplug/usb.rules contains a database of specific device IDs and pointers to scripts in /etc/hotplug/usb that run when devices are plugged in or unplugged. These might change permissions on device files so that ordinary users can access USB hardware, run commands to detect new USB devices, or otherwise prepare the system for the.

# Configuring Disks

Hard disks are among the most important components in your system. Early USB implementations required a separate driver for every USB device. Many of these devices remain in the kernel, and some software relies on them. For instance, USB disk storage devices use USB storage devices that interface with Linux's SCSI support, making USB hard drives, removable disks, and so on look like SCSI devices.

Linux provides a USB filesystem that provides access to USB devices in a generic manner. This filesystem appears as part of the /proc virtual filesystem. In particular, USB device information is accessible from /proc/bus/usb. Subdirectories of /proc/bus/usb are given numbered names based on the USB controllers installed on the computer, as in /proc/bus/usb/001 for the first USB controller. Software can access files in these directories rather than device files in /dev as most hardware devices. Tools such scanner and the Linux printing system can automatically locate compatible USB devices and use.

USB can be challenging for OSes because it was designed as a hot-plugable technology. The Linux kernel wasn't originally designed with this sort of activity in mind, so the kernel relies on external utilities to manage them. Two tools in particular are useful for managing USB devices: usbmgr and hotplug.

The usbmgr package (located at http://freecode.org/projects/usbmgr) is a program that runs in kernel to detect changes on the bus. When it detects, it loads or unloads the kernel modules that are required to handle the devices. For instance, if you plug in a USB drive, usbmgr load the necessary USB and SCSI modules. This package uses configuration files in /etc/usbmgr to manage specific devices and /etc/usbmgr/usbmgr.conf to control the overall configuration.

With the shift from in-kernel device-specific USB drivers to the USB device filesystem (/proc/bus/usb), usbmgr has been declining in importance. In fact, it may not be installed on your system. Instead, most distributions rely on Hotplug package (http://linux-hotplug.sourceforge.net), which has kernel support added with the 2.4.x kernel series. This system uses files stored in /etc/hotplug/usb.rules contains a database of specific device IDs and pointers to scripts in /etc/hotplug/usb that run when devices are plugged in or unplugged. These might change permissions on device files so that ordinary users can access USB hardware, run commands to detect new USB devices, or otherwise prepare the system for the.

# Configuring PATA

PATA disks once ruled the roost, but today SATA disks have largely supplanted them. Thus, PATA disks are still available, though.

As the full name implies, PATA disks use a parallel interface, meaning several bits of data are transferred over the cable at once. Thus, PATA disks are wide, supporting a total of 48 bits, depending on the variant.

PATA disks must be configured as masters or slaves. This can be done via jumpers on the disks. Typically, the master device sits at the end of the cable, and the slave device resides on the middle. All modern PATA disks also support an option called select. When you set this option, the drive configures itself based on its position. Your easiest configuration is to set all PATA devices to the select-cable; you can then attach them to whatever position is convenient, and the drives configure themselves.

For performance, disks should be placed on separate controllers rather than master and slave on a single controller, because each PATA controller has a limited throughput that may be exceeded by two drives. Until recently, most motherboards had at least two controllers, so putting each drive on its own controller is not a problem until you install more than two drives.

In Linux, PATA disks have traditionally been identified as /dev/hda, /dev/hdb, and so, with /dev/hda being the master on the first controller, /dev/hdb being the slave on the first controller. Thus, gaps can occur in the numbering scheme—if you have master disks on the first and second controllers but no slave disks, your system will contain /dev/hda and /dev/hdc instead of /dev/hdc. Partitions are identified after the main name, as in /dev/sda1, /dev/hda2, and so on.

The naming rules for disks also apply to optical media, except that these media typically are not partitioned. Most Linux distributions also create a link to your optical drive under the name /dev/cdrom or /dev/dvd. Removable PATA disks, such as Zip disks, are given identifiers if they were fixed PATA disks, optionally including partition identifiers.

Most modern Linux distributions favor fewer PATA drives that treat PATA disks as if they were SCSI disks. Thus, you may find that your drive filenames follow the SCSI rules rather than the PATA rules even if you have PATA disks.

![](img/35f616c7eba4e79e12bfd762129c5d27_181_0.png)
