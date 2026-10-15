
```
# lvdisplay /dev/vg00/lvol1
-- Logical volumes --
LV Name /dev/vg00/lvol1
VG Name /dev/vg00
LV Permission read/write
LV Status available/syncd
Mirror copies 0
Consistency Recovery MW C
Schedule parallel
LV Size (Mbytes) 48
Current LE 12
Allocated PE 12
Stripes 0
Stripe Size (Kbytes) 0
Bad block off
Allocation contiguous strict/contiguous/
```

关于所显示各个字段的信息，可以在该命令的在线手册页中找到。

### pvdisplay

`pvdisplay` 命令提供磁盘资源管理的状态和配置信息，特别是针对 LVM 卷组中的物理卷。对于每个物理卷，您可以显示在物理卷上分配有区的逻辑卷，以及所有物理区的使用情况。清单 5-8 显示了 `pvdisplay` 的输出。

### 清单 5-8 显示 LVM 卷组中物理卷信息的 pvdisplay 命令输出。

```
# pvdisplay /dev/dsk/c0t5d0
-- Physical volumes --
PV Name /dev/dsk/c0t5d0
VG Name /dev/vg00
PV Status available
Allocatable yes
VGDA 2
Cur LV 8
PE Size (Mbytes) 4
Total PE 1023
Free PE 607
Allocated PE 416
Stale PE 0
IO Timeout (Seconds) default
```

### vgdisplay

`vgdisplay` 命令用于获取系统中配置的 LVM 卷组信息。该命令可用于获取磁盘资源状态和配置信息。您可以获取系统中每个活动卷组的每个逻辑卷、物理卷和物理卷组的配置信息。您可以如清单 5-9 所示获取卷组、逻辑卷和物理卷的状态。来自 `lvdisplay` 和 `pvdisplay` 的一些信息也由该命令提供。例如，使用 `verbose` 选项，您不仅可以获取卷组状态，还可以获取卷组内所有逻辑卷的状态。

您可以使用 `lvdisplay` 或 `pvdisplay` 分别获取逻辑卷或物理卷的更详细信息。

## 使用系统仪表化

诸如简单网络管理协议 (`SNMP`) 和桌面管理接口 (`DMI`) 等网络和管理标准已被开发出来，以帮助简化管理工作。这些标准提供了构建仪表化的行业标准方式，以及接入仪表化的行业标准方式。`SNMP` 用于访问管理信息库 (`MIBs`)，而 `DMI` 用于访问管理信息格式 (`MIFs`)。

标准 `MIB` 和 `MIF` 定义了任何供应商都可以提供的指标。所提供的信息通常被称为仪表化信息。私有 `MIB` 和 `MIF` 提供特定于供应商的仪表化信息。本节探讨了通过这些标准之一可用的一些磁盘仪表化信息。

已存在许多用于访问仪表化信息的工具。多家供应商提供浏览器和监控功能，使用通用界面访问来自不同硬件平台和操作系统的仪表化对象。例如，每个常见的企业管理框架，包括 `HP OpenView Network Node Manager`、`HP OpenView IT/Operations` 和 `CA Unicenter TNG`，都提供 `MIB` 浏览器工具来访问 `MIB` 数据。图 5-1 中展示了一个示例。存在工具包以提供接口，使开发人员能够编写自己的工具来监控或跟踪此信息。也存在用于进行自定义仪表化的工具包。

两种标准均提供磁盘类型信息，并且随着时间推移，越来越多的信息正在被仪表化。

## 简单网络管理协议

`MIB` 是表示特定类别信息的一种标准方式。例如，`MIB-II` 提供了系统的有用信息，例如活动 `TCP` 连接的数量，系统

图 5-1 在 OpenView IT/O 中使用 MIB 浏览器访问磁盘相关信息。

![](img/eae88b61ada165139a1d9b546a34140b_125_0.png)

### 清单 5-9 显示卷组信息的 vgdisplay 命令输出。

```
# vgdisplay -v /dev/vg00
-- Volume groups --
VG Name /dev/vg00
VG Write Access read/write
VG Status available
Max LV 255
Cur LV 8
Open LV 8
Max PV 16
Cur PV 1
Act PV 1
Max PE per PV 2000
VGDA 2
PE Size (Mbytes) 4
Total PE 1023
Alloc PE 416
Free PE 607
Total PVG 0
-- Logical volumes --
LV Name /dev/vg00/lvol1
LV Status available/syncd
LV Size (Mbytes) 48
Current LE 12
Allocated PE 12
```

硬件和版本信息等。本章后面讨论的 OpenView IT/O 提供了一个 `MIB` 浏览器，可帮助您发现可用的 `MIB`，并查看每个 `MIB` 提供的信息。`MIB` 浏览器工具可以检查 `MIB` 中包含的任何项的值。如果您发现某个 `MIB` 包含一些有用的字段，您可以使用 `MIB` 浏览器从目标系统中收集这些数据。生成的数据显示在 `MIB` 浏览器的输出窗口中。通过浏览可用的 `MIB` 并查询选定 `MIB` 字段的值，您可以收集监控系统和排查问题所需的具体信息。

`SNMP` 接口提供对各种 `MIB` 中存储的对象的访问。在 `HP-UX` 系统中，`HP-UNIX MIB` 定义了用于监控磁盘资源的各种指标，例如文件系统使用情况。其他供应商，如 Sun，拥有提供类似信息的供应商特定 `MIB`。完整的 `MIB` 定义列在附录 A“使用标准”中。

`HP-UNIX MIB` 文件系统表中的对象可以被监控，以检测文件系统使用率何时达到特定阈值，从而使您能够避免文件系统故障，例如空间不足。以下是文件系统表中每个条目可用的对象列表：

- `fileSystemName`
- `fileSystemBlocks`
- `fileSystemBfree` (可用块)
- `fileSystemBavail` (非超级用户可用的块)
- `fileSystemBsize`
- `fileSystemFiles`
- `fileSystemFree`
- `fileSystemDir`

请注意，每个挂载的文件系统都有一个表条目。

## 桌面管理接口

`HP-UX MIF`（也称为系统 `MIF`）提供了 `DMI` 仪器化。对于磁盘监控，`DMI` 仪器化为磁盘硬件设备以及配置、状态和事件提供。系统 `MIF` 中也提供文件系统资源信息。带有 `DMI` 仪器化的磁盘相关指标如下列所示。完整的系统 `MIF` 和软件 `MIF` 定义见附录 A。

主机存储表包含关于逻辑存储区域的信息。它适合监控磁盘使用情况和分配失败事件。它包含以下字段：

- 类型
- 描述
- 分配单元
- 大小
- 已用
- 存储分配失败

主机设备表包含关于系统中硬件设备的信息。它适合监控硬件配置和故障。它包含以下字段：

- 设备类型
- 描述
- 设备 ID
- 设备状态 (运行中, 警告, 停机, 测试中, 保留, 未知)
- 设备错误

还可以为主机设备表中的设备生成事件，包括设备状态更改、初始化失败和配置错误。事件包含分配的严重级别，例如 信息 (`Information`)、正常 (`OK`) 或 严重 (`Critical`)。

主机磁盘存储表包含主机设备表中设备的存储信息。它包含以下字段：

- 访问方式 (只读, 读/写)
- 介质类型 (例如，硬盘, 软盘等)
- 可移动
- 容量 (以千字节为单位)

文件系统表包含以下字段：

- `FSMountPoint`
- `RemoteFSMount`
- `FSAccess`
- `FSBootable`
- `FSLastFullBackupDate`
- `FSLastPartialBackupDate`

许多供应商正在为磁盘资源以及设备特定信息开发更多的 `DMI` 仪器化。

## 使用事件监控工具

事件监控涉及在检测到故障和其他有趣的状态时生成通知消息。这与 `UNIX` 命令不同，`UNIX` 命令仅在要求时报告状态信息。您可以配置事件监控器，以便在状态发生变化或满足预定义阈值条件时生成事件。一些事件监控器在磁盘设备级别发生故障或错误时生成事件。

本节中讨论的几个监控器已集成到事件监控服务 (`EMS`) 框架中。`EMS` 框架仅在 `HP-UX` 系统上可用，它使系统能够以一致的方式提供监控器。虽然 `EMS` 框架本身是免费提供的，但监控器通常作为单独的产品提供，或者随其提供监控的个别产品捆绑在一起。
