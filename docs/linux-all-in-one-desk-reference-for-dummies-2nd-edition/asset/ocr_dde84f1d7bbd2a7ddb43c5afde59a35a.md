3. Click **Ok** and then click **Apply** to apply the changes. After **PartitionMagic** has made the changes, click **Ok**.

4. Reboot the PC.

You don’t have to do anything with the hard drive space left over after shrinking the partition that used to be the C: drive. During installation, the Linux installer uses that free space to install Linux.

# Resizing a partition with QTParted in Knoppix

After Knoppix boots and the GUI desktop appears, follow these steps to reduce the size of the Windows partition:

+   1.  Choose **Main Menu>System>QTParted** from the Knoppix desktop.
+   
+       The QTParted window appears, and the tool displays the drives it finds on your PC. The first hard drive appears with a device name `/dev/hda`, second one as `/dev/hdb`, and so on.
+   2.  Click the hard drive from the list of devices on the upper left side of the QTParted window.
+   
+       QTParted displays the drive’s information in the lower left side and the partition information in the right side of the window, as shown in Figure 2-1.

![](bbox=[0.25, 0.56, 0.6, 0.84])

3.  From the list of partitions on the right, click the partition you want to **resize**.