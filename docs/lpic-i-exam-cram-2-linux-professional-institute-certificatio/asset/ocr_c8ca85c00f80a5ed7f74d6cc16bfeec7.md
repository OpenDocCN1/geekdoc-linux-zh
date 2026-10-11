+   -s—A copy of the MBR or first sector is saved when LILo is rerun. The saved contents are put in /boot/boot.NNNN, where NNNN depends on IDE or SCSI for its naming.

+   -t—Tests the configuration only; doesn't write it to the MBR or first sector. Essentially, this is a dry run.

+   -T—This is arguably the most useful option for LILo; its keyword values can be used to bring back information about the disk and video, among others.

+   -T help—This shows help for the -T options, including

+   -T geom—Lists the drive geometry (cylinders, heads, and sectors) for all attached drives

+   -T video—Shows the graphic modes that LILo can use, which is important for laptops, specialty displays, and LCD monitors

+   -u—Followed by the device name (/dev/hda), this option copies the saved boot sector (/boot/boot.NNNN) back to the MBR or first sector. If a device name is not specified, it takes the first bootable device.

![](bbox=[0.08, 0.59, 0.2, 0.68])

> LILo is a favorite topic for the first exam, with all sorts of options being tested. Be aware of how to run a command at the next boot, how to back up the MBR, and how to restore it from a boot disk.

# LILo Error Codes

When a system boots, that occurs in two stages. The first stage loader is a single sector that is read from the BIOS or MBR. The system lets you know it's in the first stage by displaying the letter L on the screen, leading eventually to the word LILo. When the first stage is done, it prints the letter I to the screen and transfers control to the second stage loader.

The second stage loader is called from the first, and it can contain multiple sectors and more information. When the second stage loader receives control, it prints the second L in LILo to the screen, announcing that it's starting its process. When it has concluded its process, it prints the O in LILo to the screen, and then any parameters or labels desired can be entered.

If an error occurs, LILo prints a hexadecimal code for the error and attempts the process again. Some important error codes that you might see are shown here: