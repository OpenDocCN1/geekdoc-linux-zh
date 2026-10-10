
## F1 - lvlnboot

Next, look at the boot information with `lvlnboot`. `lvol2` on `vg00` is the dump device.

```
# lvlnboot -v /dev/vg00
Boot Definitions for Volume Group: /dev/vg00:
Physical Volumes belonging in Root Volume Group:
/dev/dsk/c0t5d0 (10/0.6.0) -- Boot Disk
/dev/dsk/c0t5d0 (10/0.6.0)
Root: lvol1 on: /dev/dsk/c0t5d0
Swap: lvol2 on: /dev/dsk/c0t5d0
Dump: lvol2 on: /dev/dsk/c0t5d0, 0
```

## F1 - lfls

Look at the boot area with `lfls`.

```
# lfls -Civ /dev/dsk/c0t5d0
volume ISTD data size 7984 directory size 8 94/11/10 14:46:53
filename type start size implement created
CDE -12960 584 496 0 95/05/19 13:10:50
MAPFILE -12277 1080 32 0 95/05/19 13:16:50
SYSID -12280 1112 224 0 95/05/19 13:18:50
CONFINFO -12278 1336 62 0 95/05/19 13:14:50
LVMOD -12278 1400 70 0 95/05/19 13:15:50
SUNWY -12276 1472 68 0 95/05/19 13:16:50
SLUMDB -12276 1544 244 0 95/05/19 13:16:50
MAPPER -12279 1792 91 0 95/05/19 13:14:50
IOTEST -12279 1888 150 0 95/05/19 13:16:51
PERFVER -12279 2040 80 0 95/05/19 13:14:51
TUNT -12901 2120 64 0 95/05/19 13:18:52
SYSNGO -12980 2184 1 0 96/09/16 09:04:01
ZIL -12880 2192 240 0 94/11/04 15:46:52
AUID -12289 2432 1 0 94/11/04 15:44:54
HMIN -12928 2440 800 0 94/11/04 15:44:54
LABEL BIN 3240 8 0 96/05/29 01:43:52
```

## F2

After all the appropriate information has been saved for the existing configuration, we can begin the reconfiguration. First, we break the mirror with `lvreduce` and the `-m` option.

```
# lvreduce -m 0 /dev/vg00/lvol1
Logical volume "/dev/vg00/lvol1" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol2
Logical volume "/dev/vg00/lvol2" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol3
Logical volume "/dev/vg00/lvol3" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol4
Logical volume "/dev/vg00/lvol4" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol5
Logical volume "/dev/vg00/lvol5" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol6
Logical volume "/dev/vg00/lvol6" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
# lvreduce -m 0 /dev/vg00/lvol7
Logical volume "/dev/vg00/lvol7" has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

You can type each command or make a file with the `lvreduce` commands in it and run the file. You can call the file `/tmp/reduce` with the following entries:

```
lvreduce -m 0 /dev/vg00/lvol1
lvreduce -m 0 /dev/vg00/lvol2
lvreduce -m 0 /dev/vg00/lvol3
lvreduce -m 0 /dev/vg00/lvol4
lvreduce -m 0 /dev/vg00/lvol5
lvreduce -m 0 /dev/vg00/lvol6
lvreduce -m 0 /dev/vg00/lvol7
```

After you create this file, change it to executable and then run with the following two commands.

```
# chmod 555 /tmp/reduce
# /tmp/reduce
```

You will then see all the output of having run the `lvreduce` commands.

## F3

Check to see that mirroring of `lvol1`-`7` has been reduced with `lvdisplay`. Look to see that mirrored copies are equal to 0. Only `lvol1` through `lvol3` are shown in this listing.

## Reconfiguring Some Disks: An Example of Using Some Logical Volume Commands

```
# lvdisplay -v /dev/vg00/lvol* | more
--- Logical volumes
LV Name           /dev/vg00/lvol1
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  92
Current LE        23
Allocated PE      -
Stripes           0
Stripe Size (Kbytes) 0
Bad block         off
Allocation        strict/contiguous

LV Name           /dev/vg00/lvol2
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  500
Current LE        125
Allocated PE      125
Stripes           0
Stripe Size (Kbytes) 0
Bad block         off
Allocation        strict/contiguous

LV Name           /dev/vg00/lvol3
VG Name           /dev/vg00
LV Permission     read/write
LV Status         available/syncd
Mirror copies     0
Consistency Recovery MWC
Schedule          parallel
LV Size (Mbytes)  20
Current LE        5
Allocated PE      5
Stripes           0
Stripe Size (Kbytes) 0
Bad block         on
Allocation        n't't.
```

## F4

Now remove `c0t5d0` from `vg00` with `vgreduce`. Since there is no mirroring in place, this approach will work. This disk will be put on a different SCSI controller and again used for mirroring later in the procedure.

```
# vgreduce /dev/vg00 /dev/dsk/c0t5d0
Volume Group /dev/vg00 has been successfully reduced.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

## F5

At this point `c0t5d0` is no longer in `vg00`. Verify that "PV Name" `c0t5d0` is no longer in `vg00` with `vgdisplay`.

```
# vgdisplay -v
```

There should be no `c0t5d0` in `vg00`.

## F6

Verify that "dump lvol" is in /stand/system. If not, add "dump lvol" and reconfigure the kernel. See the kernel rebuild procedure in Chapter 1.

## F7

Now the hardware upgrade takes place. The system is shut down, disk drives are added and moved, and the system is rebooted. The 4 GByte disk `/dev/dsk/c0t5d0` becomes `/dev/dsk/c1t3d0` at address 10/4/4,3.0, and a new 2 GByte disk is introduced as 10/0,5.0 with the device name `/dev/dsk/c0t5d0`. The second half of Figure 9-4 depicts this change.

## F8

The first activity to perform after the hardware upgrade is to view the new disks with `ioscan`. There is now a 2 GByte disk at 10/0,5.0 and a 4 GByte disk at 10/4/4,3.0.

```
# iostat -func disk
```

| Class | I | H/W Path | Driver | S/W State | H/W Type | Description |
|---|---|---|---|---|---|---|
| disk | 2 | 10/0,5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST332555W |
| disk | 3 | 10/0,6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST31550W |
| disk | 12 | 10/4/4.3.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 6 | 10/4/4.4.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 7 | 10/4/4.5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 8 | 10/4/4.6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 9 | 10/4/12.4.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 10 | 10/4/12.5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 11 | 10/4/12.6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST15150W |
| disk | 5 | 10/12/5.2.0 | sdisk | CLAIMED | DEVICE | TOSHIBA CD-ROM XM-5401TA |

## F9

Now we run `vgdisplay` to see new volume group information. Only `c0t6d0` is in `vg00` and no mirroring is yet configured. The other volume groups have remained the same. Only `lvol1` through `lvol3` are shown in our example.

```
# vgdisplay -v

--- Volume groups ---
VG Name                 /dev/vg00
VG Write Access         read/write
VG Status               available
Max LV                  255
Cur LV                  7
Open LV                 7
Max PV                  16
Cur PV                  1
Act PV                  1
Max PE per VV           1023
VVDA                    2
PE Size (Mbytes)        4
Total PE                1023
Alloc PE                344
Free PE                 679
Total PVG               0

--- Logical volumes ---
LV Name                 /dev/vg00/lvol1
LV Status               available/syncd
LV Size (Mbytes)        92
Current LE              23
Allocated PE            23
Used PV                 1
```
