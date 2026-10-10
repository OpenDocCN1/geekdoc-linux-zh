# Booting from Floppy Causes System to Hang or Reboot

A few things can cause a system to hang or reboot when booting from a floppy, but a bad floppy is the most likely cause. Remember that the boot image is written to the floppy without checking the format and that the entire floppy is used. Even a single bad block on the floppy can cause problems. Try writing the boot disk to a new floppy and see if it fixes the problem.

If using a new floppy does not fix the problem, make sure you used binary mode and not ASCII mode to transfer the floppy in your FTP client.

Virus protection on the motherboard is another possible cause of this problem. You can disable this protection in the system's BIOS setup utility. Please refer to your system documentation for information on how to disable the virus protection on your motherboard.

Finally, make sure you created the floppy from DOS mode, not from a DOS prompt in Windows. The latter has been known to cause boot problems on occasion.

# Boot Floppy Hangs at “Probing Devices”

The boot floppy sometimes gets confused by IDE Zip and Jazz drives. If you have one of these drives, try removing it and see if the system will boot. If it does, you can install FreeBSD and then reconnect the drive after the installation is complete.

# System Boots from CD, but Installer Shows That CD-ROM Was Not Found

This problem is probably caused by an improperly configured CD-ROM drive. Some systems ship with the CD-ROM drive as a slave drive on the secondary controller and have no master drive on the secondary controller. To fix this, you will need to change your CD-ROM drive to the master if it is on the secondary controller. This can usually be done via a jumper on the back of the CD-ROM drive (you will need to go inside your case). When your system first starts up, it may display a list of disks it found, including CD-ROM drives, as well as information about whether they are configured as master or slave disks.

# Hard Disk Geometry Is Not Detected Properly

If FreeBSD cannot detect your hard disk geometry correctly, there are two ways this can usually be fixed:

+   * You first might create a small DOS partition at the beginning of the disk. This partitioning will usually cause FreeBSD to see the right geometry.
+   * The second way is to use the *fdisk* program included on the CD-ROM (located in the *tools* directory). *fdisk* runs under DOS and will usually detect the proper geometry of the hard disk; you then can give the FreeBSD partition the proper geometry manually.