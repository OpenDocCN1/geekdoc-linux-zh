This listing shows that the four internal disks are at **SBA 0**, **LBA 0**, and SCSI buses **1** and **2**, respectively. At the time of this writing these disks have to be in the same vPar because they are on the same LBA.

To assign the LBA to which the L-Class disks are connected as well as the two disks to a vPar, we would use the full hardware paths of -i **0/0** to assign the LBA to a Virtual Partition and -i **0/0/1/1.2.0:boot** for the boot disk of that Virtual Partition.

The internal disks are not the only disks attached to our L-Class system. There is also an external disk enclosure on which we have created several Logical UNIts (LUNs) that appear as separate disk drives. If we run `ioscan` and `grep` for disk we see that several of these exist:

```
```
cvhbcon3:/ # ioscan -f | grep disk
disk          0    0/0/1/0.0             sdisk    CLAIMED    DEVICE    HP        DVD-ROM 304
disk          2    0/0/1/1.2.0          sdisk    CLAIMED    DEVICE    SEAGATE ST173404LC
disk          3    0/0/2/0.0.0          sdisk    CLAIMED    DEVICE    SEAGATE ST173404LC
disk          4    0/0/2/0.2.0          sdisk    CLAIMED    DEVICE    SEAGATE ST173404LC
disk          7    0/0/0/0.0.0.5.0.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         10    0/0/0/0.0.0.5.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         11    0/0/0/0.0.0.5.0.2    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         12    0/0/0/0.0.0.5.0.3    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         15    0/0/0/0.0.0.5.1.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         17    0/0/0/0.0.0.5.2.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         18    0/0/0/0.0.0.5.3.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          5    0/0/0/0.0.0.4.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          6    0/0/0/0.0.0.4.0.1    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          8    0/0/0/0.0.0.4.0.2    sdisk    CLAIMED    DEVICE    HP        AS577A
disk          9    0/0/0/0.0.0.4.0.3    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         13    0/0/0/0.0.0.4.1.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         14    0/0/0/0.0.0.4.2.0    sdisk    CLAIMED    DEVICE    HP        AS577A
disk         16    0/0/0/0.0.0.4.3.0    sdisk    CLAIMED    DEVICE    HP        AS577A
cvhbcon3:/ #
```
```

This listing shows first the DVD-ROM, then the four internal disks, and finally, the 14 LUNs configured on our external storage enclosure. We used one of these for the boot volume of `cable2`. The following `vparstatus -v` command shows the respective boot disks of `cable1` and `cable2`:

![](bbox=[0.08, 0.75, 0.13, 0.85])

```
```
# vparstatus -v

[Virtual Partition Details]
Name:			cable1
State:			Up
Attributes:		Dynamic,Manual
Kernel Path:		/stand/vmunix
Boot Options:

[CPU Details]
```
```