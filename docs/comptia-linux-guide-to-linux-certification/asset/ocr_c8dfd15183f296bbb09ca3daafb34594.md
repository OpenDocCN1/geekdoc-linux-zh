**vgdisplay command** A command used to view LVM VG.

**vgextend command** A command used to add additional physical volumes to an LVM VG.

**vgscan command** A command used to view LVM VGs.

**Volume Group (VG)** A group of PVs that are used by the LVM.

# # Review Questions

+   1. Which of the following commands can be used to create partitions on either a MBR or GPT hard disk?  
+   a. `gdisk`  
+   b. `cfdisk`  
+   c. `fdisk`  
+   d. `parted`

+   2. After a partition on a hard disk drive is formatted with a filesystem, all partitions on that hard disk drive must use the same filesystem. True or False?

+   3. You want to see the file systems that are presently in use on the system. What command could you use?  
+   a. `cat /etc/fstab`  
+   b. `ls -1 /etc/fstab`  
+   c. `cat /etc/mtab`  
+   d. `ls -1 /etc/fstab`

+   4. Jim has just purchased two new SCSI hard disk drives and a controller card for them. He properly installs the hardware in his machine. Before he can use them for data storage and retrieval, what must he do? (Choose all that apply.)  
+   a. Mount the two hard drives so they are accessible by the operating system.  
+   b. Mount a filesystem to each of the hard disk drives.  
+   c. Create one or more partitions on each of the hard disk drives.  
+   d. Use the vi editor to edit `/etc/mtab` and create an entry for the controller card and the hard disk drives.  
+   e. Mount any partitions created on the two hard drives such that they are accessible by the operating system.  
+   f. Format any partitions created with a valid filesystem recognized by Linux.