# Warning

Always back up information before re-partitioning and choose your tools carefully. While parted can resize a partition without destroying data, fdisk cannot.

+   2 For safety, start your machine in failsafe or single user mode.
+   3 Create a temporary mount point for the new partition. To avoid confusion, give the new partition’s mount point a name that relates to the partition that it is replacing. For example, if you are moving `/var`, call the new partition `/var_new`.
+   4 Mount the new partition.
+   5 Copy information on the old partition to the new one.
+   6 Boot from a cd or floppy.
+   7 Add the new partition to `/etc/fstab/`. Give it the mount point for the old partition.
+   8 Remove the directory for the old partition.
+   9 Reboot the computer normally. The mount point has changed.

# Creating a Swap Partition or File

Progeny Debian creates a swap partition during installation. However, you may want to add another partition or change the partition. You may also choose to create a swap file, although a swap partition is usually more stable.

+   1 Do one of the following.
+   
+   - Create the partition or file. See “Partitioning a Hard Drive,” page 361.
+   - Create a file by using by typing: `dd if=/dev/zero of=FILE bs=SIZE count=SIZE`. The size is in bytes.