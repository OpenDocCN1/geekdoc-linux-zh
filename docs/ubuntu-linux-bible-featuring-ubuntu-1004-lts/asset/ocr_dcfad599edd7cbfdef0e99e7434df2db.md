# Chapter 2: Installing Ubuntu

# # Reformatting a USB Flash Drive.

The Ubuntu "Create a USB startup disk" application will try to reuse any existing FAT32 (VFAT) partition on your USB stick. If you've reformated the USB stick to contain multiple partitions, changed the filesystem type of any of your partitions, or already have multiple partitions on the stick but don't need to use them, this sidebar explains how to reformat your flash drive so that it contains a single FAT32 partition that the "Create a USB startup disk" option can make the most of. As you might expect, this will delete any information that is currently present on the USB stick, so make sure you've copied anything you ever want to see elsewhere following the instructions in this sidebar.

To reformat a USB stick, do the following:

+   1. Select the Applications <-- Terminal command to start a GNOME terminal.
2. Enter the `sudo` command and your password to become the root user.
3. Use the `df` command to see the mounted partitions on your system. If any of partitions from your USB stick are mounted, unmount each of them using the `umount` command.
4. Execute the `fdisk` command with the device corresponding to your USB stick as an argument. You must specify the name of the device, not a partition on that device. For example, if your USB stick was `/dev/sdb`, you would execute the command `fdisk /dev/sdb`.
5. Press `p` and Enter/Return to see a list of all the partitions on the USB stick. Use the `d` command to delete each of them, where `number` is the number of the partition in device names in the first column of the output displayed by `p`. When you're done, press `p` to list the partition table—you should not see any partitions listed.
6. Use the `n` command to begin creating a new partition on the flash drive. Enter `p` to create this as a primary partition, and enter `1` as the partition number. Press Return when prompted for the starting block of the new partition to accept the default value of 1. When prompted for end of the partition, press Enter/Return again to use the entire disk.
7. Type 7 and press Enter/Return to begin changing the type of the first partition on the drive. Enter 1 to identify the partition you want to change, and enter `c` (Windows 95 FAT32 LBA) as the type of the partition.
8. Type `a` and press Enter/Return to set your new partition as active (i.e., bootable). When prompted for the partition number, enter 1 and press Enter/Return.
9. Type `w` to write your updated partition table to the USB stick. Type `q` to exit the `fdisk` application.

After re-partitioning your USB stick, you must remove and reattach it to your system to read the new partition table. After re-attaching the drive, use the `dmesg` command to display the few kernel messages, one of which identify the device name and available partitions on the USB stick that you just reattached. You can use the `fdisk /dev/DEVICE` command to list the partitions on the device named `DEVICE` to verify that you know the device name of the re-attached drive—it is

continued