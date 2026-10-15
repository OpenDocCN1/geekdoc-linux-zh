11. The wizard summarizes the virtual machine it will create, and should look similar to Figure 6.4, although the values might be different depending on your choices. If everything looks appropriate, click Done.

![](bbox=[0.24, 0.22, 0.54, 0.55])

# Adjustments with the Configuration Editor

The wizard is reliable, but not thorough. You should make a quick stop in the Configuration Editor to make a few minor adjustments before you launch the virtual machine and start the Windows installation:

+   1. Open the Configuration Editor in the Settings menu.
+   2. Verify that the wizard created a primary master (P-M) IDE virtual disk in the Win 98 configuration directory of the size you created (it might appear to be one megabyte less than you specified) and a secondary master (S-M) CD-ROM, most likely pointing to /dev/cdrom.

> You might want to come back later and reassign /dev/cdrom to be a virtual SCSI CD-ROM drive, but because VMware does not support booting from a virtual SCSI CD-ROM and the Windows 98 boot floppy does not support the VMware SCSI controller, you need the CD-ROM in virtual IDE mode to install Windows 98.

+   3. If you want the virtual machine to have direct access to your serial or parallel ports, configure them now as described in Chapter 5, "Running VMware for the First Time." Remember that serial ports start at /dev/ttyS0 and parallel ports start at /dev/lp0 on most Linux machines.