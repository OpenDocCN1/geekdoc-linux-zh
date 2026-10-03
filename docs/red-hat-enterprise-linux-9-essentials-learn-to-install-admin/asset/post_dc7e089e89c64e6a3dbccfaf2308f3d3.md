
## Adding a New Disk to a RHEL 9 Volume Group and Logical Volume

```
= reflink=1 bigtime=1 inodecount=1
data = bsize=4096 blocks=58546176, imaxpct=25
= sunitt=0 swidth=0 blks
naming =version 2 bsize=4096 ascii-ci=0, ftype=1
log =internal log bsize=4096 blocks=28587, version=2
= sectsz=512 sunitt=0 blks, lazy-count=1
realtime =none extsz=4096 blocks=0, rtextents=0
data blocks changed from 58546176 to 62216192
```

If, on the other hand, the filesystem is of type ext2, ext3, or ext4, the resize2fs utility should be used instead when performing the filesystem resize:

```
# resize2fs /dev/rhel/home
```

Once the resize completes, the file system will have been extended to use the additional space provided by the new disk drive. All this has been achieved without moving a single file or restarting the server. As far as users on the system are concerned, nothing has changed (except that there is now more disk space).

### 32.4 Adding Additional Space to a Volume Group Using Cockpit

In addition to the command-line utilities outlined so far in this chapter, it is also possible to access information about logical volumes and make volume group and logical volume changes from within the Cockpit web interface using the Storage page, as shown in Figure 32-1:

![](img/be1f159c3cc937d7b264dc5b134856dc_265_0.png)

Figure 32-1

If the Storage option is not listed, the cockpit-storaged package will need to be installed, and the cockpit service restarted as follows:

```
# dnf install cockpit-storaged
# systemctl restart cockpit.socket
```

Once the Cockpit service has restarted, log back into the Cockpit interface, at which point the Storage option should now be visible.

To add a new disk drive to an existing volume group from within the Cockpit console, start at the above Storage page and click on a filesystem associated with the volume group to be extended from the list marked A above.

On the resulting screen, click on the + button highlighted in Figure 32-2 below to add a physical volume:

![](img/be1f159c3cc937d7b264dc5b134856dc_266_0.png)

Figure 32-2

Select the new drive to be added to the volume group and click on the Add button:

![](img/be1f159c3cc937d7b264dc5b134856dc_266_1.png)

Figure 32-3

On returning to the volume group screen, scroll down to the logical volume to be extended and click on it to unfold additional information. Figure 32-4, for example, shows details of the home logical volume:

![](img/be1f159c3cc937d7b264dc5b134856dc_267_0.png)

Figure 32-4

To extend the logical volume using the new space, click the Grow button and use the slider in the resulting dialog to select how much space should be added to the volume. Then, click the Grow button to commit the change (the available space can be shared among different volume groups if required):

![](img/be1f159c3cc937d7b264dc5b134856dc_267_1.png)

Figure 32-5

Once these steps are complete, the volume group will have been configured to use the newly added space.

### 32.5 Summary

Volume groups and logical volumes provide an abstract layer on top of the physical storage devices on a RHEL 9 system to provide a flexible way to allocate the space provided by multiple disk drives. This allows disk space allocations to be made and changed dynamically without the need to repartition disk drives and move data between filesystems. This chapter has outlined the basic concepts of volume groups and logical and physical volumes while demonstrating how to manage these using command-line tools and the Cockpit web interface.

## 33. Adding and Managing RHEL 9 Swap Space

An essential part of maintaining the performance of a RHEL 9 system involves ensuring that adequate swap space is available comparable to the memory demands placed on the system. Therefore, this chapter provides an overview of swap management on RHEL 9.

### 33.1 What is Swap Space?

Computer systems have a finite amount of physical memory available to the operating system. When the operating system approaches the available memory limit, it frees up space by writing memory pages to disk. When the operating system requires any of those pages, they are read back into memory. The disk area allocated for this task is referred to as swap space.

### 33.2 Recommended Swap Space for RHEL 9

The swap recommended for RHEL 9 depends on several factors, including the amount of memory in the system, the workload imposed on that memory, and whether the system is required to support hibernation. The current guidelines for RHEL 9 swap space are as follows:

| Amount of installed RAM | Recommended swap space | Recommended swap space if hibernation enabled |
|---|---|---|
| 2GB or less | Installed RAM x 2 | Installed RAM x 3 |
| 2GB - 8GB | Installed RAM x 1 | Installed RAM x 2 |
| 8GB - 64GB | At least 4GB | Installed RAM x 1.5 |
| 64GB or more | At least 4GB | Hibernation not recommended |

Table 33-1

When a system enters hibernation, the current system state is written to the hard disk, and the host machine is powered off. When the machine is subsequently powered on, the system's state is restored from the hard disk drive. This differs from suspension, where the system state is stored in RAM. The machine then enters a sleep state whereby power is maintained to the system RAM while other devices are shut down.

### 33.3 Identifying Current Swap Space Usage

The current amount of swap used by a RHEL 9 system may be identified in several ways. One option is to output the /proc/swaps file:

```
# cat /proc/swaps
Filename Type Size Used Priority
/dev/dm-1    partition    3932156    0    -2
```

Alternatively, the *swapon* command may be used:

```
# swapon
NAME    TYPE    SIZE USED PRIO
/dev/dm-1 partition 3.7G 0B -2
```

To view the amount of swap space relative to the overall available RAM, the *free* command may be used:

```
# free
            total       used       free     shared    buff/cache   available
Mem:       3601420   1577696   1396172    404412     1273236     2023724
Swap:      3932156        0   3932156
```

### 33.4 Adding a Swap File to a RHEL 9 System

Additional swap space may be added to the system by creating a file and assigning it as swap. Begin by creating the swap file using the dd command. The size of the file can be changed by adjusting the count variable. The following command line, for example, creates a 2.0 GB file:

```
# dd if=/dev/zero of=/newswap bs=1024 count=2000000
2000000+0 records in
2000000+0 records out
2048000000 bytes (2.0 GB, 1.9 GiB) copied, 29.3601 s, 69.8 MB/s
```

Before converting the file to a swap file, it is essential to make sure the file has secure permissions set:

```
# chmod 0600 /newswap
```

Once a suitable file has been created, it needs to be converted into a swap file using the mkswap command:

```
# mkswap /newswap
Setting up swapspace version 1, size = 1.9 GiB (2047995904 bytes)
no label, UUID=28d314e9-492f-46f8-bdcf-3a734c4426db5
```

With the swap file created and configured, it can be added to the system in real-time using the swapon utility:

```
# swapon /newswap
```

Re-running swapon should now report that the new file is now being used as swap:

```
# swapon
NAME    TYPE    SIZE USED PRIO
/dev/dm-1 partition 3.7G 1M -2
/newswap file    1.9G 0B -3
```

The swap space may be removed dynamically by using the swapoff utility as follows:

```
# swapoff /newswap
```

Finally, modify the /etc/fstab file to automatically add the new swap at system boot time by adding the following line:

/newswap  swap  swap  defaults 0 0

### 33.5 Adding Swap as a Partition

As an alternative to designating a file as swap space, entire disk partitions may also be designated as swap. The steps to achieve this are the same as those for adding a swap file. Before allocating a partition to swap, ensure that any existing data on the corresponding filesystem is either backed up or no longer needed and that the filesystem has been unmounted.

Assuming that a partition exists on a disk drive represented by /dev/sdb1, for example, the first step would be to convert this into a swap partition, once again using the mkswap utility:

```
# mkswap /dev/sdb1
Setting up swapspace version 1, size = 14.5 GiB (15524163584 bytes)
no label, UUID=306b7fee-eb20-4679-9f14-f94548683557
```

Next, add the new partition to the system swap and verify that it has indeed been added:

```
# swapon /dev/sdb1
[root@demoser ver ~]# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition 3.7G 996K  -2
/dev/sdb1 partition 14.5G 0B   -3
```

Once again, the /etc/fstab file may be modified to automatically add the swap partition at boot time as follows:

/dev/sdb1  swap  swap  defaults 0 0

### 33.6 Adding Space to a RHEL 9 LVM Swap Volume

On systems using Logical Volume Management, an alternative to adding swap via file or disk partition is to extend the logical volume used for the swap space.

The first step is to identify the current amount of swap available and the volume group and logical volume used for the swap space using the lvdisplay utility (for more information on LVM, refer to the chapter entitled “Adding a New Disk to a RHEL 9 Volume Group and Logical Volume”):

```
# lvdisplay
--- Logical volume ---
LV Path              /dev/rhel/swap00
LV Name              swap00
VG Name              rhel
LV UUID              EbOScj-1qXw-bB9d-LU61-ZjdC-L7u5-Uhj8De
LV Write Access      read/write
LV Creation host, time demoserver, 2023-04-12 09:34:29 -0400
LV Status            available
# open                2
LV Size              3.75 GiB
Current LE           960
```
