

## 图 6-4 带有 -x 选项的 dasdview 命令

```text
# dasdview -x /dev/dasda
:
--- extended DASD information ----------------
real device number : hex 5 dec 5
subchannel identifier : hex b dec 11
CU type (SenseID) : hex 3990 dec 14736
CU model (SenseID) : hex e9 dec 233
device type (SenseID) : hex 3390 dec 13200
device model (SenseID) : hex a dec 10
open count : hex 3 dec 3
:
:
```

使用 `fdasd` 命令，你可以查看 DASD 的分区表。图 6-5 展示了一个示例。

## 图 6-5 fdasd 命令

```text
# fdasd -p /dev/dasda
:
---------------------------------------- tracks ----------------------------------------
Device    start    end    length    Id    System
/dev/dasda1     2    2744     2743     1 Linux native
/dev/dasda2   2745   50084    47340     2 Linux native
exiting...
```

请注意设备节点（`/dev/dasda1` 和 `/dev/dasda2`）的存在。它们是由 udev / 动态设备管理创建的。

### 6.1.2 如何检查 FCP/SCSI 设备

如果你的 Linux 系统使用 SCSI 设备，可以使用 `lsscsi` 来检查这些设备的状态。此命令从 sysfs 读取状态并显示所有在线的 SCSI 设备。

## 图 6-6 位于第 216 页，展示了 lsscsi 命令输出的示例及说明。

![](img/f332344337ca8bf6846cb313a66ee0b3_231_0.png)

## 图 6-6 lsscsi 命令

如果 `lsscsi` 未显示目标地址，你可能需要根据磁盘上线的方式检查以下内容：

- 使用 initrd
  - a. 修改 initrd 后，运行 `zipl`。
  - b. 检查 initrd 中的 `linuxrc` 脚本（以验证步骤）。
- coldplug（冷插）
  - 检查 `/etc/sysconfig/hardware/hwcfg-*`，特别是 WWPN 和 LUN ID。

检查目标 LUN 是否已映射。使用 `san_disc` 进行验证：

- SAN 交换机区域划分
- LUN 映射
- 线缆连接

### 6.1.3 需要检查的 FCP/SCSI 设备事项（续）

使用命令 `lszfcp` 可以获得有关在线的 zfcp 适配器、端口和单元更多信息。图 6-7 展示了一个 `lszfcp` 命令的示例。

## 图 6-7 lszfcp 命令

```text
# lszfcp -H -D -P
0.0.0        3ec4 host0
0.0.3fc4     host1
0.0.3ec4/0x50050763003008455 rport-0:0-0
0.0.3fc4/0x500507630030c455 rport-1:0-0
0.0.3ec4/0x50050763003008455/0x4050142010000000 0:0:0:0
0.0.3ec4/0x50050763003008455/0x4050402220000000 0:0:0:1
0.0.3fc4/0x500507630030c455/0x4050402220000000 1:0:0:0
0.0.3fc4/0x500507630030c455/0x4051402100000000 1:0:0:1

-H : list information about HBA
-P : list information about ports
-D : list information about units
```

使用 SAN 发现工具和命令 `san_disc`，你可以显示有关 SAN 的信息，例如存储端口上的全球端口名称（wwpn）和逻辑单元标识符（lunid）。

此功能仅在 SLES9 SP3 和 SLES10 上可用。你需要加载 `zfcp_haapi` 模块。有关 `san_disc` 命令的示例见图 6-8。

## 图 6-8 san_disc 命令

```text
# san_disc -o HBA_LIST
Number of Adapters: 2
No. Port WWN                Node WWN               SerialNumber     Busid
1   0x50050764012203b3    0x5005076400c4e2d4    IBM5100000004E240  0.0.38c6
2   0x50050764012203b3    0x5005076400c4e2d4    IBM5100000004E240  0.0.39c6

# san_disc -o PORT_LIST -a 1
No. Port WWN                Node WWN               DID        Type
1   0x50050764012203b3    0x5005076300c0d09     0x0300a0   N_Port
2   0x5005076300c1ad9     0x5005076300c0d09     0x0300a0   N_Port
3   0x50050764012203b3    0x5005076400c4e2d4    0x0300a0   N_Port

# san_disc -o REPORT_LUNS -a 1 -p 0x500507630c1ad9
Number of LUNs: 4
No. LUN
1   0x6200000000000000
2   0x6201000000000000
3   0x6202000000000000
4   0x6203000000000000
```

### 6.1.4 需要检查的多路径事项

命令 `multipath -ll` 读取 sysfs 并显示多路径设备（图 6-9）。

## 图 6-9 multipath -ll 命令

```text
# multipath -ll
lu5600 (1IBM_2105.60028721)
[size=953 MB][features="1 queue_if_no_path"][hwhandler="0"]
|-round-robin 0 [prio=2][enabled]
|- 0:0:1:0 sda 8:0 [active][ready]
|- 1:0:1:0 sdb 8:16 [active][ready]
```

`/etc/init.d/multipathd status` 用于检查 `multipathd` 的状态（图 6-10）。

## 图 6-10 /etc/init.d/multipathd

```text
# /etc/init.d/multipathd status
Checking for multipathd: running
```

路径检查器的日志存储在 `/var/log/messages` 中（图 6-11）。

## 图 6-11 路径检查器

```text
Jun 12 15:24:28 xxxxx multipathd: lu5600: event checker started
Jun 12 15:24:28 xxxxx multipathd: path checkers start up
```

如果目标磁盘在 `multipath -ll` 中显示，则必须在 initrd 中将磁盘变为在线状态，以便在启动时进行多路径操作。

如果启动后可以使用 `multipath` 命令配置多路径，则磁盘可能通过 coldplug 上线：

1. 检查 initrd 中的 `linuxrc` 脚本。
2. 修改 initrd 后，运行 `zipl`。

验证 `multipath.conf`。`devnode_blacklist` 是一个用于过滤多路径目标设备的参数。如果 `alias` 无效，则使用 `wwid` 作为设备名称。

配置多路径时，会创建名为 `alias` 的文件：

- `/dev/mapper/`
- `/dev/disk/by-name/`

检查 `boot.multipath` 中的分区表：

- 配置多路径。
- 读取分区表。
- 创建 `dev/mapper/aliaspN`（N 为分区号）。

有关 `/dev/mapper` 的示例见图 6-12。

## 图 6-12 /dev/mapper

```text
# ls -l /dev/mapper/
total 118
drwxr-xr-x  2 root root    408 May  1 10:55 .
drwxr-xr-x 23 root root 121088 May  1 10:55 ..
crw-------  1 root root    10, 63 May  1 10:54 control
brw-------  1 root root   253,  1 May  1 10:54 lu5201
brw-------  1 root root   253,  3 May  1 10:54 lu5201p1
brw-------  1 root root   253,  2 May  1 10:54 lu5202
brw-------  1 root root   253,  4 May  1 10:54 lu5202p1
brw-------  1 root root   253,  5 May  1 10:55 vgA-lvA
brw-------  1 root root   253,  6 May  1 10:55 vgB-lvB
brw-------  1 root root   253,  0 Jan 25 21:39 vgroot-lvroot
```

### 6.1.5 需要检查的 LVM 事项

当你在 Linux 系统中使用 LVM 时，如果 LVM 内部出现问题，这里有一些你应该检查的事项。

#### 检查 LVM 识别

使用命令 `vgdisplay -v` 可以获得有关 LVM 卷组的有用信息。`vgdisplay -v` 命令的示例见图 6-13，并继续在第 221 页的图 6-14。

## 图 6-13 vgdisplay -v

```text
# vgdisplay -v vgu01
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

## 图 6-14 vgdisplay -v（续）

```text
: (continued)
--- Logical volume
LV Name            /dev/vgu01/lvu01
VG Name            vgu01
LV UUID            REW0TH-erkC-Z3P5-yzFb-1a0W-HTLy-c0aMPR
LV Write Access    read/write
LV Status          available
# open               2
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

使用 `vgscan` 命令，所有扫描到的设备都存储在 `/etc/lvm/.cache` 文件中。目标设备文件名由 `lvm.conf` 中的 filter 参数定义。

## 图 6-15 lvm.conf 文件

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
  - filter 参数
  - types 参数
- 检查 `/etc/lvm/.cache` 以验证目标设备文件名。

