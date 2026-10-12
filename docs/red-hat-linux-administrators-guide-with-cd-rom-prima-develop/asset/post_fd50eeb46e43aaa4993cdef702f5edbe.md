
when determining how much disk drive space to be set aside for swap is to partition one and a half to two times your physical RAM.

## NOTE

If you currently have 64 megabytes of RAM on your system, 96 megabytes of swap would be a reasonable amount to devote to swap space. One thing to remember is that swap space and RAM operate together. That means that the 64 megabytes of RAM and the 96 megabytes of swap add up to 160 megabytes of memory. The minimum amount of space that should be set aside for swap space is 16 megabytes. Lastly, under some of the older Red Hat Linux releases, the most space that could be set aside for swap was 128 megabytes of RAM. That limit has since been surpassed in the latest Red Hat Linux releases.

Use discretion when setting up the swap space. Don't set so much aside to the detriment of your other partitions. Failure to set up, initialize, or configure swap space correctly can result in poor performance. Red Hat will remind you to set swap space during the installation and will not proceed if you do not set at least a minimum amount of drive space for memory size. Because of how Linux manages its swap space and places working programs on the drive for later reference, there can be too much of a good thing. If swap space is consumed quickly by system programs or doesn't start up correctly, access rates and performance suffer. Swap space greater than three times the size of RAM is probably useless.

The command used to enable swap space is `swapon -a`. This command is executed from the `/etc/rc.d` files. As the machine boots up, it reads through the rc or run command files. These are those files that the operating system reads in order to initialize the system and start various daemons. When the OS finds the `swapon` command, it activates the swap partitions.

The information about your swap partition is kept in the `/etc/fstab` file. Here your computer looks for information about the parameters you determined during setup; then, upon bootup, the computer executes these definitions. The swap partitions defined in `/etc/fstab` have a mount value of `none` and their type is set to `swap`. This informs the operating system how to treat each particular partition when the `swapon` command is issued during the boot up phase or when each partition is mounted.

A similar process is executed when the computer shuts down. As will be mentioned later, powering down a Linux machine is not as simple as turning off the power. If the system is shut down improperly or all power is cut before certain processes can be cleanly halted, file systems and data become corrupted. During the shutdown process, the system executes the `swapoff` command in order to unmount the swap partitions. If you install Linux properly, you will probably not ever need to use the `swapon` or `swapoff` command. You can manually invoke the command, however, when setting aside an additional swap partition or when cleaning up after a system failure. For more information about starting and stopping the computer, see Chapter 2, "Starting Up and Shutting Down."

### Exploring Minimal Layout Schemes

If you are using Linux for more mundane purposes, such as desktop use, or if space is limited, setting up the partitions can be even easier. In such cases, you can place all the directories on one partition. Rather than creating separate partitions, one large standard partition or `/` is set aside, into which all directories and sub-directories are then placed. Swap will still need its own partition. Table 1.2 shows a sample layout for a single 2.1 gigabyte hard drive.

**Table 1.2 A Sample Layout for a Computer with Limited Hard Drive Space**

| Partition Name | File System | Size (MB) | Description |
| :--- | :--- | :--- | :--- |
| / | /dev/hda1 | 2,000 | Root directory |
| swap | /dev/hda7 | 100 | Swap space |

Such a layout is feasible, but not recommended. If one of the directories were to fail or if a reinstall were necessary later, all the files and their contents could become corrupted or would be overwritten. Distributing both system and personal information over several different partitions is a much wiser decision.

### Setting Up Multiple Drives and Partitions

A system with several physical hard drives is even easier to set up. Here it is necessary to place a directory or partition on an actual physical drive. Whether the drives are IDE or SCSI, Linux has the resources to determine the types of drives installed and to assist in their partitioning. Table 1.3 shows a sample configuration for a system similar to that of one of my many machines. I have a 200 MHz Pentium with 64 megabytes of RAM and three actual drives, the first two of which are IDE and the last being SCSI. The table shows how I partitioned the file systems across the three physical drives.

**Table 1.3 A Sample Partitioning Scheme across Three Hard Drives**

| Partition Name | File System | Size (MB) | Description |
| :--- | :--- | :--- | :--- |
| `/` | /dev/hda1 | 400 | Root directory |
| swap | /dev/hda2 | 100 | Swap space |
| /home | /dev/hdb1 | 500 | Home directory |
| /usr | /dev/hdb2 | 500 | Binaries |
| /usr/local | /dev/sda1 | 300 | My own programs |
| /var | /dev/sda2 | 200 | Log messages |

As you can see, the first IDE drive, hda, has only 500 megabytes of space, while the second is about 1,000 megabytes. The third drive, identified by the device label sda (for SCSI drive), is also about 500 megabytes.

> **CAUTION**
> Once you have saved the new partitions and written them to disk, all information formerly found on that drive is lost. Be sure you are absolutely sure that this is what you want before deleting and creating new partitions.

The partitioning format here is much like that of the schemes used earlier in this chapter. You are free to place additional directories in other partitions. However, I have found it useful to keep the partitions to a minimum in case I need to add more drives later. That way a unique directory not allocated to a partition can be dedicated entirely to the new hard drive. This requires adding the new drive device to the `/etc/fstab` file and then mounting the partition.

The latest Red Hat Linux makes this task simpler with the kudzu utility. Much as Windows can find and determine the type of new hardware placed in the machine, Linux accomplishes the same task and can update the drivers and devices without requiring the installation CD or boot disk. You should run kudzu after installing, replacing, or exchanging hardware. You can usually start kudzu by executing the full command `/usr/sbin/kudzu` as root or superuser.

## GETTING STARTED

### Restoring Lost Partitions

If the unthinkable does happen and the system does crash, making certain partitions unreadable, or if you simply want to reinstall, having taken the time to spread the separate directories across multiple partitions can prove to be advantageous. You will first want to try to access the corrupted file system and correct any errors that might be on the disk. Usually Linux will do this for you with the `fsck` tool (pronounced by some as efes check). You may need to run `fsck` manually to clean up the system, in which case knowing the layout of your system will again prove beneficial.

You should reinstall only in worst-case scenarios. However, if you feel that reinstallation is your only option, Red Hat allows you to redefine which partitions to reformat and which to leave alone. For example, during the reinstallation process, you can leave your /home directory’s contents untouched while specifying that the /, /usr and /var partitions be reformatted. If you had the foresight to place your personal information in a separate directory such as /home, you will hardly notice that the default binaries are once again in place. If partitions such as /home and /usr/local reside on their own partition, they will remain unaffected.

> **NOTE**
> Many Linux users consider reinstallation to be a carry-over from Windows. Good Linux users usually do not need to reinstall. Usually the corrupted files can be reinstalled without damaging the system further. Consider reinstallation only as a last resort.

In only one instance have I been unable to restore a corrupted file system and needed to reinstall. When I was first learning Linux, a poorly written program blew away much of my root file system and damaged several system files needed to operate Linux. I learned three important lessons that day: first, exercise extreme caution when logged in as root; second, not to implicitly trust just any
