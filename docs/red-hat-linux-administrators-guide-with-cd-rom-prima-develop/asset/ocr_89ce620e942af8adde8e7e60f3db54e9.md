drives installed and to assist in their partitioning. Table 1.3 shows a sample configuration for a system similar to that of one of my many machines. I have a 200 MHz Pentium with 64 megabytes of RAM and three actual drives, the first two of which are IDE and the last being SCSI. The table shows how I partitioned the file systems across the three physical drives.

# **Table 1.3 A Sample Partitioning Scheme across Three Hard Drives**

| Partition Name | File System | Size (MB) | Description |
| :--- | :--- | :--- | :--- |
| `/` | /dev/hda1 | 400 | Root directory |
| swap | /dev/hda2 | 100 | Swap space |
| /home | /dev/hdb1 | 500 | Home directory |
| /usr | /dev/hdb2 | 500 | Binaries |
| /usr/local | /dev/sda1 | 300 | My own programs |
| /var | /dev/sda2 | 200 | Log messages |


As you can see, the first IDE drive, hda, has only 500 megabytes of space, while the second is about 1,000 megabytes. The third drive, identified by the device label sda (for SCSI drive), is also about 500 megabytes.

> > **CAUTION**
> >
> > Once you have saved the new partitions and written them to disk, all information formerly found on that drive is lost. Be sure you are absolutely sure that this is what you want before deleting and creating new partitions.

The partitioning format here is much like that of the schemes used earlier in this chapter. You are free to place additional directories in other partitions. However, I have found it useful to keep the partitions to a minimum in case I need to add more drives later. That way a unique directory not allocated to a partition can be dedicated entirely to the new hard drive. This requires adding the new drive device to the /etc/fstab file and then mounting the partition.

The latest Red Hat Linux makes this task simpler with the kudzu utility. Much as Windows can find and determine the type of new hardware placed in the machine, Linux accomplishes the same task and can update the drivers and