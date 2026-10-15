
如图所示并由上述输出确认的，这是一个 `HSZ WWID`，是一个长度为 60 字节的 ASCII `WWID`。注意 `WWID` 中的 `"ZG81110558ZG811107225"` 部分是两个 `HSZ` 控制器的序列号拼接在一起。让我们看看是否可以验证这一事实。在 `HSZ` 的控制台上执行 `"show this"`。输出将显示每个 `HSZ` 控制器的序列号。

```
HSZ70> show this

Controller:

HSZ70 ZG81110558 Firmware V77Z-0, Hardware H01

Configured for dual-redundancy with ZG81110725

In dual-redundant configuration
```

`"this"` 控制器的序列号是 `"ZG81110558"`，而 `"other"` 控制器的序列号是 `"ZG81110725"`。

### 7.3 硬件管理

重要：

我们讨论的许多功能将取决于硬件管理子系统。该子系统用于配置、监控和管理集群中的硬件。

以下功能属于硬件管理子系统：

- 设备配置
- 健康监控
- 错误报告
- 固件更新

硬件管理子系统提供了与硬件交互的一致接口，无论供应商是哪。这种抽象对于管理大型异构环境至关重要。

“`ldb`”文件包含了其他硬件组件（适配器、`CPU`、键盘、鼠标等）的信息，以及一些存储设备信息（`user_name`、`phys_location` 等）。组件信息可以参考下面的示例：

```
# hmwgr -show

HWID: HOSTNAME        SERVICE COMPONENT NAME

1: sheridan      none        COMPAQ AlphaStation XP900 466 MHz

2: sheridan      r--- none    CPU

3: sheridan      r-d--- none    scp

4: sheridan      r-d--- none    kevm

5: sheridan      r--- none    pc10

53: sheridan      -cds- iomap  SCSI-WWID:0c000000:00e1-0011-9fbe

54: sheridan      -cds- iomap  SCSI-WWID:0c000000:00e1-0011-9492

55: sheridan      -cds- iomap  SCSI-WWID:0c000000:00e1-0018-ba75

56: sheridan      -cds- iomap  SCSI-WWID:0c000000:00e1-0018-9f1f

57: sheridan      -cd-- iomap  SCSI-WWID:0c000000:00e1-0018-9f33

58: sheridan      -cd-- iomap  SCSI-WWID:0c000000:00e1-0018-9f1a
```

- `dec_scsi_db`

该文件由 `SCSI/CAM` 子系统所有，用于存储 `WWID` 并跟踪系统已知的 `SCSI` 设备。该二进制文件也被 `hmwgr` 命令使用。
例如：

```
# hmwgr -show

HWID: DEVICEID HOSTNAME    TYPE    DEVICE SUBTYPE DRIVER NUM PATH FILE FIRST VALID PATH

0: 0         sheridan    cdrom   none    0       1       (null)

40: 1        sheridan    disk    none    2       1       [2/0/0]

41: 2         sheridan    disk    none    2       1       [2/1/0]

45: 3         sheridan    cdrom   none    0       1       [3/0/0]

53: 4         sheridan    disk    none    0       1       [3/0/0]

54: 5         sheridan    disk    none    0       1       [3/1/0]

55: 6         sheridan    disk    none    0       1       [3/2/0]

56: 7         sheridan    disk    none    0       1       [3/3/0]

57: 8         sheridan    disk    none    0       1       [3/4/0]

58: 9         sheridan    disk    none    0       1       [3/5/0]
```

- `dec_unic_db`

此数据库包含唯一 `ID`。根据《Tru64 UNIX 系统管理指南》，“此数据库存储了分配给硬件组件的上一个最高硬件标识符 (`HWID`)。此数据库用于生成分配给新安装硬件组件的下一个 `HWID`。”文件中还包含其他信息，如 `strings (1)` 命令的输出所示，这表明该文件用于 `HWID` 以外的唯一 `ID`，尽管这可能是最常见的功能。

```
# strings /etc/dec_unid_db

DEC_UNID

hardware

dsf_group_id

cluster_minor

control_port_id
```

- `dfsc.dat` 和 `dfsl.dat`

设备文件状态文件是由 `dsfmgr` 命令维护的 `ASCII` 文件。`dfsl.dat` 文件用于本地（或成员特定）设备特殊状态以及旧的设备特殊名称。`dfsc.dat` 文件包含通用（或集群范围内的）设备特殊状态。它们被分为三个部分：

#### 1. 实例 (Instance)

实例记录包含三个字段：

- 类型 (`Type`)
- 基名称 (`Base Name`)
- 实例 (`Instance`)

例如（请原谅这个双关）：

```
"I: dsk 8"
```

#### 2. 版本 (Version)

该记录看起来像注释，但它包含了文件格式的版本以及主机名和操作系统版本。

```
# 1.0 sheridan V5.1 (Rev. 732) Tue Mar 20 01:23:34 2001"
```
