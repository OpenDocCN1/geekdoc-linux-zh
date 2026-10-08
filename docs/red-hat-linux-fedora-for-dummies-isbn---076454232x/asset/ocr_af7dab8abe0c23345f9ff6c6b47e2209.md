The button indicates whether the file system is mounted or unmounted. After a few seconds, the button changes from Unmount to Mount to show that it has been unmounted.

+   3. **Click the Exit button to close the utility.**

The file system is unmounted. If the file system is a removable type, such as a floppy disk or CD, you can remove it. Otherwise, the file system is simply not available for use until you remount it.

![](bbox=[0.13, 0.28, 0.2, 0.36])

You can run the `eject` command from a bash shell to eject a CD. You have to unmount the CD first and then enter the `eject` command. Otherwise, to eject a CD, you must unmount it and then press the eject button on the CD-ROM drive. In either case, you can’t eject the CD until you have unmounted it.

# # Adding a Disk Drive

Sooner or later, life catches up with us and you’re likely to need or want a bigger house or car or diamond in your tooth, or whatever. The same goes for disk space, in which case you want to add another disk drive.

The first step to increasing your drive space is to add a new storage device. It can be a hard drive (IDE or SCSI), but also a USB or FireWire memory stick. These steps describe the general process of adding a storage device and then formatting and mounting it:

+   1. **Install the hard drive or insert the USB or FireWire device.**

If the device is an IDE or SCSI hard drive, turn off the power to your computer and monitor. Unplug the power cable and open the computer case. (Don’t cut yourself on the sometimes sharp metal edges when reaching into the computer.) Use the antistatic strap that comes with the hard drive; follow the instructions included with the strap.

Most PCs use IDE controllers. SCSI-based PCs are more expensive and aren’t commonly found in consumer PCs; these types are more common in the commercial realm. IDE-based PCs have two IDE controllers. Each device can control as many as two IDE devices. Ribbon cables connect the controller to the devices.

You have to configure your new disk to function as a slave device if it’s connected to a ribbon cable or IDE controller that already has another device (hard drive or CD-ROM) attached.

If the device is a USB or FireWire memory stick, skip to Step 3.

![](bbox=[0.105, 0.71, 0.2, 0.78])

+   2. **Reboot your computer and run the `dmesg` command from a GNOME Terminal window.**