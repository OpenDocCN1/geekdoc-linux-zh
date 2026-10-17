
如果中断探测工作不正常，插槽驱动程序可能会为插入操作分配中断，即使中断极其稀缺以至于这样做并不理想。你可以通过将`PCI_OPTS`设置为`"poll_interval=100"`将控制器切换到轮询模式。或者，如果你有一个`CardBus`控制器和旧版本的`PCMCIA`驱动程序，使用`"pci_cse=1"`选择一个`PCI`中断（如果可用）用于卡状态变化。

在某些情况下，内核配置错误也会导致表面的中断短缺。在 2.4 及更新后的内核中，如果没有启用`CONFIG_ISA`，那么`PCMCIA`总线中断是可用的。

IO 端口共享并不常见见，但有时发生在需要大对齐 IO 端口空间区域的卡上，或者可能只能识别少数特定的 IO 端口位置。`/etc/pcmia/config.opts`中的默认 IO 端口范围通常是足够的，但可以扩展。如果这是问题所在，可以在`config.opts`中使用`include 0x1000-0x1fff`行。在少数情况下，饥饿可能表示 IO 探测失败（参见 3.4 IO 端口失败）。

在`config.opts`的默认内存窗口中，内存饥饿也不常见见。`CardBus`卡可能比典型的 16 位卡需要更大的内存区域。由于`CardBus`内存窗口可以映射到主机的`PCI`地址空间的任何位置（而不仅仅是`PC`系统中 640K-1MB 的“空洞”），在高内存中指定大型内存窗口（例如`0xa0000000-0xa0fffff`）是有帮助的。

### 3.9 仅在插入两个卡时发生资源冲突

症状：

- 两张卡在单独使用时均工作正常。

- 当两张卡都插入时，只有一张工作。

这通常表示与`Linux`不知道的系统设备存在资源冲突。`PCMCIA`设备是动态配置的，例如，中断是按需分配的而不是而不是分配给特定的卡或插槽。给定一个可用资源列表，卡按照它们配置的顺序分配资源。在这种情况下，最后被分配到资源的卡的资源实际上并不是空闲的。

检查系统日志以查看未工作的卡使用了哪些资源。从`/etc/pcmia/config.opts`中排除这些资源，并重启`configmgr`守护进程以重新加载资源数据库。

### 3.10 设备配置未完成

症状：

- 当插入卡时，恰好听到一声高音蜂鸣声。

- 后续的卡插入可能会被忽略。

这表明卡已被识别，但`cardmgr`无法完成配置。最可能的原因是设置脚本阻塞了。要确定问题，你可以手动运行设置脚本以查看阻塞在何处。`cardmgr`守护进程还显示网络状态。例如，网络命令的输出可能如下：

```
poll_interval=100
```

# 4. 使用与功能

## 4.1 配置工具

当插入卡时，恰好听到一声高音蜂鸣声。后续的卡插入可能会被忽略。这表明卡已被识别，但`cardmgr`无法完成配置。最可能的原因是设置脚本阻塞了。要确定问题，你可以手动运行设置脚本以查看阻塞在何处。`cardmgr`守护进程还显示网络状态。例如，网络命令的输出可能如下：

```
poll_interval=100
```

| 模块 | 大小 | 使用者 |
| :--- | :--- | :--- |
| i82365 | 2 | |
| linksYS | 2 | |
| pcmia_core | 3 | |

### 4.1.1 卡状态守护进程

`cardmgr`守护进程负责监控`PCMCIA`插槽、加载驱动程序以及响应卡变化的运行脚本。它还显示系统日志中的状态。高蜂鸣表示成功，低蜂鸣表示卡未识别。更多信息请参见手册页。

### 4.1.2 stab 文件

`cardmgr`在`/var/lib/pcmia/stab`中记录每个插槽的设备信息。这是一个示例列表：

| 插槽 | 类 | 驱动程序 | 名称 | 主/次号 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | scsi | Adapatec-1460 | sda | 8 |
| 0 | scsi | aha152 | scd0 | 11 |
| 1 | serial | ttyS1 | | |

对于描述设备的行，第一行是插槽，第二行是设备类，第三行是设备驱动程序，第四行是具有相同驱动程序的多个设备，第五行是设备名称，最后两个是设备的主次号（如果适用）。

`CardBus`卡的热插拔`PCI`驱动程序不由`cardmgr`管理；它们由热插拔内核管理。有关此信息请参见`http://linux-hotplug.sourceforge.net`。当`cardmgr`看到由`PCI`驱动的卡时，它将忽略该卡。插入或弹出卡时会报警，但在系统日志和`stab`文件中仅会被识别为“`CardBus`热插拔设备”。

### 4.1.3 cardctl 和 cardinfo 工具

`cardctl`命令可检查插槽状态或查看其如何配置。它也用于更改卡的配置状态。以下是`cardctl config`命令输出的示例：

```
Socket 0:
not configured
Socket 1:
Vcc = 5.0, Vpp1 = 0.0, Vpp2 = 0.0
Card type is memory and I/O
IRQ 3 is dynamic shared, level mode, enabled
Speaker output is enabled
Function 0:
Config register base = 0x0800
Option = 0x063, status = 0x008
I/O window 1: 0x0280 to 0x2bf, auto sized
I/O window 2: 0x02f8 to 0x2ff, 8 bit
```

或者使用`cardctl ident`获取识别信息：

```
Socket 0:
no product info available
Socket 1:
product info: "LINKSYS", "PCMLM336", "A", "0040052d6400"
manif: 0x0143, 0x0cab
function: 0 (multifunction)
```

# 4. 使用特性

`"cardctl suspend"`和`"cardctl resume"`命令用于在不加载驱动程序的情况下关闭卡设备。`"cardctl reset"`命令尝试重置并配置卡设备。`"cardctl insert"`和`"cardctl eject"`模拟物理插入或拔出卡片时执行的操作，包括加载或卸载驱动程序，以及配置或关闭设备。

如果你正在运行`X`，`cardinfo`工具除了`"cardctl config"`外，还提供了显示`PCMCIA`插槽当前状态的图形化显示。它还提供了一个监控`cardctl`功能的图形界面。

## 4.1. 插入和拔出卡片

理论上讲，你可以随时插入和移除`PCMCIA`卡。然而，不拔出当前正被应用程序使用的卡片是一个好习惯。比 1.1.77 旧的内核在串口串口/现代卡片时会死锁，但这个问题现在应该已经修复了。

某些类型的卡片无法安全地进行热拔出。具体而言，`ATA/IDE`和`SCSI`接口卡不是热插拔安全的。这不太可能实现，因为完整的解决方案需要对`Linux`内核驱动模型进行重大更改。此外，通常不建议热拔出任何类型的`CardBus`驱动程序。这正在针对各种卡类型（`IDE`, `SCSI`, `CardBus`）逐步改进，建议在物理拔出之前使用`"cardctl eject"`。

### 4.1.5 卡片服务与高级电源管理

如果你在配置内核时启用了`APM`支持，则可以在编译`Card Services`时带有`APM`（高级电源管理）。`APM`内核驱动由 Stephen Rothwell (`Stephen.Rothwell@ann.aug.org.au`) 维护。`apmd`守护进程由 Avery Pennurun (`apennarr@worldvisions.ca`) 维护，更多信息请参阅`http://www.worldvisions.ca/apennarr/apmd/`。如果在系统上检测到兼容版本，`PCMCIA`模块将自动配置`APM`。

无论是否配置了`APM`，你可以在笔记本电脑睡眠前使用`"cardctl suspend"`，并在恢复后使用`"cardctl resume"`，从而干净地关闭和恢复你的`PCMCIA`卡。这对于正在使用的调制调器无效，因为串口驱动程序无法保存和恢复现代操作参数。

`APM`在某些系统上似乎不稳定。如果你在系统上遇到`APM`和`PCMCIA`的问题，请尝试缩小范围，确定是哪一个包报告了错误。

某些驱动程序（`PCMCIA SCSI`驱动程序）无法从挂起/恢复周期恢复。使用`PCMCIA SCSI`卡时，请务必在系统睡眠之前使用`"cardctl eject"`。

### 4.1.6 关闭 PCMCIA 系统

要卸载整个`PCMCIA`包，请调用`rc.pcmcia`：

```
/etc/rc/rc.pcmcia stop
```

此脚本将运行几秒钟，为所有卡驱动程序留出优雅关闭的时间。如果设备当前正在使用，关闭将不完整，某些内核模块可能不会加载。
