# F1 - to scan

First let’s run **ioscan** to see the disks on the system.

```
$ **/user/sbin/ioscan** -func disk
```

| Class | H | I/N Path | Driver | S/N State H/W Type | Description |
| --- | --- | --- | --- | --- | --- |
| disk | 2 | 10/0/5.0 | adisk | CLAIMED DEVICE | SEAGATE ST3150W |
| | /dev/dsk/c0t5d0 | /dev/rdsk/c0t5d0 | | | |
| disk | 3 | 10/0/6.0 | adisk | CLAIMED DEVICE | SEAGATE ST3150W |
| | /dev/dsk/c0t6d0 | /dev/rdsk/c0t6d0 | | | |
| disk | 6 | 10/4/4.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/clt4d0 | /dev/rdsk/clt4d0 | | | |
| disk | 7 | 10/4/4.5.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/clt4d5d0 | /dev/rdsk/clt4d5d0 | | | |
| disk | 8 | 10/4/4.6.0 | sdisk | CLAIMED DEVICE | SEAGATE ST3120W |
| | /dev/dsk/clt6d8 | /dev/rdsk/clt6d8 | | | |
| disk | 9 | 10/4/12.4.0 | adisk | CLAIMED DEVICE | SEAGATE ST3180W |
| | /dev/dsk/c2t4d0 | /dev/rdsk/c2t4d0 | | | |
| disk | 10 | 10/4/12.5.0 | adisk | CLAIMED DEVICE | SEAGATE ST3180W |
| | /dev/dsk/c2t5d0 | /dev/rdsk/c2t5d0 | | | |
| disk | 11 | 10/4/12.6.0 | adisk | CLAIMED DEVICE | SEAGATE ST31510W |
| | /dev/dsk/c2t6d0 | /dev/rdsk/c2t6d0 | | | |
| disk | 5 | 10/12/5.2.0 | adisk | CLAIMED DEVICE | TOSHIBA CD-ROM XM-5401TA |
| | /dev/dsk/c3t2d0 | /dev/rdsk/c3t2d0 | | | |

Note that the disks in this configuration correspond to those on the top of Figure 9-4. We haven’t yet looked at the logical volume information related to these disks, only their physical addresses.

# F1 - vgdisplay

Next run **vgdisplay** to see the volume groups. **lv0l2** on **vg0** is the dump logical volume we are going to move to a separate 2 GByte disk. We don’t yet know if **lv0l1-7** on **vg0** are all mirrored.

```
## **vgdisplay** -v
--- Volume groups ---
VG Name /dev/vg00
VG Write Access read/write
VG Status available
Max LV 255
Cur LV 7
Open LV 7
Max PV 16
Cur PV 2
Act PV 2
```