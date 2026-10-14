# 7. The command rpm -q packagename does the following:

+   a. determines whether packagename is installed on the system
+   b. locates packagename on a CD-ROM
+   c. erases packagename if it is currently installed
+   d. summarizes the disk quota for users of packagename

# 8. The volume label for a file system is:

+   a. changed using fsck
+   b. viewed using mke2fs
+   c. stored in /etc/fstab
+   d. stored in the superblock

# 9. Defragmentation, the process of collecting all parts of a file into one contiguous part of a hard disk:

+   a. is performed in Linux using the fsck utility
+   b. is not needed in Linux because of the way ext2, ext3, and other Linux file systems arrange files
+   c. should be performed as part of each boot up, though it is typically done automatically by the /etc/rc.d/ startup scripts
+   d. causes data loss if performed on an ext3 file system

# 10. The Linux kernel is able to support multiple file systems types because it uses:

+   a. a virtual file system that separates standard disk operations from the drivers that perform those operations
+   b. the /etc/fstab file to list the file system type of file system to be mounted
+   c. the management and provisioning aspects of Red Hat Network
+   d. virtual memory in either a swap partition or a swap file

# 11. Which piece of information is not provided in the output when the mount command is entered with no parameters or options?

+   a. the mount point for each mounted file system
+   b. the file system type for each mounted file system
+   c. the size of each mounted file system
+   d. the options with which each mounted file system was mounted, as defined in the /etc/fstab file or in the mount command, if the file system was mounted manually (without reference to etc/fstab)