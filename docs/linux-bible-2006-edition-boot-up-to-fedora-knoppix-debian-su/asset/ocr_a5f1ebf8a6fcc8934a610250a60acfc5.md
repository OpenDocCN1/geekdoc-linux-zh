# Chapter 7 ✦ Installing Linux 257

4. Type the number of megabytes to be used for the partition (in the Size field). If you want this partition to grow to fill the rest of the hard disk, you can put any number in this field (1 will do fine).

5. If you have more than one hard disk, select the disk on which you want to put the partition from the Allowable Drives box.

6. Type the size of the partition (in megabytes) into the Size (MB) box.

7. Select one of the following Additional Size Options:

+   **Fixed size** — Click here to use only the number of megabytes entered into the Size box when you create the partition.

+   **Fill all space up to (MB)** — If you want to use all remaining space up to a certain number of megabytes, click here and fill in the number (You may want to do this if you are creating a VFAT partition up to the 2048MB limit that Disk Druid can create.)

+   **Fill to maximum allowable size** — If you want this partition to grow to fill the rest of the disk, click here.

8. Optionally select Force to Be a Primary Partition if you want to boot the partition or Check for Bad Blocks if you want to have the partition checked for errors.

9. Select OK if everything is correct. (The changes don't take effect until several steps later when you are asked to begin installing the packages.)

To edit a partition in Disk Druid from the main Disk Druid window, follow these steps:

+   1. Click the partition you want to edit.

+   2. Click the Edit button. A window appears, ready to let you edit the partition definition.

+   3. Change any of the attributes (as described in the add partition procedure). For a new install, you may need to add the mount point (/) for your primary Linux partition.

+   4. Select OK. (The changes don't take effect until several steps later, when you are asked to begin installing the packages.)

**Partitioning with fdisk**
The fdisk utility is available with every Linux system for creating and working with disk partitions in Linux. It does the same job as graphical partitioning tools such as Disk Druid, although it's no longer offered as an option for Fedora installation. However, during Fedora installation, and other Linux installations that have virtual terminals running, you can switch to a shell (press Ctrl+Alt+F2) and use fdisk manually to partition your hard disk.