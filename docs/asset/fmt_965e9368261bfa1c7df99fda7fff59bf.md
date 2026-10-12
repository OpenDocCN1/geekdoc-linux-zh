
指定用于为此设备创建符号链接的路径。

- `DO_FSTAB`

  布尔值 (y/n) 设置：指定是否应为此设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`

  布尔值 (y/n) 设置：指定在挂载前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`

  布尔值 (y/n) 设置：指定是否在插入卡片时自动挂载此设备。

- `FSTYPE`, `OPTIONS`, `MOUNTPT`

  用于 `fstab` 条目和/或挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_FUSER`

  卡弹出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备正忙时 `cardctl eject` 将关闭设备。如果 `NO_FUSER` 为 `true`，脚本将不会杀死使用已弹出设备的进程。

例如，这里是一个配置 SCSI ID 为 3 的磁盘设备（带有两个分区）以及 SCSI ID 为 6 的光驱的脚本：

```bash
case "$ADDRESS" in
*.sd,.*0,3,0)
  # 此设备有两个分区...
  PARTS="1 2"
  ;
  *.sd,.*0,0,1)
  # 分区 1 的选项：
  # 更新 /etc/fstab，并在 /usr1 上挂载 ext2 文件系统
  DO_FSTAB="y" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="usr1"
  ;
*.sd,.*0,3,2)
  # 分区 2 的选项：
  # 更新 /etc/fstab，并在 /usr2 上挂载 MS-DOS 文件系统
  DO_FSTAB="y" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="mddos"
  OPTS=""
  MOUNTPT="usr2"
  ;
*.sr,.*0,6,0)
  # SCSI ID 6 光驱的选项
  PARTS=""
  DO_FSTAB="y" ; DO_FSCK="n" ; DO_MOUNT="y"
FSTYPE="iso9660"
OPTS="ro"
MOUNTPT="/cdrom"
::
esac
```

## 4.6.2 关于特定卡片的说明

- `Adaptec APA-1480` CardBus 卡需要一个较大的 IO 端口窗口（在 256 端口主体上对齐的 256 个连续端口）。可能需要扩展 `/etc/pcmcia/config.opts` 中的 IO 端口区域，以确保能找到如此大的窗口。

- 不支持 `Adaptec APA-460` SlimSSI 适配器。此卡最初以 `Tranter` 为名销售，当 `Adaptec` 与 `Tranter` 合并后，他们继续带有 `Adaptec` 标签销售 `Tranter` 卡。`APA-460` 与任何现有的 Linux 驱动都不兼容。

- 我收到过一个关于 `New Media Bus Toaster` 和 `UMAX Astra 1200` 扫描仪之间发生不良交互的报告。由于 SCSI 协议的复杂性，诊断 SCSI 设备的问题非常困难，值得考虑可能存在此类未记录的冲突组合。

## 4.6.3 诊断 SCSI 适配器问题

- 使用 `aha152x_cs` 驱动（`Adaptec`、`New Media` 及其他少数驱动使用），SCSI 断开/重置似乎是磁带驱动故障的频繁来源。要禁用此“功能”，请向 `/etc/pcmcia/config.opts` 中添加以下内容。

- 同样使用 `aha152x_cs` 驱动，某些设备似乎需要更长的启动延迟，通过 `reset_delay` 模块参数控制。`Yamaha 4416S CDR` 光驱就是其中一个设备。结果是设备识别成功，然后导致系统挂起。在这种情况下，请尝试调整该参数。

- 另一个 SCSI 设备探测的潜在源是针对多个 LUN 的探测。如果你看到设备检测成功，随后在探测该设备的 LUN 1 时出现 SCSI 超时，请禁用内核的 `CONFIG_SCSI_MULTI_LUN` 选项。

- 如果你将 SCSI 配置为模块（`CONFIG_SCSI="m"`），你可能需要修改 `/etc/pcmcia/config` 以将 SCSI 模块加载到相应的 scsi 驱动中。

- 如果在探测 SCSI 总线时因“timeout”消息导致中止命令，你几乎肯定存在中断冲突。

- 如果主机驱动程序报告“no SCSI devices”，请验证你的内核在编译时是否包含了适用于你设备的适当顶层驱动（即磁盘、磁带、光驱和通用驱动）。如果缺少顶层驱动，该类型的设备将被忽略。

## 4.7 PCMCIA 内存卡

`memory_cs` 驱动处理所有类型的内存卡，并为具有其他功能的卡片提供对 PCMCIA 内存空间的直接访问。加载时，它会创建一个字符设备和块设备的组合。请参阅主页获取设备命名方案的完整描述。块设备用于类似磁盘的访问（创建和挂载文件系统等）。字符设备用于对任意位置进行“原始”无缓冲读取。传递给内存的设备地址由两个字段组成：方案和插槽号。某些闪存卡和大多数 RAM 卡会加载“卡片信息”（`CIS`）。通常情况下，`cardmgr` 会假设任何带有 `CIS` 的卡都是简单模块并加载 `memory_cs` 驱动。因此，通用卡识别问题的常见副作用是，其他类型的卡可能被误识别为内存卡。在启动时，PCMCIA 使用第一个检测到的设备来确定哪些内存区域是使用的。`memory_cs` 驱动使用启发式方法猜测卡片的容量。这种启发式方法对于已写入的卡片无效，在其他情况下也可能出错。如果你计划经常使用内存卡，最好将 `/etc/pcmcia/config.opts` 中的窗口限制为已知的良好区域。如果卡片被误识别，则应使用 `dd` 或 `mkfs` 等命令显式指定其大小。`memory_cs` 模块还有一个用于覆盖大小检测的参数。

### 4.7.1 内存设备参数

可以在 `memory.opts` 中指定以下参数：

- `DO_FSTAB`：布尔值 (y/n) 设置：指定是否应为此设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`：布尔值 (y/n) 设置：指定在挂载前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`：布尔值 (y/n) 设置：指定是否在插入卡片时自动挂载此设备。

- `FSTYPE`, `OPTIONS`, `MOUNTPT`：用于 `fstab` 条目和/或挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_FUSER`：卡弹出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备正忙时 `cardctl eject` 将关闭设备。如果 `NO_FUSER` 为 `true`，脚本将不会杀死使用已弹出设备的进程。

以下是一个根据插入插槽自动挂载内存的脚本示例：

```bash
case "$ADDRESS" in
*0,0)
  # 不在 /etc/fstab 中进行更新
  DO_FSTAB="n" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="mem"
  ;;
*1,0)
  # 不在 /etc/fstab 中进行更新
  DO_FSTAB="n" ; DO_FSCK="y" ; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
  MOUNTPT="mem1"
esac
```

## 4.7.2 使用闪存卡

以下信息仅适用于所谓的“线性闪存”内存卡。许多闪存卡（包括 `SmartMedia` 和 `CompactFlash`）实际上包含了模拟 IDE 设备的电路。这些卡片被作为 IDE 设备处理，而不是内存卡。

闪存卡有两种主要格式：FTL（闪存转换层）风格和微软闪文件系统（FFS）。FTL 通常更灵活，因为它允许在闪存卡上像使用普通磁盘设备一样使用任何高级文件系统（`ext2`, `ms-dos` 等）。FFS 是一种完全不同的文件系统。Linux 原生无法处理格式化为 FFS 的卡片。要将内存卡作为普通磁盘设备使用，首先使用 `ftl_format` 命令在设备上创建 FTL。此层隐藏了闪存内存编程的设备细节，并使卡片看起来像简单的块设备。例如：

```bash
ftl_format -i /dev/mem0c0
```

注意，这是通过“原始”内存接口访问卡片。格式化后，可以通过 `ftl_cs` 驱动作为普通块设备访问。例如：

```bash
make2fs /dev/ftl0c0
mount -t ext2 /dev/ftl0c0 /mnt
```
