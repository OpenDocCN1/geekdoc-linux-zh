# 36 · CHAPTER 3

+   * The kind of partition you are creating

+   * The drives available on your machine

Using the drop-down arrow on the Mount Point box, and select /boot to indicate that you are creating the partition for /boot. Next, enter 16 into the Size (Megs) box to indicate that it should be 16 Mb (which is the size Red Hat creates in workstation or system installations). Ensure that the “Using remaining space?” check box is unchecked, since you don't want a single partition mounted /boot! The correct type of partition is Linux native, which should already be selected. Finally, if you have only one drive, hda (or sda, a SCSI machine) will already be selected. If not, select it, and deselect any of the other drives. Double-check your work, and when you're satisfied, click OK.

The partition you just will appear in the upper right. Do not be concerned if the number under Requested headers differs from that under the Actual heading. This is caused by the geometry of your hard disk. Disk Druid will find the closest size that will allow the partition to be on a cylinder boundary.

Next, you need to create a swap partition. Interestingly, Red Hat creates a 64 Mb swap partition if you select automatic partitioning on a custom system, workstation, or laptop installation. If you select a server installation, it creates a 256 Mb swap partition. Red Hat's own Installation Guide is very helpful in answering the question of what size you should use for the swap partition because it diverges from what the program will create (“Do what I say, not what I do”).

The traditional answer is calculated by this formula: multiply the physical memory in the machine by two. Thus, a machine with 128 Mb of RAM would have a 256 Mb swap partition. Adding to the confusion, however, the latest reports say the 2.4 version of the kernel is more aggressive in its use of swap space. Recommendation is to use 256 Mb for swapping if you have a hard drive large enough to accommodate it; otherwise, use the RAM-times-two factor. In any event, don't make it larger than 512 Mb. Later, you'll be able to see the results of your selection are, and if you need, you can add additional swap space.

To create the swap partition, click Add as before, but leave the mount point blank. Insert 256 (or your chosen size) in the Size box; then using the drop-down box, select Linux Swap for your partition type, and click OK.

Now you have a big decision to make: Do incorporate everything else into the root partition, or do you separate the pieces? If you choose former, you can finish your partitioning by clicking Add. Selecting for the “Using remaining space?” option. Disk Druid will allocate the remainder of your drive to the root partition, and you can continue the installation by clicking Next.

Otherwise, create each additional partition in the same way as the /boot partition was created (changing the mount point to appropriate, of course). Click Add, select the mount point, and ensure that the partition type is Linux Native. When you've added all of the partitions that you need, continue the installation by clicking Next.

The following screen will allow you to choose the partitions to format. Since you're installing on an empty drive, you'll want to format each of the partitions. Red Hat has conveniently preselected all of the partitions you've created. An additional option, located at the bottom of the screen, is available to check for bad blocks while formatting. Modern drives have bad blocks themselves, mapping them to spare blocks kept for this purpose, so having Linux to do so is redundant. The only thing that it will cost you, should you choose to do it, though, is a little time during the format.