# Chapter 3 ✦ Partitions, Filesystems, and Files 85

Units = cylinders of 1008 * 512 = 516096 bytes

| Device | Start | End | Blocks | Id | System |
| /dev/hda | | 1041 | 524632+ | 82 | Linux swap |
| /dev/hda2 | | 1042 | 7283 | 315968 | 83 | Linux |
| /dev/hda3 | | 7284 | 11445 | 209768 | 83 | Linux |
| /dev/hda4 | | 11446 | 15321 | 195354 | 5 | Extended |
| /dev/hda5 | | 11446 | 11834 | 196024+ | 83 | Linux |

Command (m for help):

Enter n to create a partition. Because you have used all the primary partitions you can create on the disk and now have one extended partition, fdisk is clever enough to realize that you cannot create a primary partition and therefore determines that you can create only a logical partition within the empty extended partition. Although you have the ability to create many more partitions, this example creates a small logical partition of 200MB for a test filesystem.

Printing the partition table shows you five partitions. The extended partition cannot store data or be accessed by Linux as anything but a container for logical partitions.

# Updating a Disk’s Partition Table

After you have created a partition, you need to save the updated partition table for your disk. As mentioned before, do not do this on a live system unless you are allocating previously unused space. If the disk you are working on is currently in use (as may well be the case on a small home machine), the partition table will be saved but cannot be reloaded by Linux. To solve this problem, you need to reboot your machine. If you were partitioning a disk that was not in use (no filesystems mounted), then saving and reading the partition table will work without a problem. Listing 3-5 shows the q (quit) command in fdisk, followed by messages from fdisk indicating that the system must be forced to update its idea of the disk’s partition table.

# Listing 3-5: Saving the Partition Configuration

Command (m for help) : Q
The partition table has been altered!

Calling ioctl1() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: Device or busy.
The kernel still uses the old table.
The new table will be used at the next reboot.
Syncing disks.
bible:~ #