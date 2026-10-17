
```
# vgdisplay -v /dev/vg_nw
VG Name /dev/vg_nw
VG Write Access read/write
VG Status available
Max LV 2^5
Cur LV 4
Open LV 4
Max PV 1
Cur PV 6
Act PV 6
Max PE per PV 6 ^2^3
VGDA 12
PE Size (Mbytes) 4
Total PE 6416
Alloc PE 5416
Free PE 722
Total PVs 2
--- Logical volumes ---
LV Name /dev/vg_nw/lv.nwtext
LV Status available/syncd
LV Size (Mbytes) 4092
Current LE 1023
Allocated PE 2046
Used PV 2

LV Name /dev/vg_nw/lv.nwsys
LV Status available/syncd
LV Size (Mbytes) 4092
Current LE 1023
Allocated PE 2046
Used PV 2

LV Name /dev/vg_nw/lv.nwbackup
LV Status available/syncd
LV Size (Mbytes) 2548
Current LE 637
Allocated PE 1274
Used PV 2
```

# F10

使用 `vgextend` 将 4 GByte 的磁盘添加到 `vg00` 以实现镜像（此处可能还需要运行 `pvcreate`）。

```
# vgextend /dev/vg00 /dev/dsk/c1t3d0
Volume group `/dev/vg00' has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in `/etc/lvmconf/vg00.conf'
```

# F11

现在我们可以创建新的 2 GByte 磁盘并将其添加到 `vg00` 中，使用以下两个命令：`pvcreate` (F11) 用于创建物理卷，`vgextend` (F12) 用于扩展卷组。

```
# pvcreate -f /dev/rdsk/c0t5d0
Physical volume `/dev/rdsk/c0t5d0* has been successfully created.
```

# F12

```
# vgextend /dev/vg00 /dev/dsk/c0t5d0
Volume group `/dev/vg00' has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in `/etc/lvmconf/vg00.conf'
```

# F13

我们可以使用 `vgdisplay` 检查这两个磁盘是否确实已添加到 `vg00`。在我们的示例中，仅显示 `lvoll` 到 `lv013`。

显示的末尾部分是列表中的重要部分，显示三个物理卷。

```
# vgdisplay -v /dev/vg00

--- Volume groups ---
VG Name /dev/vg00
VG Write Access read/write
VG Status available
Max LV 255
Cur LV 7
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
Total PVs 1

--- Logical volumes ---
LV Name /dev/vg00/lv01
LV Status available/syncd
LV Size (Mbytes) 32
Current LE 33
Allocated PE 32
Used PV 1

LV Name /dev/vg00/lv02
LV Status available/syncd
LV Size (Mbytes) 900
Current LE 125
Allocated PE 125
Used PV 1

LV Name /dev/vg00/lv013
LV Status available/syncd
LV Size (Mbytes) 20
Current LE 5
Allocated PE 5
Used PV 1

--- Physical volumes ---
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

# F14

我们现在可以使用 `lvcreate` (`F14`) 在 `vg00` 中创建 `dump` 逻辑卷，使用 `lvextend` (`F15`) 将其扩展到 `2 GB`，并使用 `lvdisplay` (`F16`) 查看它。

```
# lvcreate -n dump /dev/vg00
Logical volume "/dev/vg00/dump" has been successfully created with character device "/dev/vg00/rdump".
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F15

```
# lvextend -l 508 /dev/vg00/dump /dev/dsk/c0t5d0
Logical volume "/dev/vg00/dump" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F16

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
PV Name    LE on PV  PE on PV
/dev/dsk/c0t5d0  508  0  508
```

# F17

为了使 `/dev/vg00/dump` 成为 `dump` 设备，我们必须首先使用 `lvchange` 使其连续，然后使用 `lvinboot` 将其设为 `dump` 设备。

```
# lvchange -C y /dev/vg00/dump
```

```
# lvinboot -d /dev/vg00/dump
```

# F18

查看 dump 设备。

```
# lvlnboot -v | more
Boot Definitions for Volume Group /dev/vg00:
Physical Volumes belonging in Root Volume Group:
  /dev/dsk/c0t6d0 (10/0.6.0) -- Boot Disk
  /dev/dsk/c1t3d0 (10/4/4.3.0) -- Boot Disk
  /dev/dsk/c0t5d0 (10/0.5.0)
Root: lvol1  on:  /dev/dsk/c0t6d0
Swap: lvol2  on:  /dev/dsk/c0t6d0
Dump: lvol2 on:  /dev/dsk/c0t6d0, 0
Dump: dump  on:  /dev/dsk/c0t5d0, 1
```
