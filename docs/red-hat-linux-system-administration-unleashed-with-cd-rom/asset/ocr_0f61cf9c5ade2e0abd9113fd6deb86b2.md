Once this entry has been created, we can prepare the disks for autodetection and activation. Using the fdisk command, create a single large partition on /dev/sdb and /dev/sdc. Once these partitions are created, set the partition type to FD. Here is a sample session in which fdisk is used to perform this step on /dev/sdb and fdisk is used to perform the same step with a single command on /dev/sdc:

```
[root@hqtest18 /root]# fdisk /dev/sdb
```

The number of cylinders for this disk is set to 1106.

There is nothing wrong with that, but this is larger than 1024, and could in certain setups cause problems with:

+   1) software that runs at boot time (e.g., LILO)
+   2) booting and partitioning software from other OSs (e.g., DOS FDISK, OS/2 FDISK)

```
Command (m for help): p

Disk /dev/sdb: 255 heads, 63 sectors, 1106 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot  Start    End    Blocks   Id  System
/dev/sdb1      1   1106  8883913+  83  Linux
```

```
Command (m for help): d
Partition number (1-4): 1

Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-1106, default 1): 1
Last cylinder or +size or +sizeM or +sizeK (1-1106, default 1106): 1106
```

```
Command (m for help): p

Disk /dev/sdb: 255 heads, 63 sectors, 1106 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot  Start    End    Blocks   Id  System
/dev/sdb1      1   1106  8883913+  83  Linux
```