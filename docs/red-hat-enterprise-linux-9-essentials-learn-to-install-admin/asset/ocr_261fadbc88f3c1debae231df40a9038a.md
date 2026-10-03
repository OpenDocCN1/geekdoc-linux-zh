# Adding a New Disk to a RHEL 9 Volume Group and Logical Volume

```
LV Status          available
# open             1
LV Size            <223.34 GiB
Current LE         57174
Segments           1
Allocation         inherit
Read ahead sectors auto
- currently set to 256
Block device       253:2
```

```
--- Logical volume ---
LV Path            /dev/rhel/root
LV Name            root
VG Name            rhel
LV UUID            OFqABO-azjy-47DO-bzRo-ha2O-sHz5-jjMPcF
LV Write Access    read/write
LV Creation host, time demoserver, 2023-04-10 14:11:17 -0400
LV Status          available
# open             1
LV Size            70.00 GiB
Current LE         17920
Segments           1
Allocation         inherit
Read ahead sectors auto
- currently set to 256
Block device       253:0
```

As shown in the above example, 70 GiB of the space in volume group rhel is allocated to logical volume root (for the / file system), approximately 223.34 GiB to the home volume group (for / home), and 3.75 GiB to swap (for swap space).

Now that we know what space is being used, it is often helpful to understand which devices are providing the space (in other words, which devices are being used as physical volumes). To obtain this information, we need to run the pvdisplay command:

```
# pvdisplay
--- Physical volume ---
PV Name            /dev/sda2
VG Name            rhel
PV Size            <297.09 GiB / not usable 4.00 MiB
Allocatable        yes (but full)
PE Size            4.00 MiB
Total PE           76054
Free PE            0
Allocated PE       76054
PV UUID            siKTC2-fq47-LXTG-VWtc-Ma33-XRCm-5uF63v
```