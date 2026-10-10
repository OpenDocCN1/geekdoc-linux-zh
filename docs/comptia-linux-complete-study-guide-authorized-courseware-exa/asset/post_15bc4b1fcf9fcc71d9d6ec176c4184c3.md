
In this example, three USB buses are detected (*001*, *002*, and *003*). The first bus has no devices attached, but the second and third each have one device—a Logitech TrackMan Marble Wheel trackball and a Minolta DiMAGE Scan Elite 5400 scanner, respectively. (The scanner's name isn't fully identified by this output, except *s100a* as the ID number encodes this information.) You can gather additional information by using various options to `lsusb`:

- **Be verbose**: The `-v` option produces extended information about each product.
- **Restrict bus and device number**: Using the `-s [bus]:[devnum]` option restricts output to the specified bus and device number.
- **Restrict vendor and product**: You can limit output to a particular vendor and product by using the `-d [vendor]:[product]` option. The *vendor* and *product* are the codes just after ID on each line of the basic `lsusb` output.
- **Display device by filename**: Using `-D filename` displays information about the device that's accessible via *filename*, which should be a file in the `/proc/bus/usb` directory tree. This directory provides a low-level interface to USB devices, as described shortly.
- **Tree view**: The `-t` option displays the device list as a tree, so that you can more easily see what devices are connected to specific controllers.
- **Version**: The `-V` or `--version` option displays the version of the `lsusb` utility and exits.

Early Linux USB implementations required a separate driver for every USB device. Many of these drivers remain in the kernel, and some software relies on them. For instance, USB disk storage devices use USB storage drivers that interface with Linux's SCSI support, making USB hard disks, removable disks, and so on like SCSI devices.

Linux is migrating toward a model in which a USB filesystem provides access to USB devices. This filesystem appears as part of the /proc virtual filesystem. In particular, USB device information is accessible from `/proc/bus/usb`. Subdirectories of `/proc/bus/usb` are given numbered names based on the USB controllers installed on the computer, as in `/proc/bus/usb/001` for the first USB controller. Software can access files in these directories to control USB devices rather than use device files in `/dev` as with most hardware devices.

## USB Manager Applications

USB can be challenging for OSs because it was designed as a hot-pluggable technology. The Linux kernel wasn't originally designed with this sort of activity in mind, so the kernel relies on external utilities to help manage matters. Two tools in particular are used for managing USB devices: **usbmgr** and **hotplug**.

The `usbmgr` package (located at `http://freesheet.net/projects/usbmgr/`) is a program that runs in the background to detect changes on the USB bus. When it detects changes, it loads or unloads the kernel modules that are required to handle the devices. For instance, if you plug in a USB Zip drive, `usbmgr` will load the necessary USB and SCSI disk modules. This package uses configuration files in `/etc/usbmgr` to handle specific devices and `/etc/usbmgr/usbmgr.conf` to control the overall configuration.

With the shift from in-kernel device-specific USB drivers to the USB device filesystem `/proc/bus/usb`, **usmgr** has been declining in importance. In fact, it may not be installed on your system. Instead, most distributions rely on the Hotplug package (<http://linux-hotplug.sourceforge.net>), which relies on kernel support added with the 2.4.x kernel series. This system uses files stored in `/etc/hotplug` to control the configuration of specific USB devices. In particular, `/etc/hotplug/usb.usermap` contains a database of USB device IDs and pointers to scripts in `/etc/hotplug/usb` that are run when devices are plugged in or unplugged. These scripts might change permissions on USB device files so that ordinary users can access USB hardware, run commands to detect new USB disk devices, or otherwise prepare the system for a new (or newly removed) USB device.

## Configuring Hard Disks

Hard disks are among the most important components in your system. Three different hard disk interfaces are common on modern computers: *Parallel Advanced Technology Attachment* (PATA), a.k.a. ATA; *Serial Advanced Technology Attachment* (SATA); and *Small Computer System Interface* (SCSI). In addition, external USB and IEEE-1394 drives are available, as well as external variants of SATA and SCSI drives. Each has its own method of low-level configuration.

### Configuring PATA Disks

PATA disks once ruled the roost in the x86 PC world, but today they’re fast giving way to SATA disks. Thus, you’re most likely to encounter PATA disks on slightly older computers—say, from 2005 or earlier. PATA disks are still readily available, though, and PATA is still used even in some new computers, particularly for CD-ROM and DVD-ROM drives.

As the full name implies, PATA disks use a parallel interface, meaning that several bits of data are transferred over the cable at once. Thus, PATA cables are wide, supporting a total of either 40 or 80 lines, depending on the variety of PATA. You can connect up to two devices to each PATA connector on a motherboard or plug-in PATA controller, meaning that PATA cables typically have three connectors—one for the motherboard and two for disks.

PATA disks must be configured as masters or as slaves. This can be done via jumpers on the disks themselves. Typically, the master device sits at the end of the cable and the slave device resides on the middle connector. All modern PATA disks also support an option called cable select. When set to this option, the drive attempts to configure itself automatically based on its position on the PATA cable. Thus, your easiest configuration is usually to set all PATA devices to use the cable-select option; you can then attach them to whatever position is convenient, and the drives should configure themselves.

For best performance, disks should be placed on separate controllers rather than configured as master and slave on a single controller, because each PATA controller has a limited throughput that may be exceeded by two drives. Until recently, most motherboards have included at least two controllers, so putting each drive on its own controller isn't a problem until you install more than two drives in a single computer.

All but the most ancient BIOSs auto-detect PATA devices and provide information about their capacities and model numbers in the BIOS setup utilities. Until recently, most motherboards would boot PATA drives in preference to other drives, although BIOSs have also often provided options to change this preference in favor of SCSI drives. Thus, in a mixed-drive setup, you may have to place your boot loader on a PATA drive.

In Linux, PATA disks have traditionally been identified as /dev/hda, /dev/hdb, and so on, with /dev/hda being the master drive on the first controller, /dev/hdb being the slave drive on the first controller, and so on. Thus, gaps can occur in the numbering scheme—if you've got master disks on the first and second controllers but no slave disks, your system will contain /dev/hda and /dev/hdc, but no /dev/hbd. Partitions are identified by numbers after the main device name, as in /dev/hda1, /dev/hda2, and so on.

The naming rules for disks also apply to optical media, except that these media aren't typically partitioned. Most Linux distributions also create a link to your optical drive under the name /dev/cdrom or /dev/dvd. Removable PATA disks, such as Zip disks, are given identifiers as if they were fixed PATA disks, optionally including partition identifiers.

Recently, Linux drivers have appeared that treat PATA disks as if they were SCSI disks. Thus, you may find that your device filenames follow the SCSI rules rather than the PATA rules even if you have PATA disks.

### Configuring SATA Disks

SATA is a newer interface than PATA, but SATA is rapidly displacing PATA as the interface of choice. New motherboards typically host four or more SATA interfaces, often at the expense of PATA interfaces.

SATA disks connect to their motherboards or controllers on a one-to-one basis—unlike PATA, you can't connect more than one disk to a single cable. This fact simplifies configuration; there typically aren't jumpers to set, and you needn't be concerned with the position of the disk on the cable.

As the word serial in the expansion of SATA implies, SATA is a serial bus—only one bit of data can be transferred at a time. SATA transfers more bits per unit time on its data line, though, so SATA is faster than PATA (150–750 MB/s for SATA vs. 16–133 MB/s for PATA; but these are theoretical maximums that are unlikely to be achieved in real-world situations). Because of SATA's serial nature, SATA cables are much thinner than PATA cables.

Modern BIOSs detect SATA disks and provide information about them just as they do for PATA disks. The BIOS may provide boot order options, too. Older BIOSs are likely to be more limited. This is particularly true if your motherboard doesn't provide SATA support but you use a separate SATA controller card. You may be able to boot from an SATA disk in such cases if your controller card supports this option, or you may need to use a PATA boot disk.
