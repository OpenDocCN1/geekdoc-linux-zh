
```
IMPORTS
MODULE-IDENTITY, OBJECT-TYPE, Counter32, Gauge32, Counter64,
Integer32, TimeTicks, mib-2,
NOTIFICATION-TYPE FROM SNMPv2-SMI
TEXTUAL-CONVENTION, DisplayString,
PhysAddress, TrueValue, RowStatus,
Timestamp, AutonomousType, TestAndcr FROM SNMPv2-TC
MODULE-COMPLIANCE, OBJECT-GROUP,
NOTIFICATION-GROUP FROM SNMPv2-CONF
snmpTraps FROM SNMPv2-MIB
IAIFype FROM IAIFype-MIB;
```

然后是模块的定义。

```
ifMIB MODULE-IDENTITY
LAST-UPDATED "200006140000Z"
ORGANIZATION "IETF Interfaces MIB Working Group"
CONTACT-INFO
+ - Keith McCloghrie
Cisco Systems, Inc.
170 West Tasman Drive
San Jose, CA 95134-1706
US
408-526-5260
kzm@cisco.com

DESCRIPTION
"用于描述网络接口子层通用对象的 MIB 模块。此 MIB 是 MIB-II 中 ifftable 的更新版本，并包含了 RFC 1229 中定义的扩展。"

REVISION
"2000061400000Z"
DESCRIPTION
"Interfaces MIB WG 同意的澄清说明，并发布在 RFC 2863 中。"

REVISION
"1996022821552Z"
DESCRIPTION
"Interfaces MIB WG 进行的修订，并发布在 RFC 2233 中。"

REVISION
"1993110821552Z"
DESCRIPTION
"初始修订，作为 RFC 1573 的一部分发布。"
::={ mib-2 31 }
```

该模块定义了 `ifMIB`，它在整个 MIB 地址空间中占据 `{ mib-2 31 }` 位置。组织和联系信息可以清晰识别，随后是按时间倒序排列的该 MIB 之前版本的描述。时间和和日期看起来非常神秘，但它们只是 GMT 时间下年、月、日和分钟的拼接（由 `Z` 表示格威治时间）。因此，最近的修订（`2000061400000Z`）是在 2000 年 6 月 14 日完成的。

接下来，你将看到 MIB 对象实际结构的定义，以及任何此 MIB 新增的文本约定。

# 总结

这是一场关于 SNMP 的旋风式之旅。我们已经涵盖了 SNMP 的基本部分：协议、语法和第一组受管理对象。你现在应该理解 `SMI`、`MIB` 和 `OID` 这些缩写，以及 `object`（对象）和 `trap`（陷阱）等术语。你还应该熟悉 `MIB-2` 术语并对其内容有一个大致了解。我们讨论了各种数据类型，包括标量和表格。到此时，你应该能够获取一个陌生的 MIB 并阅读它，理解它的基本结构以及它试图描述的内容。我们还提到了你可能发现用于探测启用 SNMP 设备的两个命令行工具：`snmpwalk` 和 `snmpget`。

通过简单的剪贴和一些明智的修改，你可能开发出一个简单的 MIB。

# 安装帧缓冲区设备驱动

Laddie CD 设计旨在用于尽可能多的视频卡。为了实现这一点，它默认使用一种广泛采用的视频标准的帧缓冲区驱动程序，并为仅 8 位的低分辨率显示进行配置。

在附录中，我们将涵盖以下主题：

- 查找帧缓冲区设备驱动
- 配置帧缓冲区

## 查找视频卡的帧缓冲区驱动

要查找视频卡的可用驱动程序，使用 Laddie CD 启动。如果 Laddie CD 成功找到视频卡的驱动程序，它将启动帧缓冲区，如图 C 所示。否则，它将显示消息：

![](img/ab18faa434b6e10df0a92984bf70fc_348_0.png) C

目前，我们假设帧缓冲区不可用。退出帧缓冲区 UI，并输入：

内核产生的消息显示：

```
```

### VESA 驱动

Laddie CD 支持由视频标准协会（VESA）开发的接口。这意味着驱动必须在启动时进行配置。以下是我们一个系统的示例输出：

```
vga0: VGA compatible
```

### 硬件特定驱动

如果 Laddie CD 没有找到你显卡的驱动程序，较新的内核可能会支持它。在这种情况下，使用 `lspci` 命令识别你的显卡。如果你的显卡是 AGP、PCI 或 PCI-Express，它会报告出来。运行 `lspci` 命令产生的输出行之一是：

```
01:00.0 VGA compatible controller: nvidia Corporation NV15 [GeForce 2 GTS/Pro] (rev a4)
```

### 未包含在 Laddie CD 中

如果 Laddie CD 没有找到你显卡的驱动程序，较新的内核可能会支持它。在这种情况下，使用 `lspci` 命令识别你的显卡。如果你的显卡是 AGP、PCI 或 PCI-Express，它会报告出来。运行 `lspci` 命令产生的输出行之一是：

```
01:00.0 VGA compatible controller: nvidia Corporation NV15 [GeForce 2 GTS/Pro] (rev a4)
```

## 配置帧缓冲区设备驱动

一旦你为硬件找到了合适的视频驱动程序，你就需要为所需的视频模式对其进行配置。

### vesafb 驱动程序

由于 `vesafb` 驱动依赖实模式 BIOS 函数进行初始化，因此它必须被编译到内核中并在启动时进行配置。此配置在内核命令行中指定，并可以在启动提示符处或引导程序的配置文件中提供。对于 `vesafb` 驱动，内核命令行应包含以下内容：

```
video=vesafb vga=<linux video mode>
```

Linux 视频模式是一个指定特定分辨率和像素位数的数字。该数字通过向 VESA BIOS 扩展指定的视频模式数字加上 `0x200` 生成。Linux 视频模式总结在表 C-1 中。

表 C-1：Linux 视频模式数字
| 像素位数 | 320x200 | 640x400 | 640x480 | 800x600 | 1024x768 | 1280x1024 |
|---|---|---|---|---|---|---|
| 4 | | | | 0x302 | 0x304 | 0x306 |
| 8 | | | 0x300 | 0x301 | 0x303 | 0x305 | 0x307 |
| 15 (5:5:5) | 0x30d | | 0x310 | 0x313 | 0x316 | 0x319 |
| 16 (5:6:6) | 0x30e | | 0x311 | 0x314 | 0x317 | 0x31a |
| 24 (8:8:8) | 0x30f | | 0x312 | 0x315 | 0x318 | 0x31b |

### 选择合适的视频模式

典型的符合 VBE 标准的显卡不会支持所有模式，你可能需要实验来找到一个可用的。最简单的方法是在 Linux 启动提示符处指定

```
video=vesafb vga=ask
```

（如果你正在使用 Laddie CD 进行实验，完整的启动提示符行将 `linux vga=ask`。）内核初始化将显示模式列表并要求输入数字。你可以忽略它呈现的模式，因为这些是用于纯文本控制台的。

此外，不要选择 `scan` 选项。最好的情况下，这将提供更长的模式列表；最坏的情况下，它会导致系统挂起，你必须重启。事实上，每当你输入不支持的模式时，内核会立即响应 `Unknown mode ID`。重试即可，找到可用的模式并不困难。在输入模式时，只需提供数字而不需要十六进制前缀 `0x`。

### 更新内核命令行

一旦你找到了一个可用的 VBE 视频模式，就可以更新引导程序配置文件中的内核命令行。在这种情况下，你确实需要使用前缀 `0x`。例如，命令

```
video=vesafb vga=0x311 3
```
