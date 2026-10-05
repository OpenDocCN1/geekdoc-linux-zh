
## Chapter 3: Discovering What's in Your System

File Utilities Help

| Disk Drive Type | Free | Total Size |
| :--- | :--- | :--- |
| A: Floppy Drive, 5.25" | | 1.44 MB 8 Cylinders, 2 Heads, 512 Bytes/Sector, 16 Sectors/Track |
| : Floppy Drive, 3.5" | | 8 Cylinders, 2 Heads, 512 Bytes/Sector, 16 Sectors/Track |
| C: Fixed Disk 3.6" | | 183 Cylinders, 16 Heads, 512 Bytes/Sector, 16 Sectors/Track |
| CMOS Fixed Disk Parameters | | 0 Cylinders, 255 Heads, 4 Sectors |
| D: Hard Drive | | |

| DEVICE | Installed MESSAGE |
| :--- | :--- |
| Version 3.22 Installed | ERROR: 0 | |

Figure 3-6: The msd program tells you about the disk parameters.

Disk Drives: Displays disk drive types and sizes.

- 16. Press Enter.
- 17. Press Q (for IRQ list) and copy the information.

IRQ, which stands for interrupt request, is used by the different hardware pieces to signal the main CPU that they have some data that has to be processed.

No two devices can have the same IRQ. Copying the information in these columns for all 16 IRQs (0–15) is important for later sanity.

- 18. Press Enter to go back to the main screen, and then press F3 to end the msd program.

## Leave a Trail of Bread Crumbs

![](img/96a9ce6a13d8d15ed05f867f41574278_76_0.png)

This next step is very important: Back up your system! Follow your directions for making a backup disk that includes your master boot record, MBR.

## Chapter 4

## Making Room for SuSE Linux

### In This Chapter

- Finding out what you need to install from a CD-ROM
- Creating your boot disk
- Discovering whether you need a supplemental disk
- Squeezing SuSE Linux onto your disk

Now it's time to open your distribution — unless you're the impatient and have already ripped it from its packaging. If you are installing SuSE from the SuSE Linux For Dummies CD-ROM or from the full distribution, the installation should work exactly as described here.

## Installing from a CD-ROM

The easiest way to install Linux is on a system with a CD-ROM (especially an ATAPI/IDE or SCSI CD-ROM). Many modern motherboards are capable of booting from a CD-ROM. If you have one of these, you are lucky! Your life just got a bit easier.

If not, you must create a boot floppy and perhaps a supplemental floppy (also referred to as a modules floppy) from files on the CD. If, to install Linux, you need to use a PCMCIA card for a CD-ROM controller, you have to make the supplemental floppy as well as the boot floppy. The modules floppy contains the device drivers and other code needed for PCMCIA cards to work.

If you're not sure whether you need a modules floppy, make one anyway. If it's required, you have it. If it's not required, hey, you can always write over the floppy.

If you're not sure whether your motherboard will allow you to boot to a CD-ROM, you can always check. To set your system to boot from the CD-ROM, you need to change a setting in your BIOS (the Basic Input Output System on your motherboard). If the thought of this gives you the heebie jeebies, stop here and create yourself a boot floppy! To set the system:

- 1. Reboot your system.

The first text you see on your system screen is usually the memory check. In the upper-left corner of your screen, you will see numbers counting up and ending at none other than the total amount of memory on your system. Are you with me?

At this point, you should also see a message on the bottom of your screen that says something like Press <delete> for setup.

- 2. Press Delete to enter the system BIOS.

If you see no such messages and you lost your documentation long ago, you may be out of luck and may need to create a floppy.

- 3. After you are in the system BIOS, look for the menu option that sets the boot sequence, as it is often called; set the boot sequence so that the CD-ROM is first in the list.

- 4. Save and exit the BIOS and reboot your computer.

If this works, you do not have to make a boot disk and can boot right to the CD-ROM!

Next, we will tell you all the exciting details for creating boot and modules disks.

## Making boot and supplemental disks in MS-DOS

If you have a Windows 3.1, 95, or 98 system, you can use it to read the SuSE Linux For Dummies CD-ROM and create your boot and modules floppies. The CD includes a program called RAWWRITE.EXE, which you can use to make the floppies.

First, you need a high-density (1.44MB) 3½-inch floppy for each disk that you plan to create (boot floppy and possibly the modules floppy). Then place the SuSE Linux For Dummies CD-ROM into your CD-drive.

In these instructions, we assume that the CD-ROM is drive D and your floppy drive is A. If your drive letters are different, substitute D and A in the example with the appropriate letters.

Next, you need to...
