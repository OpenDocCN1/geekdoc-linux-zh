
```
$ /usr/sbin/ioscan -func disk

| 类 | H/W 路径 | 驱动 | S/W 状态 | H/W 类型 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| disk | 2 | 10/0/5.0 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c05d0 |
| disk | 3 | 10/0/6.0 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c06d0 |
| disk | 6 | 10/4/4.0 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c14d0 |
| disk | 7 | 10/4/4.5 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c15d0 |
| disk | 8 | 10/4/6.0 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c16d0 |
| disk | 9 | 10/4/12.0 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c24d0 |
| disk | 10 | 10/4/12.5 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c25d0 |
| disk | 11 | 10/4/12.6 | sdisk | CLAIMED | SEAGATE ST150W | /dev/dsk/c26d0 |
| disk | 5 | 10/12/5.0 | sdisk | CLAIMED | TOSHIBA CD-ROM XM-540 | /dev/dsk/c32d0 |
```

注意此配置中的磁盘对应图 2-4 部的磁盘。我们尚未查看与这些磁盘相关的逻辑卷信息，只有它们的物理地址。

`F2` 运行显示 查看卷。`vg0` `lvol2` 是我们要移动到独立 2 GByte 磁盘的逻辑卷。我们还不知道 `vg0` `lvol1-7` 是否都已镜像。

# 重配置某些磁盘 - 使用某些逻辑卷命令的示例 201

```
# vgdisplay -v

-- 卷组 --

VG 名称            /dev/vg00

VG 写入访问    read/write available

VG 状态           255

Max LV              7

Cur LV               0

Open LV             7

Max PV              16

Cur PV               2

Act PV 2

Max PE per PV 1023

VGDA 4

PE Size (Mbytes) 4

Total PE 2046

Alloc PE 688

Free PE 1358

Total PV 0

--- 逻辑卷 ---

LV 名称 /dev/vg00/lv1

LV Status available/sync

LV Size (Mbytes) 92

Current LE 23

Allocated PE 46

Used PV 2

LV 名称 /dev/vg00/lv2

LV Status available/sync

LV Size (Mbytes) 500

Current LE 125

Allocated PE 250

Used PV 2

LV 名称 /dev/vg00/lv3

LV Status available/sync

LV Size (Mbytes) 20

Current LE 5

Allocated PE 10

Used PV 2

LV 名称 /dev/vg00/lv4

LV Status available/sync

LV Size (Mbytes) 252

Current LE 63

Allocated PE 126
Used PV 2

LV 名称 /dev/vg00/lv5

LV Status available/sync

LV Size (Mbytes) 32

Current LE 8

Allocated PE 16
Used PV 2

LV 名称 /dev/vg00/lv6

LV Status available/sync

LV Size (Mbytes) 320

Current LE 80

Allocated PE 160
Used PV 2

LV 名称 /dev/vg00/lv7

LV Status available/sync

LV Size (Mbytes) 160

Current LE 40

Allocated PE 80
Used PV 2
```
