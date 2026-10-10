When invoked, `fdisk` will show a greeting, then a warning and it will wait for your commands.

```
# fdisk /dev/sda
Welcome to fdisk (util-linux 2.33.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help):
```

The warning is important. You can create, edit or delete partitions at will, but *nothing* will be written to disk unless you use the write (w) command. So you can "practice" without risk of losing data, as long as you stay clear of the w key. To exit `fdisk` without saving changes, use the q command.

> **NOTE**  That being said, you should never practice on an important disk, as there are always risks. Use a spare external disk, or a USB flash drive instead.

# Printing the Current Partition Table

The command `p` is used to print the current partition table. The output is something like this:

```
Command (m for help): p
Disk /dev/sda: 111.8 GiB, 120034123776 bytes, 234441648 sectors
Disk model: CT120BX500SSD1
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x97f8fef5

Device Boot Start End Sectors Size Id Type
/dev/sda1 4096 226048942 226048847 107.8G 83 Linux
/dev/sda2 226048944 234437550 8388607 4G 82 Linux swap / Solaris
```

Here is the meaning of each column:

# Device

The device assigned to the partition.

# Boot

Shows whether the partition is “bootable” or not.