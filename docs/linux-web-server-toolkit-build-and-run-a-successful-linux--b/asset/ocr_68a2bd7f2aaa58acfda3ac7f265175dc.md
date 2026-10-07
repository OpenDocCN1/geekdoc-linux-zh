# Linux Web Server Toolkit

3. If you have more than one hard disk on your system, choose which one you want to use FIPS on. You need only press the number; you don't need to press Enter afterwards:

Which Drive (1=0x80/2=0x81)? 1

4. A partition table for that hard disk is shown. Enter the partition you want to split off as free space for Linux. Choose your DOS/Windows partition. If the hard disk has several partitions, you can identify the correct partition from either the size (the far right column) or the System (filesystem type), which will be O6 for DOS systems:

Which Partition do you want to split (1/2)? 1

5. A screen of statistics is displayed as FIPS checks the status of the partition you selected. Press y to make a backup copy of your root and boot sectors before continuing:

Do you want to make a backup copy of your root and boot sector before proceeding? (y/n)? y

6. Insert a bootable floppy (you can make one with the SYS command in DOS) in the first floppy drive and press y:

Do you have a bootable floppy disk in drive A: as described in the documentation (y/n)? y

7. The partition size information is shown in megabytes, with the cylinder boundary for where the split will occur between the existing partition and the new (free space) area:

| Old partition | Cylinder | New Partition |
| 1297.3 MB | 751 | 2.0 MB |

8. Use the arrow keys to make the New Partition size equal to the amount of free space you want for Linux system (the swap and main Linux partitions). Press Enter when it's adjusted the way you want.

9. The new partition table is displayed with your edits in place (you're making two partitions out of one).

10. Press c to continue or r if you want to try changing the sizes of the partitions again:

Do you want to continue or reedit the partition table (c/r)? c

11. Another screen of statistics is shown. If you're ready to alter the hard disk partition table, press y. If you're not sure about it as you want, press n:

Ready to write new partition scheme to disk
Do you want to proceed (y/n)? y