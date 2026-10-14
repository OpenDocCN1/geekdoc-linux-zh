# 16 – Storage Media

In previous chapters we’ve looked at manipulating data at the file level. In this chapter, we will consider data at the device level. Linux has amazing capabilities for handling storage devices, whether physical storage, such as hard disks, or network storage, or virtual storage devices like RAID (Redundant Array of Independent Disks) and LVM (Logical Volume Manager).

However, since this is not a book about system administration, we will not try to cover this entire topic in depth. What we will try to do is introduce some of the concepts and key commands that are used to manage storage devices.

To carry out the exercises in this chapter, we will use a USB flash drive, a CD-RW disk (for systems equipped with a CD-ROM burner) and a floppy disk (again, if the system is so equipped.)

We will look at the following commands:

+   - mount – Mount a file system
+   - umount – Unmount a file system
+   - fsck – Check and repair a file system
+   - fdisk – Partition table manipulator
+   - mkfs – Create a file system
+   - fdformat – Format a floppy disk
+   - dd – Write block oriented data directly to a device
+   - genisoimage (mkisofs) – Create an ISO 9660 image file
+   - wodim (cdrecord) – Write data to optical storage media
+   - md5sum – Calculate an MD5 checksum

# Mounting And Unmounting Storage Devices

Recent advances in the Linux desktop have made storage device management extremely