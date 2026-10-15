
# vgdisplay -v vgu01

```text
Using volume group(s) on command line
Finding volume group "vgu01"
--- Volume group ---
VG Name               vgu01
System ID
Format                lvm2
Metadata Areas        3
Metadata Sequence No  4
VG Access             read/write
VG Status             resizable
MAX LV                255
Cur LV                1
Open LV               1
Max PV                255
Cur PV                3
Act PV                3
VG Size               5.78 GB
PE Size               4.00 MB
Total PE              1479
Alloc PE / Size       1460 / 5.70 GB
Free PE / Size         19 / 76.00 MB
VG UUID               OUTQJr-Y88K-jKSc-HpE5-720h-4LZs-3pFC8e

Annotations:
the number of meta-data areas
all PVs have meta-data area by default
If in "Exported", "exported/resizable" is displayed.
In this case, it is in "Imported".
num of Open LV
UUID of the VG
(it is recorded in meta-data area of PVs)
```

### 图 6-14 vgdisplay -v（续）

```text
: (continued)
--- Logical volume
LV Name            /dev/vgu01/lvu01
VG Name            vgu01
LV UUID            REW0TH-erkC-Z3P5-yzFb-1a0W-HTLy-c0aMPR
LV Write Access    read/write
LV Status          available
######## open               2
LV Size            5.70 GB
Current LE         1460
Segments            3
Allocation         inherit
Read ahead sectors  0
Block device       253:8
--- Physical volumes
PV Name            /dev/dasd0
PV UUID            5pXoDK-9M1Z-zH4i-iyM0-Jny6-YTCW-8Gz1K0
PV Status          allocatable
Total PE / Free PE 307 / 0
```

VG 中的 LV

LV 的 UUID

（记录在 PV 的元数据区域中）

如果 vg id 已停用，则显示 "NOT available"。

打开该 LV 的进程数量。如果它不为 "0"，则无法停用该 LV。

LV 的设备号（major:minor）

这些具有相同的 major:minor 号。

- `/dev/mapper/vgu01-lvu01`
- `/dev/dm-8`
- `/dev/vgu01/lvu01`

组成 VG 的 PV。

PV 的 UUID

（记录在 PV 的元数据区域中）

使用 `vgscan` 命令，所有扫描到的设备都存储在 `/etc/lvm/.cache` 文件中。目标设备文件名由 `lvm.conf` 中的 `filter` 参数定义。

### 图 6-15 lvm.conf 文件

```text
persistent_filter_cache {
    valid_devices=[
        "/dev/dm-6",
        "/dev/dasdc",
        "/dev/dasdb1",
        "/dev/dasdcl",
        "/dev/dasda1",
        "/dev/dm-5",
        "/dev/mapper/lu5601p1",
        :
        :
    ]
}
```

`vgscan` 命令对 LVM 的识别顺序如下：PVs → VGs → LVs。

除非识别出组成 VG 的所有 PV，否则该 VG 不可用。首先需要在启动时的 `vgscan` 中识别 PV。PV 需要在 initrd 或 `zipl.conf` 中识别。

可以使用 `pvdisplay` 命令来显示已识别的 PV。

如果 PV 已被识别但 VG 未被识别，PV 中的元数据区域可能已损坏。

如果 PV 未被识别（未通过 `pvdisplay` 列出），请检查以下内容：

- 在 `lvm.conf` 中：
  - `filter` 参数
  - `types` 参数
- 检查 `/etc/lvm/.cache` 以验证目标设备文件名。

#### 6.1.5 I/O 统计

关于存储设备的另一个信息来源是 DASD I/O 统计数据。通过 I/O 统计数据，可以收集并存储所有关于存储设备的重要信息到一个文件中，以便进一步分析。您可以根据需要开启或关闭 DASD I/O 统计数据。图 6-16 展示了如何开启和关闭 DASD I/O 统计数据。

![](img/f332344337ca8bf6846cb313a66ee0b3_238_0.png)

图 6-16 开启/关闭 DASD I/O 统计数据

若要重置收集过程，请将 DASD I/O 统计数据关闭后再重新开启。

有关 DASD I/O 统计数据的更多信息，另请参阅第 68 页的 3.1.8 节“netstat”。

##### 6.2 案例研究

在本节中，我们将通过一个涉及实际问题的案例研究进行探讨。在这个案例研究中，我们讨论了一种场景，其中交换速率过高，导致系统吞吐量大幅下降。

我们有一个运行 DB2 数据库的 Linux 客户机系统。由于 DB2 请求的增加，Linux 系统的工作负载也随之增加。我们使用了 z/VM 工具和 Linux 基本工具来监控这种情况。在性能工具包窗口 FCX100 的第一页（图 6-17）中，系统的负载和分页活动均正常。
