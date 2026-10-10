
# F9

仅显示 `/dev/vg_nw` 中的前三个逻辑卷。

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

我们现在可以使用 **lvcreate** (**F14**) 在 **vg00** 中创建 **dump** 逻辑卷，使用 **lvextend** (**F15**) 将其扩展到 **2 GB**，并使用 **lvdisplay** (**F16**) 查看它。

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

为了使 **/dev/vg00/dump** 成为 **dump** 设备，我们必须首先使用 **lvchange** 使其连续，然后使用 **lvinboot** 将其设为 **dump** 设备。

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

这可能不是你想要的结果。如“0”所示，主 dump 设备是 /dev/dsk/c0t6d0，如“1”所示，次要 dump 设备是 /dev/dsk/c0t5d0。我们可以选择重新执行此操作。让我们先继续对 /dev/vg00 上的 lvol 进行镜像，稍后再处理 dump 设备。

# F19

让我们现在使用 lvextend 扩展 vg00 中所有卷以用于一个镜像。

```
# lvextend -m 1 /dev/vg00/lvol1 /dev/dsk/c1t3d0
The newly allocated mirrors are now being synchronized.
This operation will take some time. Please wait . . .
Logical volume "/dev/vg00/lvol1" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

将以下内容放入 /tmp/mirror 并运行。lvol1 之前已扩展：lvol2 是交换分区，无需扩展：

```
lvextend -m 1 /dev/vg00/lvol3 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol4 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol5 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol6 /dev/dsk/c1t3d0
lvextend -m 1 /dev/vg00/lvol7 /dev/dsk/c1t3d0
```

```
The newly allocated mirrors are now being synchronized.
This operation will take some time.
Please wait.... Logical volume "/dev/vg00/lvol2" has been successfully extended.
Volume Group configuration for /dev/vg00 has been saved in /etc/lvmconf/vg00.conf
```

# F20

让我们现在使用 `lvdisplay` 验证镜像是否已到位（仅显示 `lvol1` 和 `lvol2`）。

```
# lvdisplay -v /dev/vg00/lvol* | more

--- Logical volumes ---
LV Name                 /dev/vg00/lvol1
VG Name                 /dev/vg00
LV Permission            read/write
LV Status                available/syncd
Mirror copies            1
Consistency Recovery     mwc
Schedule                 parallel
LV Size [Mbytes]         52
Current LE               23
Allocated PE             46
Stripes                  0
Stripe Size [Kbytes]     0
Bad Block                off
Allocation               strict/contiguous

--- Distribution of logical volume ---
PV Name        LE on PV  PE on PV
/dev/dsk/c0t6d0   23     23
/dev/dsk/c1t3d0   23     23

--- Logical extents ---
LE          PV1            PE1   Status
0000 /dev/dsk/c0t6d0   0000 current   /dev/dsk/c1t3d0 0000 current
0001 /dev/dsk/c0t6d0   0001 current   /dev/dsk/c1t3d0 0001 current
0002 /dev/dsk/c0t6d0   0002 current   /dev/dsk/c1t3d0 0002 current
0003 /dev/dsk/c0t6d0   0003 current   /dev/dsk/c1t3d0 0003 current
```

您可以从此列表中看出，`c0t6d0` 在 `c1t3d0` 上进行了镜像。

# F21

重启系统以确认所有更改已生效。

重启后，执行以下操作以创建转储。对于 ^b 起作用，键必须处于“Service”位置（必须位于服务器上的系统控制台才能使其起作用）。

- 使用 ^b 获取 CM> 提示符。
- 在 CM> 提示符下使用 tc 命令创建核心转储。

# F22

系统在核心转储后会自动重启。使用以下命令将核心转储保存到磁带上。即使核心转储位于转储逻辑卷中而不是 /var/adm/crash 目录中，也需要 /var/adm/crash 文件名。

```
# savecore -t /dev/rmt/0m /var/adm/crash
```

# F23

然后使用 `savecore -xt` 和目录名来提取核心转储。如果您没有足够的空间容纳核心转储，或者想要更彻底的检查，您可以致电要求 HP 响应中心验证保存到磁带是否成功。

```
# savecore -xt /dev/rmt/0m /var/adm/crash
```

核心转储的空间需求是从转储的末尾向前计算的。因此，大约 1.5 GBytes 被写入转储逻辑卷，然后大约 600 MBytes 被写入 lvol2。
