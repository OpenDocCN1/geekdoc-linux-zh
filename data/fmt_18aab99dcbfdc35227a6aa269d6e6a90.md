
```
# hwmgr -show name

HWID: NAME      HOSTNAME    PERSIST TYPE    PERSIST AT
------------------------------------------------------------
33: ata0     sheridan    BUS             pci0 slot 13
49: isp0     sheridan    BUS             pci0 slot 15
44: ltp sa1   sheridan    BUS             pci0 slot 14
36: isp a0    sheridan    BUS             pci0 slot 15
51: mchan0    sheridan    CONTROLLER      pci0 slot 16
5: pci0      sheridan    BUS             nexus
50: scsi3     sheridan    CONTROLLER      isp0 slot 0
37: scsi2     sheridan    CONTROLLER      itpsa0 slot 0
35: scsi1     sheridan    CONTROLLER      ata0 slot 1
34: scsi0     sheridan    CONTROLLER      ata0 slot 0
32: tul       sheridan    CONTROLLER      pci0 slot 11
31: tu0       sheridan    CONTROLLER      pci0 slot 9
```

### `dec_hwc_cdb` and `dec_hwc_ldb`

这些是硬件组件数据库文件。`ldb` 文件是此系统的本地（或成员特定）数据库文件，而 `cdb` 文件是通用（或集群范围）数据库文件。这些数据库包含系统所有已注册硬件组件的信息。

`cdb` 文件包含存储设备及其部分信息，如 WWID。可以通过键入以下命令进行验证：`strings /etc/dec_hwc_cdb`。

`ldb` 文件包含其他硬件组件（适配器、cpu、键盘、鼠标等）以及部分存储设备信息（`user_name`, `phys_location` 等）。组件信息可在以下示例中看到：

```
# hwmgr -show component

HWID:  HOSTNAME  FLAGS SERVICE COMPONENT NAME
----- ---------- ----- ------- ----------------
  1:  sheridan   r---  none    CPU0 AlphaStation XP900 466 MHz
  2:  sheridan   r---  none    CPU0
  4:  sheridan   r-d-  none    scp
  5:  sheridan   r-d-  none    kenv
  6:  sheridan   r-d-  none    pci0

 53:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0019-9fbe
 54:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0019-9492
 55:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0018-ba75
 57:  sheridan   -cds  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f1f
 58:  sheridan   -cd-  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f33
 59:  sheridan   -cd-  iomap   SCSI-WWID:0c000008:0000-0e11-0018-9f1a
```

### `dec_scsi_db`

此文件由 SCSI/CAM 子系统拥有，用于存储 WWID 并跟踪系统已知的 SCSI 设备。此二进制数据文件也由 `hwmgr` 命令使用。例如：

```
# hwmgr -show scsi

             SCSI              DEVICE    DEVICE  DRIVER  NUM  DEVICE FIRST
HWID:       DEVID   HOSTNAME    TYPE     SUBTYPE  OWNER  PATH  FILE   VALID PATH
-----       -----   --------    -------  -------  ------ ----  -----  ----------
   0:          0    sheridan    cdrom    none       0     1   (null)
  40:          1    sheridan    disk     none       2     1   dsk0   [2/0/0]
  41:          2    sheridan    disk     none       2     1   dsk1   [2/1/0]
  45:          3    sheridan    cdrom    none       0     1   cdrom0 [0/0/0]
  53:          4    sheridan    disk     none       0     1   dsk2   [3/0/0]
  54:          5    sheridan    disk     none       0     1   dsk3   [3/1/0]
  55:          6    sheridan    disk     none       0     1   dsk4   [3/2/0]
  56:          7    sheridan    disk     none       0     1   dsk5   [3/3/0]
  57:          8    sheridan    disk     none       0     1   dsk6   [3/4/0]
  58:          9    sheridan    disk     none       0     1   dsk7   [3/5/0]
```

### `dec_unid_db`

此数据库包含唯一 ID。根据 Tru64 UNIX 系统管理指南，“这是一个二进制数据库，存储分配给硬件组件的前一个最高硬件标识符（HWID）。此数据库用于生成分配给新-已安装的硬件组件。”文件中还包含其他信息，如使用 `strings(1)` 命令的输出所示，该输出表明该文件除了 HWID 之外还用于唯一 ID，尽管这可能是其最常见的功能。

```
# strings /etc/dec_unia_db
DEC_UNID
hardware
dfs_group_id
cluster_minor
control_port_id
```

### `dfsc.dat` 和 `dfsl.dat`

设备文件状态数据文件是由 `dsfmgr` 命令维护的 ASCII 文件。`dfsl.dat` 文件用于记录本地（或成员特定）设备特殊文件的状态以及旧的设备特殊文件名。`dfsc.dat` 文件包含公共（或集群范围）设备特殊文件的状态。这些文件分为三个部分：

1. **实例**

实例记录包含三个字段：

- 类型
- 基名
- 实例

例如（请原谅这个双关语）：

```
"I: dsk 8"
```

2. **版本**

该记录看起来像注释，但其中包含文件格式版本以及主机名和操作系统版本。

```
"# 1.0    sheridan V5.1 (Rev. 732)  Tue Mar 20 01:23:34 2001"
```

3. **状态**

状态记录当前包含 12 个字段：

- 状态（A、C 或 d）
- 集群设备主/次编号
- 基名 ID
- 设备类型
- （块或字符）
- 设备路径
- 设备实例
- 本地设备主/次编号
- 硬件 ID
- 设备节点 ID
- 旧节点名称
- 设备前缀
- 设备后缀

以下是一些示例：

第一个示例来自 `/etc/dfsc.dat`，显示了集群设备的“A”（活动）状态。

```
A:       0 1300041      45       10       0  b  ""       /dev/disk/ cdrom 0 a
```

第二个示例同样来自 `/etc/dfsc.dat`，显示了集群设备的“d”（已停用）状态。
