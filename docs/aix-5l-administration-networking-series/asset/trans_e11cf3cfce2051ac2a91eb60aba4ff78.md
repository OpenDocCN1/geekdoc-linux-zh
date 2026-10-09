

卷已命名。出于报告目的，每个逻辑分区的镜像副本被视为独立的。这种独立性允许您针对热点区域微调镜像。

**lvmstat** 还支持按时间间隔（以秒为单位）进行报告。每个间隔都会生成一份独立的报告。该系列中的第一份报告包含自卷组最近一次变更后收集统计数据以来的信息，而随后的每份报告则包含自上一次报告以来的统计数据。count 参数允许您指定要报告多少个分区（如果使用了 `-l` 标志来指定单个逻辑卷）或要报告多少个逻辑卷（如果使用了 `-v` 标志来指定一个卷组）。如果 count 为 5，则对于逻辑卷（`-l`）将报告最繁忙的五个分区，或者对于卷组（`-v`）将报告最繁忙的五个逻辑卷。例如，要显示 rootvg 卷组中排名前三个的逻辑卷，请使用以下命令：

```
# lvmstat -v rootvg -c 3
Logical Volume   iocnt  Kb_read  Kb_writn  Kbps
hd2              6982   23016    25920     0.01
hd9var           6258    564     24366     0.00
hd4              4536   1960     16412     0.00
```

要显示 hd2 逻辑卷中排名前十分区，请使用以下命令：

```
lvmstat -l hd2 -c 10
Log_part    mirror   iocnt  Kb_read  Kb_writn  Kbps
5           1        1207    652      8084      0.00
1           1        1047    72       1116      0.00
107         1         754    508      2520      0.00
9           1         427    156      2796      0.00
55          1         412    348      1328      0.00
23          1         401    304      1304      0.00
37          1         392    296      1276      0.00
57          1         376    228      1276      0.00
11          1         334     76      1260      0.00
15          1         245    440       552      0.00
```

要连续每五秒显示一次 hd2 逻辑卷的报告，请运行以下命令：

```
# lvmstat -l hd2 5
```

要每五秒显示十份报告，请运行以下命令：

```
# lvmstat -l hd2 5 10
```

要重置 rootvg 卷组的所有统计计数器，请运行以下命令：

```
# lvmstat -v rootvg -C
```

要禁用 rootvg 卷组的统计收集，请使用以下命令：

```
# lvmstat -d rootvg
```

## 迁移物理分区

使用 **lvmstat** 命令的输出，识别热点逻辑分区（LP）非常容易。这些高负载的 LP 会脱颖而出，并列出在报告输出的顶部。如果您有一个磁盘包含多个热点 LP，并且希望将负载在可用磁盘之间进行平衡，您可以使用 **migrate** 命令在磁盘之间移动 LP。

**migrate** 命令使用逻辑分区号（`LPNumber`）、逻辑卷名（`LVName`）、逻辑卷副本号（`CopyNumber`），以及如果 LV 是镜像的，则还使用目标物理卷（`DestPV`）和物理分区号（`PPartNumber`）来控制副本服务的用法。**migrate** 命令的语法如下所列：

```
migrate   LVName/LPNumber[/CopyNumber]  DestPV[/PPartNumber]
```

如果指定了目标 **PPartNumber**，则使用该值；否则，将使用逻辑卷的重新生成策略生成目标 **PPartNumber**。对于镜像 LV，LP 的第一个镜像副本将被移动。如果您想指定要迁移哪个 LP 副本——您肯定需要这样做——您必须使用 1、2 或 3 作为 **migrate** 命令的 **CopyNumber** 参数。以下是一些使用 **migrate** 命令的手册页示例：

1. 要移动逻辑卷 iv00 的第一个逻辑分区到 hdisk1，请键入
    ```
    # migrate lp iv00/1 hdisk1
    ```
2. 要移动逻辑卷 hd2 第三个逻辑分区的第二个镜像副本到 hdisk5，请键入
    ```
    # migrate lp hd2/3/2 hdisk5
    ```
3. 要移动逻辑卷 testlv 第二十五个逻辑分区的第三个镜像副本到 hdisk7 的一百号分区，请键入
    ```
    # migrate lp testlv/25/3 hdisk7/100
    ```

AIX 5L 的这些新功能包含在标准的 **bos.rte.lvm** 文件集中。此 LVM 文件集还包含一些其他可供您研究的新命令：

- 中间级命令，使用热备迁移丢失的磁盘并同步过期分区
  - `/usr/sbin/hotspare`
- 报告 VG 或 LV 的状态
  - `/usr/sbin/lvmstat`
- 允许在磁盘之间重新定位 LP
  - `/usr/sbin/migratelgp`
- 直接从 VGDA 读取数据
  - `/usr/sbin/readvgda`
- 减小分页空间的大小
  - `/usr/sbin/shrinkpg`

AIX 4.3.3 **bos.rte.lvm** 文件中缺失的一个文件集是 **/usr/sbin/updatedlv** 命令。

# 配置卷组

为了让新磁盘可供 LVM 使用，该磁盘必须被指定为物理卷，并被分配一个物理卷标识符（PVID）。在较旧的 AIX 版本中，PVID 是一个 16 位十六进制数，而在 AIX 5L 中是一个 32 位十六进制数。AIX 4.3 和 AIX 5L 都通过 **lspv** 命令仅显示 16 位数字。**lsattr -El hdisk0** 命令将在 AIX 5L 和 AIX 4.3.3（安装维修级别 8 及以上时）显示 32 位 PVID。值得注意的是，所有额外的 16 个字符都是“0”。使用以下命令在新磁盘上创建 PVID：

```
# chdev -l hdisk<n> -a pv=yes
```

您可以使用 **lsdev** 列出系统上的物理磁盘：

```
# lsdev -C -c disk
hdisk0  Available  00-00-05-00  4.2  GB  SCSI  Disk  Drive
hdisk1  Available  00-00-05-10  4.2  GB  SCSI  Disk  Drive
hdisk2  Available  00-00-30  Other  SCSI  Disk  Drive
hdisk3  Available  00-04-00-40  Other  SCSI  Disk  Drive
hdisk4  Available  00-04-00-50  Other  SCSI  Disk  Drive
hdisk5  Available  00-04-00-00  Other  SCSI  Disk  Drive
hdisk6  Available  00-04-00-10  Other  SCSI  Disk  Drive
hdisk7  Available  00-04-20  Other  SCSI  Disk  Drive
```

要列出与这些磁盘相关的 PVID，请使用 **lspv** 命令：

```
# lspv
hdisk0  000008870001c7e1  rootvg
hdisk1  00001508fce5bbee  rootvg
hdisk2  0000406c0c388efc4  vg00
hdisk3  000015082c65e92df  vg00
hdisk4  0000150837cc1a85  vg01
hdisk5  000015082c28f5c7  vg01
hdisk6  000015082c2931f5  vg01
hdisk7  000015082c296d8f  vg01
```

要将新磁盘添加到新卷组或现有卷组中，请使用 **SMIT** 或 `mkvg` 和 `extendvg` 命令（见图 11-4）：

```
# mkvg -f -y vg10 hdisk10 hdisk11  # 使用 hdisk10 和 hdisk11 创建卷组 vg10
# extendvg -f rootvg hdisk8  # 将 hdisk8 添加到 rootvg 卷组

# smit mkvg
```

每个卷组都会分配一个卷组标识符（VGID）。在较旧的 AIX 版本中，VGID 是一个十六位的十六进制数，而在 AIX 5L 中是一个 32 位的十六进制数。系统中的每个 VGID 都由 `/etc/vg` 目录中的一个条目表示。

```
# ls /etc/vg
vg00012560841690B0   vg0001256084A8C772
vg00012560841690B00000000000000000
```

![](img/82f851021955589d82b22750fb3b1646_213_0.png)

要显示系统中现有卷组的配置，请使用 **lsvg** 命令：

```
# lsvg # 列出卷组
rootvg
vg01
vg02
vg03

# lsvg -l rootvg # 列出 rootvg 卷组的内容

rootvg:
LV NAME TYPE LPs PPs PVs LV STATE MOUNT POINT
hd5 boot 2 2 1 closed/syncd N/A
hd6 paging 84 84 1 open/syncd N/A
hd8 jfsLog 1 1 1 open/syncd N/A
hd4 jfs 8 8 1 open/syncd /
hd2 jfs 296 296 2 open/syncd /usr
hd9var jfs 13 13 2 open/syncd /var
hd3 jfs 26 26 1 open/syncd /tmp
hd1 jfs 1 1 1 open/syncd /home
hd10opt jfs 156 156 2 open/syncd /opt
lvcscripts jfs 25 25 1 open/syncd /scripts
lv00 jfs 10 10 1 open/syncd /storix

# lsvg -P rootvg # 列出根卷组中的物理卷

rootvg:
PV_NAME PV STATE TOTAL PPs FREE PPs FREE DISTRIBUTION
hdisk0 active 479 0 .00..0000..00
hdisk1 active 479 336 96...48..00..96..96
```

## 法定人数

卷组中的每个物理卷都标记有卷组描述符区域（VGDA）和卷组状态区域（VGBA）。VGDA 和 VGBA 是卷组中最重要的组件！VGDA 包含组成卷组的所有逻辑卷、物理卷和分区的标识符。VGBA 是一个位图，用于指示磁盘上哪些物理分区是过期的，需要同步更新。

当使用 **varyonvg** 命令或 SMIT 激活卷组时，LVM 在联机之前会验证它是否能访问至少 51% 的 VGDA 和 VGBA 副本。这种多数称为 *法定人数*（quorum），是 LVM 为确保数据完整性所必需的。任何不可用的物理卷都会被报告。系统管理员必须决定是否在设备不可访问时继续操作。如果法定多数是

