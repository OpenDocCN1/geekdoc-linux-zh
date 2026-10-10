# F14

We can now create the **dump** logical volume in **vg00** with **lvcreate** (**F14**), extend it to **2 GB** with **lvextend** (**F15**), and view it with **lvdisplay** (**F16**).

```
```
# lvcreate -n dump  /dev/vg00
Logical volume "/dev/vg00/dump" has been successfully created with character de-
vice "/dev/vg00/rdump".
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```
```

# F15

```
```
# lvextend -l 508 /dev/vg00/dump /dev/dsk/c0t5d0
Logical volume "/dev/vg00/dump" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```
```

# F16

```
```
# lvdisplay /dev/vg00/dump | more
--- Logical volumes ---
LV Name           /dev/vg00/dump
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  2032
Current LE        508
Allocated PE      508
Stripes           0
Stripe Size (Kbytes) 0
Bad Block         on
Allocation        strict

--- Distribution of logical volume ---
PV Name    LE on PV  PV on PV
/dev/dsk/c0t5d0  508  0  508
.  .  .
.  .  .
```
```

# F17

In order to make **/dev/vg00/dump** the **dump** device, we must first make it contiguous with **lvchange** and then make it a **dump** device with **vlnboot**.