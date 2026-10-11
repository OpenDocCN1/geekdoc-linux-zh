4. After making the changes, click the Next button in the Disk Druid screen to proceed to the next installation step. As shown in figure 9.

![](bbox=[0.31, 0.19, 0.79, 0.47])

# Configuring Linux Installation

After you prepare the disk partitions with Disk Druid and specify which partitions to format, perform the following steps to configure Linux installation:

+   - Install Boot Loader GRUB
+   - Configure the network
+   - Firewall configuration
+   - Set the time zone
+   - Set the root password and add user accounts
+   - Configure password authentication

The following sections guide you through each of these configuration steps.

# Installing the Boot Loader (GRUB)

The next part of the Boot Loader Configuration screen as shown in figure 10 gives you the option of installing the boot loader in one of the two locations, which are as follows:

+   - Master Boot Record (MBR), which is located in the first sector of your PC's hard disk.
+   - First sector of the partition where you loaded Linux.