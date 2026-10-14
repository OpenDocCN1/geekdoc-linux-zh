

## dccd.dat

dccd.dat 文件是 dsfmgr 用于创建设备特殊文件的 Category to Class-Directory, Prefix Database。这是一个 ASCII 文件，但不应被修改。文件中包含以下信息：

- 设备类别。
- 设备名称。
- 设备类型（block, character, rewind, norewind, sgeneric, storage, *）。
- 设备特殊文件所在的子目录。
- 设备特殊文件类型（block 或 character）。
- 文件模式权限位（八进制）。
- 设备前缀。
- 实例宽度（例如，cdrom 设备在实例字段中始终至少有一位数字：cdrom0）。

请注意 kevm 设备实例宽度为零且设备名称仅为 kevm，而实例宽度为二的硬连线终端将命名为 tty00。

```
# more /etc/dccd.dat
disk    cdrom    block    disk    b 600 cdrom 1
disk    cdrom    char    rdisk    c 600 cdrom 1
..    pseudo    kevm    *    .    c 600 kevm 0
..    terminal    hardwired    *    .    c 666 tty 2
```

## dcdd.dat

dcdd.dat 文件是 Device Class Directory Default Database。它被 dsfmgr 命令用于创建设备目录。这是一个 ASCII 文件，不应被修改。该文件包含目录位置（local - /dev，或 cluster - /devices）、目录模式权限位（八进制）以及目录名称。

```
# cat /etc/dcdd.dat
l 0755 .
l 0755 none
c 0755 cport
c 0755 disk
c 0755 rdisk
c 0755 tape
c 0755 ntape
c 0755 changer
c 0755 dmapi
```

- ddr.db

Dynamic Device Recognition（DDR）数据库用于描述 SCSI CAM（common access method）设备参数和特性，以便动态创建设备。这是一个数据文件，由 ddr_config(8) 使用 ddr.dbase 文件作为输入创建。有关更多信息，请参阅 ddr.dbase(4) 参考页。

- dec_devsw_db

这是指主设备开关表数据库文件。它包含设备驱动程序主编号和设备开关条目。这是一个二进制数据文件，由内核维护，但可使用 devswmgr(8) 程序查看。

- dec_hw_db

此二进制文件保存系统的硬件拓扑结构。该文件包含总线和控制器的硬件持久性信息。该文件由内核驱动程序框架维护，可通过 hwmgr 命令使用 "name" 子系统进行修改和查询。例如：

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

- dec_hwc_cdb and dec_hwc_ldb

这些是硬件组件数据库文件。"ldb" 文件是此系统的本地（或成员特定）数据库文件，而 "cdb" 文件是通用（或集群范围）数据库文件。这些数据库包含系统所有已注册硬件组件的信息。

"cdb" 文件包含存储设备及其部分信息，如 WWID。可以通过键入以下命令进行验证："strings /etc/dec_hwc_cdb"。

"ldb" 文件包含其他硬件组件（适配器、cpu、键盘、鼠标等）以及部分存储设备信息（user_name, phys_location 等）。组件信息可在以下示例中看到：

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

- dec_scsi_db

此文件由 SCSI/CAM 子系统拥有，用于存储 WWID 并跟踪系统已知的 SCSI 设备。此二进制数据文件也由 hwmgr 命令使用。例如：

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

- dec_unid_db

此数据库包含唯一 ID。根据 Tru64 UNIX 系统管理指南，“这是一个二进制数据库，存储分配给硬件组件的前一个最高硬件标识符（HWID）。此数据库用于生成分配给新-

