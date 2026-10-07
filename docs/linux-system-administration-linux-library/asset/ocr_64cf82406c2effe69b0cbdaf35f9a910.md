experience is of limited use in making judgment, because the systems may be used in radically different ways. Once you've gained some experience, or if you see a compelling reason to do so initially, you may want to separate partitions for /var, /tmp, /usr/local/, /opt, and other directories.

# Linux Disk-Partitioning Software

Linux's main partitioning tool is called fdisk (for fixed disk). It's named after the DOS FDISK utility but works quite differently. To use fdisk, type its name followed by the device file you want to modify, such as /dev/sda or /dev/hdb, thus:

```
# fdisk /dev/hdb
```

> **WARNING** Every x86 OS has its own disk-partitioning software. Linux's fdisk is unusually flexible, but can produce partitions that other OSs don't like. As a general rule of thumb, you should use each OS's partitioning tools to create its partitions. Alternatively, you can use a more OS-agnostic tool, such as PartitionMagic, to do the job for all OSs.

On modern disks, you'll likely be told that the number of cylinders exceeds 1024. You can safely ignore this warning, except to know that it's best to place the Linux boot partition below the 1024-cylinder limit. Once fdisk is running, you see only a prompt that below reads command (m for help): You type single-letter commands at this prompt in order to accomplish various tasks. You can type m or ? to see what these commands are. Table 10.3 summarizes the most important ones.

# **Table 10.3** Important Linux fdisk Commands

| Command | Meaning |
|---|---|n| d | Deletes a partition |
| l | Displays a list of known partition type codes |
| m or ? | Displays a summary of commands |
| n | Creates a new partition |
| p | Displays the disk's current partition table |