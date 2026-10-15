![](bbox=[0.22, 0.09, 0.78, 0.52])

Figure 6.5 Drives D and E are actually partitions on a real Windows hard drive, configured as a raw disk in VMware.

# Creating Plain Disks

Raw disks have their advantages, but their use is obviously predicated on having a spare hard drive you want to use directly inside a VMware virtual machine. If you simply want to break the 2GB virtual disk limit without employing a separate hard drive, plain disks might be the right choice.

The easiest, and arguably most useful, type of plain disk is made of files in your Linux file system. These files are, in essence, a series of large files strung together to form a single virtual disk. Although the files themselves are still subject to a 2GB limit, VMware creates as many as are necessary to accommodate the plain disk file size you request and divides the load equally between the files. (That is, if you use a 3GB plain disk, the two files will be 1.5GB in length, rather than one 2GB file and one 1GB file.)

The major disadvantage to plain disks over virtual disks is that they immediately consume the entire requested space on your Linux hard drive. Virtual disks, on the other hand, grow as necessary to your preset limit. So there is little or no advantage to using a file-based plain disk of less than 2GB.

To create a file-based plain disk, follow these steps:

+   1. Open the virtual machine configuration in the Configuration Editor.
+   2. Find a free slot in the IDE or SCSI Drives section.