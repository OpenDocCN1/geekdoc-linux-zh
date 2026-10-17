
## 重配置某些磁盘 - 使用逻辑卷命令的示例

### F19

让我们使用 `lvextend` 为 `vg00` 中的所有卷扩展一个镜像：

```
# lvextend -m 1 /dev/vg00/lvol1 /dev/dsk/clt3d0
```

新分配的镜像现在正在同步中。

此操作将需要一些时间。请稍候 ...

逻辑卷 "`dev/vg00/lvol1`" 已成功扩展。

`/dev/vg00` 的卷组配置已保存到 `/etc/lvmconf/vg00.conf`

进入 `/tmp/mirror` 并运行。`lvol1` 之前已经扩展过了；

```
# lvextend -m 1 /dev/vg00/lvol3 /dev/dsk/clt3d0
lvextend -m 1 /dev/vg00/lvol4 /dev/dsk/clt4d0
lvextend -m 1 /dev/vg00/lvol5 /dev/dsk/clt5d0
lvextend -m 1 /dev/vg00/lvol6 /dev/dsk/clt6d0
lvextend -m 1 /dev/vg00/lvol7 /dev/dsk/clt7d0
```

新分配的镜像现在正在同步中。
此操作将需要一些时间。
请稍候 .... 逻辑卷 "`dev/vg00/lvol2`" 已成功扩展。
`/dev/vg00` 的卷组配置已保存到 `/etc/lvmconf/vg00`.

### F20

现在让我们用 `lvsdisplay` 验证镜像是否已就绪（仅 `lvol1` 和 `lvol2`）：

```
# lvsdisplay -v /dev/vg00/lvol* | more
Logical volumes

LV Name                 /dev/vg00/lvol1

VG Name                 /dev/vg00

Permission              read/write

Status                  available/synced

Mirror copies           1

Consistency Recovery  MWC

Schedule                parallel

LV Size (Bytes)         92

Current LE              23

Allocated PE            46

Used PE                 0

Stripes Size (Kbytes)   0

Bad block               off

Allocation              strict/contiguous

-- Distribution of logical volume --

PV Name                  LE on PV  PE on PV

/dev/dsk/clt6d0         23        23

/dev/dsk/clt3d0         * 23        23
```

```
--- Logical extents ---

LE              PE1 Status 1 PV2      PE2 Status 2

0000dev/disk/c0t6d0 0000 current /dev/disk/clt3d0 0000 current

0001 /dev/disk/c0t6d0 0001 current /dev/disk/clt3d0 0001 current

0002 /dev/disk/c0t6d0 0002 current /dev/disk/clt3d0 0002 current

0003 /dev/disk/c0t6d0 0003 current /dev/disk/clt3d0 0003 current
```

你可以从此列表中看到 `c0t6d0` 已经镜像化到 `c1t3d0` 上。

## 216 第 2 章 HP-UX 文件系统及相关命令

### F21

重启系统以确认所有更改已生效。重启后，执行以下操作以创建转储（dump）。按键必须处于“Service”位置 `^b` 才能生效（你必须在服务器上操作才能生效）。

使用 `^b` 进入 `CM>` 提示符。

在 `CM>` 提示符下使用 `te` 命令创建核心转储（core dump）。

### F22

系统会在核心转储后自动重启。使用以下命令将核心转储保存到带上。尽管核心转储在 `dump` 逻辑卷而不是 `/var/adm/crash` 目录下，但仍需要 `/var/adm/crash` 文件名。

```
# savecore -t /dev/rmt/0m /var/adm/crash
```
