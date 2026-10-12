```
: (continued)
--- Logical volume
LV Name /dev/vgu01/lvu01
VG Name vgu01
LV UUID REW0TH-erkC-Z3P5-yzFb-1a0W-HTLy-
c0aMPR
LV Write Access read/write
LV Status available
# open 2
LV Size 5.70 GB
Current LE 1460
Segments 3
Allocation inherit
Read ahead sectors 0
Block device 253:8
--- Physical volumes
PV Name /dev/dasd0
PV UUID 5pXoDK-9M1Z-zH4i-iyM0-Jny6-YTCW-
8Gz1K0
PV Status allocatable
Total PE / Free PE 307 / 0
```

Figure 6-14 vgdispaly -v (continued)

LVs in the VG

UUID of the LV
(it is recorded in meta-data area of PVs)

If the vg id deactivated, "NOT available" is displayed.

num of processes which open the LV. If it is not "0", the LV cannot be deactivated.

device number of the LV(major:minor)
These have same major:minor number.

+   - /dev/mapper/vgu01-lvu01
+   - /dev/dm-8
+   - /dev/vgu01/lvu01

PVs which compose the VG.

UUID of the PV
(it is recorded in meta-data area of PVs)