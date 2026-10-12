disk partition into two partitions. FIPS cordons off the unused part of a hard disk and makes a new partition out of that unused part without destroying any existing data. FIPS cannot split partitions with the NTFS file system that’s often used in Windows NT/2000/XP systems.

![](bbox=[0.12, 0.2, 0.25, 0.29])

Some words of caution before you proceed to repartition your hard disk with FIPS. In the words of the FIPS author Arno Schaaf, “FIPS is still somewhat experimental, although it has been used by many people successfully and without serious problems.” That tells you in a nutshell that you’re on your own when it comes to using FIPS. Neither the publisher nor I can accept responsibility or liability for damages resulting from the use or misuse of FIPS. There is a chance that FIPS could damage your hard disk, making it unusable. You should try FIPS only after making sure that you’ve backed up everything on the hard drive and that your backup is usable. Also, before you use FIPS, check your hard disk to make sure it’s ready:

+   - Your hard drive should have only a FAT or FAT32 partition to start with.
+   - The drive should have enough free space available for a useful Red Hat Linux installation — and that means 3 to 4 gigabytes (3–4GB) of free space.
+   - The drive must be defragmented before you can use FIPS.
+   - The drive must not be in use. You can’t partition the hard drive while you’re using it, which means (among other things) that you can’t run FIPS from inside Windows. You have to shut down Windows, boot from a startup disk, and run FIPS by itself.

When you’re ready to use FIPS, follow these steps (use FIPS only if you are running Windows 95/98/Me):

+   1. Open the Control Panel by choosing Start→Settings→Control Panel.
+   2. Double-click the Add/Remove Programs icon in the Control Panel window.
+   3. Click the Startup Disk tab, click the Create Disk button, and follow the instructions.
+   4. Insert this book’s DVD-ROM in the DVD-ROM drive.
+   5. Use Explorer to view the contents of the DOSUTILS folder. Then copy FIPS.EXE and RESTORRB.EXE to the startup disk in the A drive. FIPS.EXE is the program that splits partitions. RESTORRB.EXE is a program that can restore parts of your hard drive from a backup of the areas created by FIPS (you use RESTORRB if something goes wrong).
+   6. Go to the FIPSDOCS folder that’s inside the DOSUTILS folder on the DVD. Copy the ERRORS.TXT file to the startup disk.