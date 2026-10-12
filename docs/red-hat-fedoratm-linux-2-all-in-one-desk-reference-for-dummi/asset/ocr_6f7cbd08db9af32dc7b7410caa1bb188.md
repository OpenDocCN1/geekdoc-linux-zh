To reduce the size of the Windows partition, follow these steps:

+   1. In the partition map in PartitionMagic's main window, right-click the partition and select Resize/Move from the menu.
+      The Resize Partition dialog box appears.

+   2. In the Resize Partition dialog box, click and drag the right edge of the partition to a smaller size.
+      For a large hard disk (anything over 10GB), reduce the Windows partition to 5GB and leave the rest for Fedora Core.

+   3. Click OK and then Apply to apply the changes. After PartitionMagic has made the changes, click OK.

+   4. Reboot the PC.

+   5. Choose Start-⁸Programs-⁸Accessories-⁸System Tools-⁸ScanDisk to run ScanDisk.

You don’t have to do anything with the disk space left over after shrinking the partition that used to be the C drive. During installation, the Fedora Core installer uses that free space to install Fedora Core.

# Repartitioning with FIPS

The DVD-ROM includes a utility program called FIPS (First Nondestructive Interactive Partition Splitting Program) that can split an existing disk partition into two partitions. FIPS cordons off the unused part of a hard disk and makes a new partition out of that unused part without destroying any existing data. FIPS cannot split partitions with the NTFS file system that’s often used in Windows NT/2000/XP systems.

Some words of caution before you proceed to repartition your hard disk with FIPS. In the words of FIPS author Arno Schaefer, “FIPS is still somewhat experimental, although it has been used by many people successfully and without serious problems.” That tells you in a nutshell that you’re on your own when it comes to using FIPS. Neither the publisher nor I can accept responsibility or liability for damages resulting from the use or misuse of FIPS. There is a chance that FIPS could damage your hard disk, making it unusable. Try FIPS only after making sure that you backed up everything on the hard drive and that your backup is usable. Also, before you use FIPS, check your hard disk to make sure it’s ready:

+   - Your hard drive has only a FAT or FAT32 partition to start with.
+   - The drive has enough free space available for a useful Fedora Core installation — and that means 3 to 4 gigabytes (3–4GB) of free space.