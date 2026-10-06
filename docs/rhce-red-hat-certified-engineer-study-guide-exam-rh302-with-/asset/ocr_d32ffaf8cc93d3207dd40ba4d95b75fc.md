+   * /usr
* /usr/local
* /var

To apply your understanding of partitions to a practical problem, complete Exercise 6.1.

# EXERCISE 6.1

# Designing a Partition Structure

Design a partition structure for a system having two disk drives, each with a 5GB capacity. Provide at least 1GB of space for users' home directories and 2GB of space for commercial applications installed under the /opt directory.

# Using fips

Often, a target system has insufficient free disk space for installing Linux. If an MS-DOS (FAT or FAT32) partition contains unused space, you can use fips to split the partition, creating an empty partition into which you can install Linux.
To fips, follow these steps:

+   1. Use scandisk to check the partition for errors.
2. Use defrag to move the files to the low end of the partition.
3. Disable virtual memory by using the System Control Panel.
4. Create an MS-DOS boot floppy using the Add/Remove Programs Control Panel.
5. Copy the following files from the installation CD-ROM to the floppy disk:
* \dosutils\fips20\restorb.exe
* \dosutils\fips20\fips.exe
* \dosutils\fips20\errors.txt