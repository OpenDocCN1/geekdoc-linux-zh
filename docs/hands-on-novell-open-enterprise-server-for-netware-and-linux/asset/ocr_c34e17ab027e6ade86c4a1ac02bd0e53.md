The Resize dialog box shown in Figure 13-22 contains fields for setting new starting and ending cylinder numbers. In the following activity, you learn how to use the Expert Partitioner utility to create a new partition and then change its size.

![](bbox=[0.11, 0.12, 0.59, 0.34])

Figure 13-22 Resizing a partition

# Activity 13-6: Creating and Editing Linux Partitions

**Time Required:** 10 minutes

**Objective:** Use the YaST utility to create and work with Linux partitions.

**Requirements:** Free or unpartitioned space on your disk drive

![](bbox=[0.11, 0.505, 0.15, 0.545])

If you're using VMware, you might want to add another drive to your Linux system, as described in Appendix C.

**Description:** After installing the Linux server, often you need to create and work with partitions to set up the network file system. For example, Eric wants you to create another traditional partition to be used for storing Engineering Department CAD files. In this activity, you use the Expert Partitioner utility to create a new partition and then resize it.

+   1. If necessary, log in to your SUSE Linux server with your user name and password.
+   2. Start the YaST utility and enter your root password.
+   3. Click the **System** icon in the left pane, and then click the **Partitioner** option in the right pane. When you see the message asking whether you want to continue, click **Yes** to display the Expert Partitioner window.
+   4. Click the **Create** button. (If you're using VMware and have a second disk drive, you're asked which drive to use. Select the second drive and click **OK** to continue.)
+   5. Click the **Primary partition** option button, and then click **OK** to display the Create a primary partition dialog box.
+   6. Verify that the Reiser file system is selected in the Format section.
+   7. Enter a partition size of at least 50 cylinders, and record the mount point:
+   8. Click **OK** to create the partition.
+   9. Click **Apply** to write your changes and return to the YaST main menu, click **Apply** again if asked for confirmation, and leave YaST open for the next activity.