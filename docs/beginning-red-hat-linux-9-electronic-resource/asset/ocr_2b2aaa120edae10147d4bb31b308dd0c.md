# Chapter 7

> An alternative is to list the contents of /proc/partitions, which lists all the currently available partitions including those that have not been mounted yet. Here is the listing of a typical /proc/partitions file. For our purposes, it is sufficient to look for a new row in the table and note the name column, in this case hdb.

```
$ cat /proc/partitions
major minor #blocks name
22 0 661728 hdo 40 32 280 500 0 0 0 -24865 2297424 1939878
3 0 6297480 hda 17031 21392 305170 253707 11959 16564 228632 422367 -1 6577905 2337991
3 1 104391 hda1 35 85 240 408 14 6 40 244 0 636 652
3 2 5807497 hda2 16967 21086 304394 252974 11788 14238 208776 250927 0 188263 503912
3 3 385560 hda3 9 25 104 146 157 2320 19816 171195 0 3453 171341
```

If there are no kernel startup messages or listings in /proc/partitions, then it is quite likely that the disk was not detected. There are several possible reasons for the system's failure to detect the disk. To eliminate the possibility of a hardware setup problem, we should check all hardware settings such as the master-slave mode settings of the hard disk and compare them with the manufacturer's recommended settings. It's possible that the detection failure may have occurred because the correct driver is missing from the kernel; this problem can be remedied by re-compiling a kernel, or by using a dynamically loadable kernel module that has support for the new hard disk. Chapter 10 has details on how to perform these steps.

# Partitioning the Hard Disk

Once the disk has been detected, it is usually assigned a /dev name (such as /dev/hdb) automatically by the system. Once we know what this name is, as can be seen from the dmesg output or the /proc/partitions file, we need to partition the device.

If we intend to create a swap partition on this disk, the rule of thumb is to create a partition that is at least 2.5 times the size of the available physical RAM. We may use parted, fdisk, sfdisk (or another similar command) to partition the new drive. During the partitioning process, it is necessary to specify the intended file system for this hard disk.

# Formatting the Hard Disk

After partitioning, the next logical step is to format the disk. The formatting process prepares the partition for a certain file system type to create files and directories. During this process several file system-specific information may be created on the partitions. Formatting is very much specific to the file system that will be installed on the partition. For instance, to format the first partition of the /dev/hdb disk to use the ext3 file system, the following command is used:

```
# mkfs.ext3 -c /dev/hdb1
```

The -c option forces a check for disk errors.