
密度也是特定类型磁带的因子。如果你使用的是 DDS 兼容驱动器，如果你在两者之间共享数据，则需要避免使用最高密度。如果交换的数据量很，最大的机会是以驱动器支持的最低密度读取磁带。

## 在拨打支持之前

如果你无法读取磁带，请检查以下项：

- 磁带是空白的吗？
- 消磁了吗？
- 你尝试过用 `dd` 查看磁带是否包含数据吗？
- 磁带格式被 Tru64 UNIX 支持吗？
- 如果磁带来自 UNIX 系统，你尝试过 `cpio`、`ltf` 和 `dump` 吗？
- 如果磁带来自非 UNIX 系统，你尝试过 `ltf` 和 `tar` 吗？
- 磁带密度被驱动器支持吗？

## 8.3 存储管理器

在本节中，我们将讨论逻辑存储管理器（LSM）。LSM 是一个强大的产品，用于管理磁盘并在软件层面实现某些 RAID 选项。LSM 设置和操作的细节超本书的范围；有关 LSM 的许多功能和命令，我们建议参考 Tru64 UNIX 手册。

### 8.3.1 设备故障

LSM 最常见的故障排除之一是处理其控制设备故障。理想情况下，你已经对这种情况做了计划，并使用 RAID 1（镜像）或 RAID 5 使文件系统冗余。在这种情况下，你可以轻松更换故障设备。但如果文件系统没有冗余，你可能需要尽快修复问题。

在 LSM 中检测故障的工具是 `volprint` 和 `voldisk` 命令。这些工具将显示哪些设备已故障以及配置的通用状态。在下面的示例中，`voldisk list` 显示了一个故障磁盘：

```
voldisk list

DEVICE  TYPE      GROUP    STATUS

dsk1    sliced    disk01   online

dsk2    sliced    disk02   failed
```

相应的 `volprint` 输出显示该驱动器的 plex 处于“DISABLED”状态。

```
volprint

Disk group: rootdg

DG NAME  NCONFIG   NLOG    MINORS  GROUP-ID

DM NAME  DEVICE    TYPE    PRIVLEN  PUBLEN  STATE

V NAME   USETYPE   KSTATE   STATE   LENGTH  READPOL PREFLEX NCOL/WIDE MODE

PL NAME  VOLUME    KSTATE   STATE   LENGTH  LAYOUT  NCOL/WIDE MODE

SD NAME  PLEX      DISK    DISKOFFS LENGTH [COL:/]OFF DEVICE MODE

dg rootdg    default   default 0 995304195.1029.18791:19:11:43

dm disk01 sliced 4096 17765065 - -

dm disk02 - - NODEVICE

v nda_vol ENABLED ACTIVE 1776432 SELECT -

pl nda_vol-01 nda_vol ENABLED ACTIVE 177632 CONCAT - RW

sd disk01-01 nda_vol-01 disk01 0 177632 dsk1 ENABLED

pl nda_vol-02 nda_vol DISALLOWED NODEVICE 177632 CONCAT RW

sd disk02-01 nda_vol-02 disk02 0 177632 - RELOC
```

注意在该示例中，卷仍然处于“ENABLED ACTIVE”状态，这意味着即使驱动器处于故障状态，它也能工作。你可以修复问题而用户不会察觉，因为即使在磁盘故障后数据仍然可用。

### 8.3.2 Volumnotify

LSM 的一个潜在问题是在大多数情况下，它工作得太好了。例如，你可能会发现一个镜像卷包含故障磁盘已经有一段时间。LSM 只是静静地完成了它的工作，可能只在错误日志中写了一条消息，而系统继续正常运行。针对这些情况设计了监控（watch）和通知（notify）设施。它们共同通知你 LSM 发生的事件和问题。

- `smartwatch(8)` 是一个监控 LSM 的脚本，等待异常事件的发生。它向 root 用户（默认）或命令行中指定的用户发送电子邮件。
- `volnofify(8)` 是一个实用程序，用于显示由 LSM 配置守护进程管理的磁盘和配置更改相关的事件。`volnofify` 显示请求的事件类型，直到它被信号杀死、接收了指定数量的事件或通过了指定时间。

## 8.2 磁带

表 8.1 Tru64 UNIX 支持的格式和工具

| 格式 | 读取工具 | 写入工具 |
| --- | --- | --- |
| tar | tar and pax | tar and pax |
| cpio | cpio and pax | cpio and pax |
| dump | restore | dump |
| vdump | vstore | vdump |
| ANSI | ltf | ltf |
| Raw | dd or custom program | dd or custom program |

LSM 支持的 RAID 级别如下：

- RAID 0—也称为条带（striping），RAID 级别0不具备冗余，因此并不真正符合 RAID 的缩写。在级别0中，数据分布在各个驱动器上，从而获得更高的数据吞吐量。由于没有存储冗余信息，性能非常好，但阵列中任何磁盘的故障会导致数据丢失。
- RAID 1—RAID 级别1通过将所有数据写入两个或多个驱动器来提供冗余。与单个驱动器相比，级别1 RAID 阵列的读取速度通常更快，写入速度较慢；如果其中一个驱动器故障，数据不会丢失。这是一个很好的入门冗余系统，因为只需要两个驱动器。另一方面，由于数据完全复制，每兆字节的成本很高。这种级别通常被称为镜像（mirroring）。
- RAID 0+—此级别在原始的 Berkeley 论文中从未被提到，但它是镜像和条带的结合，为每份数据副本提供完全的冗余以及条带带来的性能优势。该级别的每兆字节成本与 RAID 1 相同，但性能往往更好。
- RAID 5—RAID 级别5与 RAID 0 类似，但增加了一个磁盘并在驱动器之间分配校验位以获得冗余。冗余提供的成本仅略高于 RAID 0，但会有性能损失。

### 8.3.4 修复故障的 LSM 驱动器

当 LSM 控制下的驱动器发生故障时，需要放置新磁盘来替换故障驱动器。然而，当涉及 LSM 时，不仅仅是替换损坏的驱动器。以下步骤描述了在 LSM 中替换故障驱动器的过程：

- 为磁盘贴上新标签，如果可能，恢复旧的磁盘标签。如果你没有在文件中保存标签（这是一个良好的习惯），查看是否可以找到另一个在 LSM 中以相同方式使用的相同类型驱动器，将其标签复制到新磁盘。
- 使用“`voldisk rm`”命令删除对故障驱动器的旧引用（如“`voldisk list`”所示）。
- 使用“`voldisk -f init`”命令初始化新磁盘的私有区域。
- 使用“`voldg -k adddisk`”命令将故障驱动器与其旧媒体名称重新连接。
- 如果磁盘位于镜像卷中，此时副本（plexes）将不会同步。允许“`volcover -sb`”命令使副本重新同步。

如果问题不是驱动器完全故障，而是瞬时故障，导致驱动器本身仍然良好，请使用以下步骤进行恢复：

- 使用“`voldisk online`”命令将 LSM 磁盘恢复上线。
- 使用“`voldg -k adddisk`”命令将驱动器重新连接到磁盘媒体名称。
- 使用“`volrecover -sb`”命令同步镜像卷。

### 8.3.5 卷配置守护进程故障

卷配置守护进程（`vold`）是 LSM 架构中的关键组件。该进程必须一直运行，以响应配置更改请求并收集有关 LSM 状态的信息。守护进程的问题并不意味着 LSM 控制下的卷和数据出现问题。然而，如果进程由于某种原因未能响应或退出，则存在必须解决的严重问题。如果你的 LSM 配置已设置并运行了一段时间，问题的第一个症状可能是来自某个 LSM 命令的错误。

```
# voldisk list

lsm:voldisk: ERROR: IPC failure: Configuration daemon is not accessible
```

如果你收到此类错误，请使用以下命令检查进程的健康状况：

## 8.3 逻辑存储管理器

```
# voldctl mode

mode: not-running
```
