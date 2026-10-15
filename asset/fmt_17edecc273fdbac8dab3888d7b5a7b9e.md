
如果指定了目标 `PPartNumber`，则使用该值；否则，将使用逻辑卷的重新生成策略生成目标 `PPartNumber`。对于镜像 `LV`，`LP` 的第一个镜像副本将被移动。如果您想指定要迁移哪个 `LP` 副本——您肯定需要这样做——您必须使用 `1`、`2` 或 `3` 作为 `migrate` 命令的 `CopyNumber` 参数。以下是一些使用 `migrate` 命令的手册页示例：

1. 要移动逻辑卷 `iv00` 的第一个逻辑分区到 `hdisk1`，请键入

   ```
   # migrate lp iv00/1 hdisk1
   ```

2. 要移动逻辑卷 `hd2` 第三个逻辑分区的第二个镜像副本到 `hdisk5`，请键入

   ```
   # migrate lp hd2/3/2 hdisk5
   ```

3. 要移动逻辑卷 `testlv` 第二十五个逻辑分区的第三个镜像副本到 `hdisk7` 的一百号分区，请键入

   ```
   # migrate lp testlv/25/3 hdisk7/100
   ```

`AIX 5L` 的这些新功能包含在标准的 `bos.rte.lvm` 文件集中。此 `LVM` 文件集还包含一些其他可供您研究的新命令：

- 中间级命令，使用热备迁移丢失的磁盘并同步过期分区
  - `/usr/sbin/hotspare`
- 报告 `VG` 或 `LV` 的状态
  - `/usr/sbin/lvmstat`
- 允许在磁盘之间重新定位 `LP`
  - `/usr/sbin/migratelgp`
- 直接从 `VGDA` 读取数据
  - `/usr/sbin/readvgda`
- 减小分页空间的大小
  - `/usr/sbin/shrinkpg`

`AIX 4.3.3` `bos.rte.lvm` 文件中缺失的一个文件集是 `/usr/sbin/updatedlv` 命令。

# 配置卷组

为了让新磁盘可供 `LVM` 使用，该磁盘必须被指定为物理卷，并被分配一个物理卷标识符（`PVID`）。在较旧的 `AIX` 版本中，`PVID` 是一个 `16` 位十六进制数，而在 `AIX 5L` 中是一个 `32` 位十六进制数。`AIX 4.3` 和 `AIX 5L` 都通过 `lspv` 命令仅显示 `16` 位数字。`lsattr -El hdisk0` 命令将在 `AIX 5L` 和 `AIX 4.3.3`（安装维修级别 `8` 及以上时）显示 `32` 位 `PVID`。值得注意的是，所有额外的 `16` 个字符都是“`0`”。使用以下命令在新磁盘上创建 `PVID`：

```
# chdev -l hdisk<n> -a pv=yes
```

您可以使用 `lsdev` 列出系统上的物理磁盘：

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

要列出与这些磁盘相关的 `PVID`，请使用 `lspv` 命令：

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

要将新磁盘添加到新卷组或现有卷组中，请使用 `SMIT` 或 `mkvg` 和 `extendvg` 命令（见图 `11-4`）：

```
# mkvg -f -y vg10 hdisk10 hdisk11  # 使用 hdisk10 和 hdisk11 创建卷组 vg10
# extendvg -f rootvg hdisk8  # 将 hdisk8 添加到 rootvg 卷组

# smit mkvg
```

每个卷组都会分配一个卷组标识符（`VGID`）。在较旧的 `AIX` 版本中，`VGID` 是一个十六位的十六进制数，而在 `AIX 5L` 中是一个 `32` 位的十六进制数。系统中的每个 `VGID` 都由 `/etc/vg` 目录中的一个条目表示。

```
# ls /etc/vg
vg00012560841690B0   vg0001256084A8C772
vg00012560841690B00000000000000000
```

![](img/82f851021955589d82b22750fb3b1646_213_0.png)

要显示系统中现有卷组的配置，请使用 `lsvg` 命令：

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

卷组中的每个物理卷都标记有卷组描述符区域（`VGDA`）和卷组状态区域（`VGBA`）。`VGDA` 和 `VGBA` 是卷组中最重要的组件！`VGDA` 包含组成卷组的所有逻辑卷、物理卷和分区的标识符。`VGBA` 是一个位图，用于指示磁盘上哪些物理分区是过期的，需要同步更新。

当使用 `varyonvg` 命令或 `SMIT` 激活卷组时，`LVM` 在联机之前会验证它是否能访问至少 `51%` 的 `VGDA` 和 `VGBA` 副本。这种多数称为 *法定人数*（`quorum`），是 `LVM` 为确保数据完整性所必需的。任何不可用的物理卷都会被报告。系统管理员必须决定是否在设备不可访问时继续操作。如果法定多数是未建立卷组时，它不会被激活。然而，信不信由你，你可以使用 `varyonvg` 命令的 `-f` 开关强制将其设置为在线状态。

```
# varyonvg <VGname> # Vary a volume group online
# varyonvg -f <VGname> # Force vary on a volume group
```

你可以使用 `varyoffvg` 命令或通过 `SMIT` 使卷组离线。请注意，必须终止对卷组中所有逻辑卷的访问。卷组中的所有文件系统必须卸载，且任何分页空间不得处于活动状态。

```
# varyoffvg <VGname>
# smit varyoffvg
```

为了维护目的移除或替换卷组中的物理卷，请使用 `SMIT` 或 `chpv` 命令。

```
# reducevg <VGname> <PVname> # Remove the disk from VG
# rmdev -dl hdisk<x> # Remove the hdisk definition
```

替换磁盘...

```
# cfgrw -v # Let the system discover the disk
# lscpu # Find the newly found disk and write down the hdisk #
# chdev -l hdisk<x> -a pv=yes # Create a PVID for the new hdisk
# extendvg <VGname> <hdisk<x>> # Add the new disk into the volume group
```

> **注意** 当你从卷组中移除所有物理卷时，该卷组将从系统中删除（`reducevg` 命令）。

整个卷组可以作为单一单元从一个系统迁移到另一个系统。当卷组被导出时，指向它的所有引用都将从 `ODM` 中移除。当卷组在新系统上被导入时，所有设备表、特殊文件和 `/etc/filesystem` 条目都会自动添加到 `ODM` 中。你可以在同一系统上导出和导入卷组，以重新同步 `VGDA` 和 `ODM` 信息。

```
# exportvg <VGname>
# importvg <VGname> <PVname>
```

## 根卷组—rootvg

`AIX` 使用一个名为 `rootvg` 的特殊卷组来存放操作系统的根文件系统和默认分页区。为本地用户和应用文件系统使用独立的卷组是一个好主意。这样，你可以在系统激活时在不同系统间导出和导入这些卷组，并在操作系统升级前后迁移文件组。每次 `AIX BOS` 安装都会销毁 `rootvg` 的全部或部分。

### rootvg 的镜像

如果你不对根卷组进行镜像，那么你就存在单点故障。务必对 `rootvg` 进行镜像！我见过太多不必要的系统重建，就是因为 `rootvg` 没有进行镜像。对 `rootvg` 进行镜像是一个简单的过程，包括以下步骤，我们将把 `rootvg` 镜像到一个名为 `hdisk1` 的新磁盘：

1. 将 `hdisk1` 添加到 `rootvg` 以进行镜像：

   ```bash
   # extendvg rootvg hdisk1
   ```

2. 如果所有 `rootvg` 逻辑卷都创建得当，请使用此命令：

   ```bash
   # mirrorvg rootvg # This command will do it all if no errors occur
   ```

3. 或者（如果遇到问题的话）手动镜像 `rootvg`，但不要镜像转储设备（例如中的 `lv00`）：

   ```bash
   # lsvg # To make sure there are two drives in rootvg
   # lsvg -l rootvg # To see if anything is mirrored already
   # lsvg rootvg # To check available space
   ```

4. 镜像每个逻辑卷：

   ```bash
   # for N in $(lsvg -l rootvg | grep synced | awk '{print $1}' | grep -v lvol0)
   > do
   > echo $N
   > mklvcopy $N 2
   > done
   ```

5. 同步卷组：

   ```bash
   # syncvg -v rootvg
   # lsvg -l rootvg
   ```

6. 配置启动设备：

   ```bash
   # ipl_varyon -i
   PNAME        BOOT DEVICE     PVID             VOLUME GROUP ID
   hdisk0         NO             0000104735ac2310     000010472822f021
   hdisk1         YES            000010472822e532     000010472822f021

   # bosboot -a -d /dev/hdisk0

   bosboot: Boot image is 6955 512 byte blocks.

   # ipl_varyon -i
   ```

| PVNAME | BOOT DEVICE | PVID | VOLUME GROUP ID |
|---|---|---|---|
| hdisk0 | YES | 0001047375ac2330 | 00010472822f021 |
| hdisk1 | YES | 00010472822e2532 | 00010472822f021 |

```
# chvg -a'y' -Q'n' -x'n' rootvg ◄── A quorum of disks required = no
# bootlist -m normal -o
hdisk1
# bootlist -m normal hdisk0 hdisk1
# bootlist -m normal -o
hdisk0
hdisk1
# lsvg rootvg | grep -i QUORUM
OPEN LVs: 14 QUORUM: 1
```

`mirrorvg` 命令在幕后为你执行了所有的 `mklvcopy` 命令。由于禁用了磁盘仲裁（`quorum`），我们必须重启系统以使更改生效。

```
# shutdown -r now
```

## 添加卷组

正如我们之前讨论的，卷组由一个或多个磁盘（或物理卷）组成。创建新卷组时，我们有两个选项：普通卷组和大型卷组。大型卷组将最大逻辑分区数从 `256` 扩展到 `512`。表 `11-2` 和 `11-3` 显示了普通卷组和大型卷组限制之间的区别。

| VG 中磁盘的最大数量 | 每个磁盘的最大分区数 |
|---|---|
| 1 | 32512 |
| 2 | 16256 |
| 4 | 8128 |
| 8 | 4096 |
| 16 | 2032 |
| 32 | 1016 |

**表 11-2. 普通卷组限制**

| VG 中磁盘的最大数量 | 每个磁盘的最大分区数 |
|---|---|
| 1 | 130048 |
| 2 | 65024 |
| 4 | 32512 |
| 8 | 16256 |
| 16 | 8128 |
| 32 | 4096 |
| 64 | 2032 |
| 128 | 1016 |

**表 11-3. 大型卷组限制**

要指定大型卷组，请在 `mkvg` 命令中添加 `-B` 开关。如果省略 `-B` 开关，卷组将是普通卷组。要指定磁盘数量和每个磁盘的最大分区数，使用 `t` 因子。`t` 因子是 `1016` 的倍数。每当 `t` 因子增加一级，物理分区的数量就会翻倍，但卷组中允许的最大磁盘数会减半。

要使用 `hdisk4` 创建一个名为 `appvg` 的普通卷组，其 `PP` 大小为 `16MB` 且最多可包含 `16` 个磁盘，请执行以下命令：

```
# mkvg -s 16 -t2 -y appvg hdisk4
```

`-s 16` 指定了 `16MB` 的 `PP` 大小，`-t2` 指定了 `t` 因子为 `2`。`-y` 开关指定卷组名称为 `appvg`。在表 `11-2` 中，我们可以看到在这个普通卷组中，每个磁盘最多可以有 `16256` 个分区，且最多可以有 `16` 个磁盘。

要创建一个名为 `bigappvg` 的大型卷组，最多可包含 `16` 个磁盘和每个磁盘 `8128` 个分区，并使用 `hdisk5` 到 `hdisk10`，请执行以下命令：

```
# mkvg -B -t8 -y bigappvg hdisk5 hdisk6 hdisk7 hdisk8 hdisk9 hdisk10
```

我们还可以使用以下命令将普通 `appvg` 卷组更改为大型卷组：

```
# chvg -B appvg
```

## 导入和导出卷组

卷组的一个好处是它们具有可移植性。你可以在一台机器上导出卷组，将磁盘召回到另一个系统，然后导入该卷组。导出和导入卷组的两个命令分别是 `exportvg` 和 `importvg`。导出卷组时，你会将其完全从 `ODM` 中移除；导入卷组时，你会将其添加到 `ODM` 中。作为一个例子，我们希望在另一台机器上使用我们的 `bigappvg` 卷组。以下命令将导出卷组并导入卷组。

在机器 `A` 上：

```
# exportvg bigappvg
```

在机器 `B` 上：

```
# importvg -y bigappvg hdisk5
```

之前的例子中假设了很多内容。你需要使用卷组中其中一个磁盘的 `PVID` 作为目标磁盘集，该集包含导出的 `VG`。（还记得 `VGDA` 吗？）在这个例子中，我们通过检查 `lspv` 命令的输出发现 `PVID` 位于 `hdisk5` 上。卷组还有一个在系统中唯一的 `主设备号`（`major number`）。要在系统中找到下一个可用的主设备号，请执行以下命令：

```
# lvlsmajor
```

要指定主设备号，使用 `-V` 开关。在我的机器上，下一个可用的主设备号是 `27`。因此我们将 `importvg` 命令更改为使用主设备号 `27`：
