# How to Create Partitions

# Procedure Reference: Create a Primary Partition

To create a primary partition:

+   1. Log in as root.
2. Enter fdisk /dev/(device name) to partition the disk.
3. Enter n to create a partition.
4. Create a primary partition.
 a. Enter p to create a primary partition.
 b. To accept the default starting point of the partition, press Enter.
 c. Specify the partition size.
 - To accept the default partition size, press Enter.
 - To specify a custom partition size.
 - Enter +[Required size] to specify the partition size in blocks.
 - Enter +[Required size]K to specify the partition size in kilobytes (KB).
 - Enter +[Required size]M to specify the partition size in megabytes (MB).
5. Enter w to write the partition table on the disk.
6. Enter partprobe or reboot the system to update the partition table.
7. Enter sfdisk -l /dev/(device name) to list the partition table.

# Procedure Reference: Create an Extended Partition

To create an extended partition:

+   1. Log in as root.
2. Enter fdisk /dev/(device name) to begin disk partitioning.
3. Enter n to create a partition.
4. Create an extended partition.
 a. Enter e to create an extended partition.
 b. To accept the default starting point of the partition, press Enter.
 c. To accept the default partition size, press Enter.
 d. Enter n to create a logical partition within the extended partition.
 e. To accept the default starting point of the partition, press Enter.
 f. Specify the partition size.
 - To accept the default partition size, press Enter.
 - To specify a custom partition size.
 - Enter +[Required size] to specify the partition size in blocks.
 - Enter +[Required size]K to specify the partition size in kilobytes (KB).
 - Enter +[Required size]M to specify the partition size in megabytes (MB).
5. Enter w to write the partition table on the disk.
6. Enter partprobe or reboot the system to update the partition table.
7. Enter sfdisk -l /dev/(device name) to list the partition table.