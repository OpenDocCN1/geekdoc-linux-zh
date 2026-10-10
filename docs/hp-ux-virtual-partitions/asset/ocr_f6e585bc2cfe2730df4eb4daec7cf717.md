The end of the display is the significant part of the listing showing three physical volumes.

```
# vgdisplay -v /dev/vg00

--- Volume groups ---
VG Name /dev/vg00
VG Write Access read/write
VG Status available
Max LV 255
C-i LV 7
Open LV /
Max PV 8
Cur PV 1
Act PV 1
Max PE per PV 1051
VGA
PG Size (Mbytes) 4
Total PE 456
Alloc PE 444
Free PE 12
Totoi PVG 1

--- Logical volumes -

LV Name /dev/vg00/lv01
LV Status available/syncd
LV Size (Mbytes) 32
Current Le 33
Allocated PE 32
Used PV 1

LV Name /dev/vg00/lv02
LV Status available/syncd
LV Size (Mbytes) 900
Current Le 125
Allocated PE 125
Used PV 1

LV Name /dev/vg00/lv013
LV Status available/syncd
LV Size (Mbytes) 20
Current Le 5
Allocated PE 5
Used PV 1

--- Physical volumes

PV Name /dev/dsk/ct0d10
PV Status available
Total PE 1023
Free PE 679

PV Name /dev/dsk/ct32d0
PV Status available
Total PE 1023
Free PE 1023

PV Name /dev/dsk/ct54d0
PV Status available
Total PE 508
Free PE 508
```