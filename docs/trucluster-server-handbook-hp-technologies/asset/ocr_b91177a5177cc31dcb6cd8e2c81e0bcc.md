Then execute "swapon -a" if you are adding additional swap space. If you are replacing the primary swap space, you will need to reboot for this change to take effect since you cannot yank a swap partition away from the OS. It should be noted that moving the swap space to a local disk is good for performance and reduces I/O to the shared bus, but it also makes that swap partition more vulnerable to a controller problem. If swap is moved to a local partition and there is a failure on that path, it could cause the system to hang or panic. If the swap partition is on a shared disk, you won’t face this problem if at least one member maintains access to the disk. Another benefit of having swap on a shared bus is if that member crashes and for some reason is not bootable, the crash dump can be processed by another cluster member and crash analysis can begin before the original member is even booted. For example, if we know that dsk6b is the other member’s swap partition and that the partition is large enough to hold the crash dump, we can process the dump and create the requisite vmunix.0 and vmzcore.0 files (and from those create crash-data.0 if we’re so inclined).

```
# /sbin/savecore -d /dev/disk/dsk6b .
System went down at Thu Jun 27 23:11:13 2002
Saving 23949312 bytes of image in vmzcore.0
```

```
# /usr/bin/crashdc vmunix.0 vmzcore.0 > crash-data.0
```

```
# ls
crash-data.0    vmunix.0    vmzcore.0
```

To see how swap is currently configured, issue the "swapon -s" command:

```
# swapon -s
Swap partition /dev/disk/dsk16b (default swap):
  Allocated space:     211639 pages (1.61GB)
  In-use space:        129 pages ( 0%)
  Free space:          211510 pages ( 99%)

Swap partition /dev/disk/dsk4b:
  Allocated space:     124063 pages (969MB)
  In-use space:        129 pages ( 0%)
  Free space:          123934 pages ( 99%)

Total swap allocation:
  Allocated space:     335702 pages (2.56GB)
  Reserved space:      11873 pages ( 3%)
  In-use space:          258 pages ( 0%)
  Available space:    323829 pages ( 96%)
```

In this example there are two swap partitions.