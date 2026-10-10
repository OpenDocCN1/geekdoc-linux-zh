
`V-Path` 是系统可以看到磁盘驱动器的虚拟路径。因此，当您创建逻辑卷的卷组时，您需要使用 `V-Path` 定义来指定磁盘。使磁盘实现“`RAID`”功能的技巧在于，我们通过负载均衡软件将每个逻辑卷条带化地分布在所有光纤通道适配器上。对于同一个内部 `RAID` 级别 5 阵列，四条路径带来的性能提升巨大。`ESS` 内部使用 `RAID` 级别 5，因此这种配置性能非常出色！您也可以在 `Shark` 中使用 `JBOD`（Just a Bunch of Disks，即一堆磁盘），但在磁盘故障时您将失去自动恢复功能。有关存储区域网络的更多信息，请参见第 29 章。

## 固定磁盘架构

磁盘本身是由多个像唱片一样堆叠在轴上的盘片组成的（参见图 11-1）。每个盘片都涂有一层磁性基底。一个或多个电磁头可以在盘片上从外缘到内缘前后移动。磁头对围绕盘片表面格式化在圆形磁道上的磁性粒子的极化做出反应。磁头由磁盘控制器电路定位，该电路接收来自操作系统的指令。

大多数磁盘出厂时已预先格式化了坏扇区映射。如果您必须格式化磁盘，请调用 `diag` 命令或将系统重启到单用户维护模式。从 `diag` 功能选择中选择 `Task Selection`（任务选择），然后选择 `Media Format`（介质格式化）和 `Media Certify`（介质认证）。

```
# diag
```

-   功能选择
-   任务选择（诊断、高级诊断、服务辅助工具等。）
-   服务辅助工具
-   格式化介质
-   认证介质

![](img/82f851021955589d82b22750fb3b1646_197_0.png)

磁盘上的格式化空间由扇区或块组成。扇区大小因制造商和型号而异，可能是固定的，也可能是可变的。磁道由在每个盘片上排列成圆形的扇区组成。盘片上堆叠的磁道构成一个柱面。如今所有这些大容量磁盘都是技术发展的结果，该技术极大地减小了在盘片上运行的磁头尺寸。如果您打开一个磁盘驱动器（仅对故障磁盘这样做！）并从头臂上取下磁头，您会看到磁头只是一个微小的斑点。在这项新技术出现之前，磁头的大小大约是小拇指指甲那么大。

## 磁盘安装

若要向系统添加新的 `SCSI` 磁盘，请将该磁盘插入系统单元背面的某个 `SCSI` 适配器上。最好在系统断电的情况下进行此操作，但如果您的磁盘和子系统支持热插拔，则可以在在线状态下进行。单个 `SCSI` 适配器可以菊花链连接多个 `SCSI` 设备。链中的每个磁盘必须代表一个唯一的 `SCSI` ID 和逻辑单元号（`LUN`）。`SCSI` ID 可通过驱动器组件或外壳上的跳线或开关进行选择。旧式 `SCSI` 驱动器的 `SCSI` ID 范围从 0 到 7，而宽体和 `Ultra` `SCSI` 的范围从 0–15，其中 7 通常分配给适配器。系统启动时，新磁盘会自动识别并记录在 `RDS` 和 `ODM` 数据库中。您可以通过调用 `cfmgrp` 或使用 `mkdev` 命令在线更新设备信息。新磁盘被分配下一个可用的 `hdisk<nn>` 标签。

```
# mkdev -c disk -s scsi -t oadisk -p scsi2 -w 8,0,0 -l hdisk10 -a pv=yes
# cfmgr -v1 scsi2
(或)
# cfmgr -v
(或)
# smitty cfmgr
# lsvg
# lsdev -Cc disk
```

使用此处显示的 `lsvg` 和 `lsdev` 命令以确保磁盘具有 `PVID` 并处于可用状态。

## 管理物理卷

`AIX` 中的物理磁盘卷被命名为 `hdisk#`，其中 `#` 是从 0（零）开始的整数。磁盘由配置管理器检测、配置并命名，使用 `cfmgrp` 命令。磁盘的实际名称取决于其在系统中的物理安装位置，因为 `cfmgrp` 会遍历总线，并在找到每个磁盘时分配 `hdisk` 编号。在大多数系统中，`cfmgr` 会以并行模式遍历总线，但您可以向 `cfmgr` 命令添加 `-s` 标志以指定串行模式来覆盖此方法。

有一些技巧会影响 `hdisk` 编号的分配，您在某个时候可能需要使用它们。例如 `HASCMP` 集群系统（有关更多详细信息请参见第 28 章），在这种情况下，确保共享磁盘的 `hdisk` 编号同步至关重要。使 `hdisk` 编号同步的一种方法是每次只打开一个外部磁盘集，并运行 `cfmgr` 多次，每个磁盘集开启时运行一次。诀窍是在处理过程的每一步中，在每台机器上复制相应的操作。

程序大致如下：

1.  停止两个系统上的所有应用程序。
2.  移除所有您想要同步且不在 `rootvg` 中的磁盘的 `hdisk` 定义。对每个磁盘使用 `rmdex -hdisk#` 命令。对共享磁盘集群中的所有系统重复此操作。
3.  运行 `lssp` 命令以确保所有磁盘已移除。
4.  关闭所有您希望 `hdisk` 编号同步的磁盘。
5.  打开第一组磁盘。这些磁盘将获得最低的 `hdisk` 编号。
6.  在每个系统上运行 `cfmgr -v`。如果您知道磁盘的父适配器，可以执行 `cfmgr -vl *adapter*` 命令。
7.  运行 `lssp` 以确保磁盘在每个系统上的编号符合您的要求，并确保磁盘编号同步。您需要参考 `PVID` 以确保所有系统上的 `PVID` 和 `hdisk` 编号匹配。
8.  对其余磁盘集重复步骤 5、6 和 7。

## 更简单的磁盘重命名方法

如果前一节让您感到困惑，请尝试本节的练习。场景如下：我们在 `scsi1` 控制器上有三个名为 `hdisk2`、`hdisk3` 和 `hdisk4` 的磁盘。我们需要移除这些磁盘，并将它们作为 `hdisk10`、`hdisk12` 和 `hdisk14` 重新添加回系统。

第一步是列出系统内的磁盘位置：

```
# lsdev -Cc disk

  hdisk0  Available  04-B0-00-0,0  Other SCSI Disk Drive
  hdisk1  Available  04-B0-00-1,0  Other SCSI Disk Drive
  hdisk2  Available  04-03-00-8,0  Other SCSI Disk Drive
  hdisk3  Available  04-03-00-9,0  Other SCSI Disk Drive
  hdisk4  Available  04-03-00-10,0  Other SCSI Disk Drive
```

接下来，我们需要列出系统中适配器的位置：

```
# lsdev -Cc adapter | grep scsi

  scsi0  Available  04-B0  Wide SCSI I/O Controller
  scsi1  Available  04-03  Wide SCSI I/O Controller
```

现在，我们需要列出涉及此磁盘重新分配的卷组：

```
# lspv

  hdisk0    000400434b33e6eb    rootvg
  hdisk1    000400434a771e22    rootvg
  hdisk2    000400439e42cd74    appvg
  hdisk3    000400439a5def f0    appvg
  hdisk4    000400439ae07e9    appvg
```

在进行任何更改之前，我们首先需要使目标卷组不可用：

```
# varyoffvg appvg
```

> 有关更多详细信息，请参阅本章稍后的“开启和关闭卷组”部分。

现在，我们可以移除 `scsi1 (2@8,0 3@8,0 4@0,0)` 上的目标设备。在命令提示符下，输入以下命令序列。基本上，这就像在命令行上编写一个 shell 脚本：

```
# for N in 2 3 4
> do
> rmdev -dl hdisk$N
> done
```

> **注意** 不要输入大于号（>），因为它们是提示符。每行结束后按下 `ENTER` 键。

预览用于以新名称添加设备的命令：

```
# for NA in 10@8,0 12@9,0 14@10,0
> do
> N=$(echo $NA | awk -F@ '{print $1}')
> A=$(echo $NA | awk -F@ '{print $2}')
> echo "mkdev -c disk -s scsi -t oadisk -p scsi1 -w $A -l hdisk$N -a pv=yes"
> done
```

预览输出将显示这些命令：

```
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 8,0 -l hdisk10 -a pv=yes
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 9,0 -l hdisk12 -a pv=yes
mkdev -c disk -s scsi -t oadisk -p scsi1 -w 10,0 -l hdisk14 -a pv=yes
```

现在移除 `echo` 围绕在 `mkdev` 命令周围的部分，以实际执行这些命令：

```
# for NA in 10@8,0 12@9,0 14@10,0
> do
> N=$(echo $NA | awk -F@ '{print $1}')
> A=$(echo $NA | awk -F@ '{print $2}')
> mkdev -c disk -s scsi -t oadisk -p scsi1 -w $A -l hdisk$N -a pv=yes
> done
```

结果输出如下，显示我们新的 `hdisk` 编号：

```
hdisk10 Available
hdisk12 Available
hdisk14 Available
```

列出新的设备名称：

```
# lsdev -Cc disk

hdisk0 Available 04-B0-00-0,0 Other SCSI Disk Drive
hdisk1 Available 04-B0-00-1,0 Other SCSI Disk Drive
hdisk10 Available 04-03-00-8,0 Other SCSI Disk Drive
hdisk12 Available 04-03-00-9,0 Other SCSI Disk Drive
hdisk14 Available 04-03-00-10,0 Other SCSI Disk Drive
```

列出 `hdisk` 编号、`PVID` 以及关联的卷组：

```
# lsvg

hdisk0 0004040434b32e6eb rootvg
hdisk1 0004040434a781e22 rootvg
hdisk10 0004040439e42cd74 appvg
hdisk12 0004040439a5def0 appvg
hdisk14 0004040439a5e07e9 appvg
```

请注意，卷组中的物理磁盘是通过 `PVID` 而不是 `hdisk` 编号来识别的。我们在将其开启之前不需要再次导入卷组。

```
# lqueryvg -Atp hdisk10

Max LVs:              256
PP Size:              25
Free PPs:             504
LV count:             3
PV count:             3
Total VGDAs:          3
Conc allowed:         0
MAX PPs per PV:       1016
MAX PVs:              32
Conc Autovar:         0
Varied on:            0
Logical:
      000400439a5df5d2.1   lv1ac1 1
      000400439a5df5d2.2   lcg1v00 1
      000400439a5df5d2.3   lv01 1
Physical:
      000400439a5d5eff 1    0
      000400439a5e07e9 1    0
      000400439e42cd74 1    0
Total PPs:            813
```

通过再次开启 `appvg` 来使卷组可用：

```
# varyonvg appvg     # 在这种情况下无需 importvg
```

## 配置热备盘

在此热备示例中，`appvg` 从 `hdisk1` 镜像到 `hdisk2`，而 `hdisk3` 和 `hdisk4` 将作为热备盘：

```
# lsvg appvg
VOLUME GROUP:   appvg                  VG IDENTIFIER: 0000224800004900000000000ebab4a5fe2
VG STATE:       active                PP SIZE:        32 megabyte(s)
VG PERMISSION:  read/write            TOTAL PPs:      2184 (69888 megabytes)
MAX LVs:        256                   FREE PPs:       2184 (69888 megabytes)
LVs:            0                     USED PPs:       1092 (34944 megabytes)
OPEN LVs:       0                     QUORUM:         1
TOTAL PVs:      4                    VG DESCRIPTORS: 3
STALE PVs:      0                    STALE PPs:      0
ACTIVE PVs:     4                    AUTO ON:        yes
MAX PPs per PV:  1016         MAX PVs:              32
LTG size:        128 kilobyte(s)  AUTO SYNC:          no
HOT SPARE:       no
```

检查与磁盘关联的卷组：

```
# lsvpv
hdisk0        0000468644af1894        rootvg
hdisk1        00003095a330a867        appvg
hdisk2        00003095a330baa8        appvg
hdisk3        00003095a330bca2        appvg
hdisk4        00003095a330c825        appvg
```

`chpv` 命令有一个 `-h` 标志，用于设置物理卷的特征和分配权限，使其可以作为热备盘使用。对于非镜像逻辑卷，`-h` 标志没有效果。`-h` 标志可以接受 `y` 或 `n` 作为参数，以将磁盘添加至或从热备池中移除。

设置热备盘：

```
# chpv -h 'y' hdisk3 hdisk4    # -h [y|n]
```

检查热备盘：

```
# for N in a867 baa8 bca2 c825
> do
> lquerypv -g 000022480004a900000000bab4aeefe2 -P 00003095a330$N -S
> done
0
0
32
32
```

> **注意** 不要输入大于号（>）；这些是提示符。

与 `chpv` 命令类似，`chvg` 命令使用 `-h` 标志来设置卷组的备用特征，该卷组由 `VolumeGroup` 参数指定。`-h` 标志有四个可用的参数：

-   `y` 允许从故障磁盘分区到单个热备盘的自动迁移。
-   `Y` 允许故障磁盘的自动迁移，并且可以迁移到整个热备池。这与一对一的分区迁移不同。
-   `n` 禁止故障磁盘迁移。这是默认设置。
-   `r` 从卷组的热备池中移除所有磁盘。

接下来，我们将为卷组启用热备：

```
# chvg -h 'y' -s 'y' appvg
```

我们在上一个命令中使用 `s` 标志来同步镜像。

查看卷组的变化：
