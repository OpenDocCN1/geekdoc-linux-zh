
### Physical volumes
```
PV Name      /dev/dsk/c0t1d0
VG Name      /dev/vg00
PV Status    available
Allocatable  yes
VGDA         2
Cur LV       7
PE Size (Mbytes)   4
Total PE     157
Free PE      8
Allocated PE 149
Stale PE     0
```

### Distribution of physical volume
```
LV Name              LE of LV   PE for LV
/dev/vg00/lvol1       12        12
/dev/vg00/lvol2       17        17
/dev/vg00/lvol6       75        75
/dev/vg00/lvol7        9         9
/dev/vg00/lvol4       25        25
/dev/vg00/lvol5        6         6
/dev/vg00/lvol3        5         5
```

### Physical extents
```
PE Status  LV                 LE
0000 current /dev/vg00/lvol1  0000
0001 current /dev/vg00/lvol1  0001
0002 current /dev/vg00/lvol1  0002
0003 current /dev/vg00/lvol1  0003
0004 current /dev/vg00/lvol1  0004
0005 current /dev/vg00/lvol1  0005
0006 current /dev/vg00/lvol1  0006
0007 current /dev/vg00/lvol1  0007
0008 current /dev/vg00/lvol1  0008
0009 current /dev/vg00/lvol1  0009
0010 current /dev/vg00/lvol1  0010
0011 current /dev/vg00/lvol1  0011
0012 current /dev/vg00/lvol2  0000
0013 current /dev/vg00/lvol2  0001
0014 current /dev/vg00/lvol2  0002
0015 current /dev/vg00/lvol2  0003
0016 current /dev/vg00/lvol2  0004
```

## PV 移动

```
0017 current /dev/vg00/lvol2 0005
0018 current /dev/vg00/lvol2 0006
0019 current /dev/vg00/lvol2 0007
0020 current /dev/vg00/lvol2 0008
0021 current /dev/vg00/lvol2 0009
0022 current /dev/vg00/lvol2 0010
0023 current /dev/vg00/lvol2 0011
0024 current /dev/vg00/lvol3 0000
0025 current /dev/vg00/lvol3 0001
0026 current /dev/vg00/lvol3 0002
0027 current /dev/vg00/lvol3 0003
0028 current /dev/vg00/lvol3 0004
0029 current /dev/vg00/lvol4 0000
0030 current /dev/vg00/lvol4 0001
0031 current /dev/vg00/lvol4 0002
0032 current /dev/vg00/lvol4 0003
0033 current /dev/vg00/lvol4 0004
0034 current /dev/vg00/lvol4 0005
0035 current /dev/vg00/lvol4 0006
...
0156 free 0000
```

从该列表中可以看出，`lvol1` 大约为 48 MBytes，其分配的物理扩展区数量远多于大约 20 MBytes 的 `lvol3`。

### pvmove

您可以使用此命令将物理扩展区从一个物理卷移动到其他的物理卷。通过指定源物理卷和一个或多个目标物理卷，您可以使用此命令将数据分散到您希望的各种物理卷中。

#### 卷组命令

- **`vgcfgbackup`**

此命令用于保存卷组的配置信息。请记住，卷组由一个或多个物理卷组成。在您做出 LVM 更改后，SAM 会自动运行此命令。

- **`vgcfgrestore`**

此命令用于恢复卷组的配置信息。

- **`vgchange`**

此命令使卷组处于活动或非活动状态。使用 `-a` 选项，您可以使卷组失活 (`-an`) 或激活 (`-ay`)。

- **`vgcreate`**

您可以使用此命令创建卷组并指定其所有参数。创建卷组时，您需要指定卷组名称以及该卷组的所有相关参数。

- **`vgdisplay`**

如果您使用详细 `-v` 选项，这将显示与卷组相关的所有信息，包括：卷组名称；卷组状态；卷组中的最大、当前和打开的逻辑卷数量；卷组中的最大、当前和活动的物理卷数量；以及物理扩展区相关信息。

以下是使用 `vgdisplay` 查看卷组 `vg00` 的示例：

```
$ vgdisplay /dev/vg00
```

--- 卷组 ---

VG Name            /dev/vg00

VG Write Access    read/write

VG Status          available

Max LV             255

Cur LV             7

Open LV            7

Max PV             16

Cur PV             1

Act PV             1

Max PE per PV      2000

VGDA               2

PE Size (Mbytes)   4

Total PE           157

Alloc PE           149

Free PE            8

Total PVG          0

- **`vgexport`**

此命令将逻辑卷组从系统中移除，但不会修改物理卷上的逻辑卷信息。然后可以使用 `vgimport` 将这些物理卷导入另一个系统。

- **`vgextend`**

可以通过此命令指定要添加到卷组的物理卷，从而将物理卷添加到卷组中。

- **`vgimport`**

此命令可用于将物理卷导入另一个系统。

- **`vgreduce`**

可以通过此命令缩小卷组的大小，方法是指定要从卷组中移除哪个物理卷。在进行此操作之前，请确保要移除的物理卷上没有数据。

- **`vgremove`**

可以使用此命令将卷组定义完全从系统中移除。

- **`vgscan`**

在发生某种灾难的情况下，您可以使用此命令扫描系统，以尝试重建 `/etc/lvmtab` 文件。

- **`vgsync`**

有时，卷组中的镜像数据会变得“陈旧”或过时。`vgsync` 用于同步卷组中每个镜像逻辑卷的物理扩展区。

#### 逻辑卷命令

- **`lvcreate`**

此命令用于创建新的逻辑卷。逻辑卷在卷组内创建。逻辑卷可以跨越多个磁盘，但必须存在于卷组内。当您在 SAM 中创建逻辑卷时，SAM 会为您执行此命令。此命令有许多选项，其中两个常用的选项是 `-L` 用于定义逻辑卷的大小，`-n` 用于定义逻辑卷的名称。

- **`lvchange`**

此命令用于以某种方式更改逻辑卷。例如，您可能希望使用 `-p` 选项将逻辑卷的权限更改为读写 `w` 或只读 `r`。或者，您可能希望将严格策略（在磁盘镜像下描述）更改为严格 `y`、非严格 `n` 或 PVG 严格 `g`。

- **`lvdisplay`**

此命令显示您指定的每个逻辑卷的状态和特征。如果使用该命令的详细 `-v` 选项，您将获得许多类别的大量有用数据，包括：

    - 1) 关于逻辑卷设置方式的信息，例如逻辑扩展区所在的物理卷；物理卷上的本地扩展区数量；以及物理卷上的物理扩展区数量。
    - 2) 逻辑扩展区的详细信息，包括逻辑扩展区编号以及关于逻辑扩展区所在的物理卷和物理扩展区的一些信息。

以下是针对之前 `bdf` 示例中显示的第一个逻辑卷 `vol1` 使用 `lvdisplay` 的示例：
