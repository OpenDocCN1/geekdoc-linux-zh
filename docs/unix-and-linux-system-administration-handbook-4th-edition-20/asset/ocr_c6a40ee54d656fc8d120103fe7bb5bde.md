# Traditional partitioning

+   - Since log files are kept in /var, it's a good idea for /var to be a separate disk partition. Leaving /var as part of a small root partition makes it easy to fill the root and bring the machine to a halt.

+   - It's useful to put users' home directories on a separate partition or even if the root partition is corrupted or destroyed, user data has a good chance of remaining intact. Conversely, the system can continue to operate after a user's misguided shell script fills up to /home.

+   - Splitting swap space among several physical disks increases performance. This technique works for filesystems, too; but the busy ones on different disks. See page 1129 for notes on this subject.

+   - As you add memory to your machine, you should also add swap space. See page 1124 for more information about virtual memory.

+   - Backups of a partition may be simplified if the entire partition can fit on one piece of media. See page 294.

+   - Try to cluster quickly-changing information on a few partitions that are backed up frequently.

# Traditional partitioning

Systems that allow partitions implement them by writing a "label" at the beginning of the disk to define the range of blocks included in each partition. The exact details vary; the label must coexist with other startup information (such as a boot block), and it often contains extra information such as a name or unique ID that identifies the disk as a wheel. Under Windows, the label is known as the MBR, or master boot record.

The device driver for representing the disk reads and uses the partition table to calculate the physical location of each partition. Typically, one or two devices represent each partition (one block device and one character device; Linux has only block devices). Also, a separate set of device files represents the disk.

Solaris calls partitions "slices", or more accurately, it calls them slices when they are implemented with a Solaris-style label and partitions that are implemented with a Windows-style MBR. Slice 2 includes the entire expanse of the disk, illustrating the rather truth that not one slice can claim a given disk. Perhaps the word "slices" was selected because "partition" gets a simple division, whereas slices overlap. The terms are otherwise interchangeable.

Despite the universal availability of logical volume managers, some situations still require or benefit from traditional partitioning.

+   - On PC hardware, the boot disk must have a partition table. Most systems require MBR partitioning (see Windows-style partitioning, next), but

![](bbox=[0.948, 0.442, 0.996, 0.545])