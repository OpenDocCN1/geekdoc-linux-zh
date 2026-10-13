chapter on using SCSI devices for Windows, Linux, and NetWare later on in this book.

+   8. Next, you will have to select the type of disk that you will be using. You can choose to create a new virtual disk (which is what I suggest you do to get started), use an existing disk if you already have one, or use a physical disk. This last option is not recommended for most common installations.
+   
+   9. In the next window, you have to select the Virtual Disk Type: IDE or SCSI. If you are not sure if SCSI is correctly supported by your operating system, then set it to IDE because that is supported by any known operating system.
+   
+   10. If you have chosen to use a virtual disk in step 8, you must now select the size of the disk. Also, select if you want the disk to grow dynamically to that size, or if the disk space should be allocated when creating the virtual disk.

![](bbox=[0.12, 0.38, 0.88, 0.78])

Figure 2.9: Specify the disk size and other features for your virtual disk.

The minimum size of a disk is 100 MB and the maximum is 950 GB for both IDE and SCSI.

If you have a file system that only supports files to a maximum of 2 GB (such as FAT), you will have to split the disk files onto separate 2 GB files. However, they will, form a set of files that have the same name prefix and are