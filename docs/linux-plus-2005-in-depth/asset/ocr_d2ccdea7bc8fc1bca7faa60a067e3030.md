and continue the boot process. The mkbootdisk command can be used to create a boot disk after installation; to create a boot disk with the 2.6.5-1.358 kernel on it, you can use the command mkbootdisk 2.6.5-1.358 at the command prompt and insert a blank floppy disk when prompted. This boot disk can then be used to boot into a system such that the boot loader can be repaired.

Because the operating system transfers data to and from the hard disk frequently, the file-system can become corrupted over time; a corrupted filesystem can be identified by very slow write requests, errors printed to the console, or failure to mount. If the filesystem on a partition mounted to a noncritical directory, such as /home or /var, becomes corrupted, you should perform the following troubleshooting steps:

+   1.  Unmount the filesystem if mounted.
+   2.  Run the fsck command with the -f (full) option on the filesystem device.
+   3.  If the fsck command cannot repair the filesystem, use the mkfs command to re-create the filesystem.
+   4.  Restore the original data for the filesystem using a back-up utility.

![](bbox=[0.16, 0.44, 0.22, 0.5])

> > **NOTE**
> >
> > Do not restore data onto a damaged filesystem; ensure that the filesystem has been re-created first.

If the / filesystem becomes corrupted, the system is unstable and must be turned off. Following this, you can use a copy of Linux on the installation media to remedy the problem using the following troubleshooting steps:

+   1.  Place the first Red Hat Fedora installation CD-ROM in the CD-ROM drive and turn on the computer.
+   2.  At the welcome screen shown in Figure 13-5, type linux rescue and press Enter. When prompted for language and keyboard layout, choose English and US (us), respectively. When prompted to start the network, choose No.
+   3.  At the screen depicted in Figure 13-6, choose Skip to enter a shell for the Linux system on the CD-ROM, as shown in Figure 13-7. This system contains utilities in the /usr/bin and /usr/sbin directories that can restore the filesystem on the hard disk.
+   4.  Use the mkfs command on the CD-ROM Linux system to create a new / filesystem on the appropriate partition on the hard disk.
+   5.  Use a back-up utility on the CD-ROM Linux system (tar, dump, or cpio) to restore the original data to the re-created / filesystem.
+   6.  Type exit at the shell prompt to reboot the system.