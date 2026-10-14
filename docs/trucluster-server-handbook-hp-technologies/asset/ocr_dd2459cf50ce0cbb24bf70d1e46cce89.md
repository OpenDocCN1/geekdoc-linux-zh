```
Enter your choice: 1
```

As we have chosen not to have a secondary swap partition, we answer "no" when prompted.

```
You may choose to have a second swapping area (swap2).
Do you want a second swapping area [y/n] ? n
```

In this section, we are prompted if we want to have a separate /var from /usr. In our case, we normally do keep /usr and /var as separate file systems. In keeping with tradition, we keep /var on the "h" partition. The /var file system is also on an AdvFS file system.

```
You can make /var a separate file system, or you can have it
share space on the /usr file system.
```

```
Should /var be a separate file system (y/n) ? y
```

```
Select the disk where the /var file system will reside, or
enter "ping <disk>" where <disk> is the device name (for example, dsk0)
to physically identify a particular disk.

Device      Size    Controller    Disk          Location
Name        in GB   Type          Model
1) dsk0      18.2    SCSI          BD018635C4    bus-5-targ-0-lun-0
...
```

```
Enter your choice: 1
```

```
Select the dsk0 partition where the /var file system will reside.

Partition   Size    Start         End           Overlaps
                Block         Block
1) e         3.9GB   10485760      18787864      c
2) f         2.0GB   18787864      22982168      c
3) h         2.0GB   31370776      35565080      c
```

```
Enter your choice: 3
```