storage device — now let's actually make it do work. The following example creates two partitions on the disk /dev/sdb.

To partition a disk using fdisk, do the following:

+   1. Use the sudo command to start the fdisk command, supplying the name of the disk that you want to partition as an argument, as in the following example:

```
sudo fdisk /dev/sdb
```nThe number of cylinders for this disk is set to 14593. There is nothing wrong with that, but this is larger than 1024, and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs (e.g., DOS FDISK, OS/2 FDISK)
Command (m for help):

The last line of the sample output is fdisk's command prompt, which shows that it is waiting for a command.

+   2. Use the p (print) command to display a list of any existing partitions that may already be on the disk. After all, you don't want to accidentally create partitions on the wrong disk or destroy any existing data. This command and its output look like the following:

```
Command (m for help): p
Disk /dev/sda: 120.0 GB, 12034123776 bytes
255 heads, 63 sectors/track, 14593 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot Start End Blocks Id System
Command (m for help):\```

Good. As the total lack of partitions shows, this disk does not currently contain any partitions.

+   3. Use the n (new) command to define a new partition:

```
```
Command (m for help): n
Command action
e extended
p primary partition (1-4)
```
```

+   4. Entering this command prompts you for the type of partition that you want to create, either e (extended) or p (physical). The p command to create a physical partition:

```
```
p
Partition number (1-4):
```
```