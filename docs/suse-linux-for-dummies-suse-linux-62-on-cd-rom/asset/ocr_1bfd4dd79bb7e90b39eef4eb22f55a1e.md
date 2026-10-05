# Chapter 3: Discovering What's in Your System

File Utilities Help
Disk Drive Type Free Total Size
A: Floppy Drive, 5.25" 1.44
8 Cylinders, 2 Heads
512 Bytes/Sector, 16 Sectors/Track
: Floppy Drive, 3.5"
8 Cylinders, 2 Heads
512 Bytes/Sector, 16 Sectors/Track
C: Fixed Disk 3.6"
183 Cylinders, 16 Heads
512 Bytes/Sector, 16 Sectors/Track
CMOS Fixed Disk Parameters
0 Cylinders, 255 Heads
4 Sectors
D: Hard Drive
DEVICE Installed
MESSAGE Version 3.22 Installed
ERROR: 0

Figure 3-6: The msd program tells you about the disk parameters.

Disk Drives: Displays disk drive types and sizes.

+   16. Press Enter.

+   17. Press Q (for IRQ list) and copy the information.

IRQ, which stands for interrupt request, is used by the different hardware pieces to signal the main CPU that they have some data that has to be processed.

No two devices can have the same IRQ. Copying the information in these columns for all 16 IRQs (0–15) is important for later sanity.

+   18. Press Enter to go back to the main screen, and then press F3 to end the msd program.

# Leave a Trail of Bread Crumbs

![](bbox=[0.065, 0.665, 0.155, 0.735])

This next step is very important: Back up your system! Follow your directions for making a backup disk that includes your master boot record, MBR.