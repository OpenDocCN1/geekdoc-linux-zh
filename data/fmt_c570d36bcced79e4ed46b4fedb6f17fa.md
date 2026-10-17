
虽然 `MRTG` 设计为成对监控事物，但你可以通过两次列出同一个 `MIB` 来监控单个 `MIB`：

```
Target[localhost.memAvail]:.1.3.6.1.4.2021.4.6.0.1.3.6.1.4.2021.4.6.0:GetNext@localhost
```

这将仅在 `MRTG` 图表上显示一个 `MIB`。

注意：为目标选择一个单独的标签（`label`），并将其用于该目标的所有配置语句。如果不这样做，`MRTG` 要么报错，要么覆盖来自其他目标的日志文件。

## 自定义 MRTG

一旦你有了可以运行的 `MRTG` 设置，请小心测试新配置。我通常在单独的工作目录（`WorkDir`）中测试新的 `MRTG` 配置，这样任何错误配置都不会损坏现有日志。

`mrg.cfg` 文件包含各种选项，允许自定义几乎每个方面。

### WithPeak[label]:my

`MRTG` 的 `WithPeak` 选项可以设置最大值。

### MaxBytes[label]:number

可以到达的最大值。`MRTG` 使用它来判断是否合理。

### YLegend[label]:text

`MRTG` 将此内容放在图表的侧边。在这里测量的内容。

### Legend1[label] & Legend2[label]:text

`Legend1` 是你测量的第一个 `MIB`，`2` 是第二个。它们将出现在图表底部。

### Legend1[label] & Legend2[label]:text

`Legend1` 是你测量的第一个 `MIB`，`2` 是第二个。

### Legend3[label] & Legend4[label]:text

这些标签将在记录最大值时使用。如果不记录最大值，这些标签将无效。

### Directory[label]:directoryname

大型 `MRTG` 设置会产生大量文件。`directory` 允许你将文件放在 `WorkDir` 的特定子目录下。

### Options[label]:option-names

`Options` 允许你处理特殊情况。所有选项都写在目标后面的。

- `growright`: 默认情况下，`MRTG` 从右侧绘图。使用此选项让它从右侧绘制。
- `bits`: 这将图表从字节转换为比特。比特不仅令人印象深刻，取决于你的测量还可能更准确。
- `gauge`: `SNMP` 通常以计数器格式保留信息。对于不变化的 `MIB` 使用 `gauge`。
- `unknzero`: 当目标由于任何原因（包括电源故障或网络问题）无法访问时，系统将使用最后一个已知值。此选项导致 `MRTG` 在无法访问目标时假设值为 0。

`Legend0[myhost.AbsoluteBSD.com.cpu]`: 系统 `CPU`
`Legend1[myhost.AbsoluteBSD.com.cpu]`: 用户处理器使用率
`Legend2[myhost.AbsoluteBSD.com.cpu]`: 系统处理器使用率
`Legend3[myhost.AbsoluteBSD.com.cpu]`: 5 分钟最大用户使用率
`Legend4[myhost.AbsoluteBSD.com.cpu]`: 5 分钟最大处理器使用率

`Options[myhost.AbsoluteBSD.com.cpu]`: `growright`, `gauge`

`PageTop[myhost.AbsoluteBSD.com.cpu]`: `<H1>myhost.AbsoluteBSD.com 的 CPU 使用情况</H1>`

# 交换空间使用

在测量交换空间（`swap` `space`）之前，你需要知道系统有多少交换空间。你可以通过执行 `snmpwalk` 获取总交换空间，或者执行 `snmpwalk hostname community .1.3.6.1.4.1.2021.4` 来获取该信息。将该值填入 `MaxBytes` 空间，它就会显示在 `PageTop` 下方的你的页面上。

```
Title[myhost.AbsoluteBSD.com]: myhost.AbsoluteBSD.com 可用交换空间
YLegend[myhost.AbsoluteBSD.com]: swap
WithPeak[myhost.AbsoluteBSD.com]: wmy
MaxBytes[myhost.AbsoluteBSD.com]: 128000
Target[myhost.AbsoluteBSD.com]: swap
1.3.6.1.4.1.2021.4.4.0:public@myhost.AbsoluteBSD.com
ShortLegend[myhost.AbsoluteBSD.com]: swap
Legend1[myhost.AbsoluteBSD.com]: 可用交换空间
Legend0[myhost.AbsoluteBSD.com]: 可用交换空间
Legend[myhost.AbsoluteBSD.com]: 可用交换空间
Legend2[myhost.AbsoluteBSD.com]: 可用交换空间
Legend3[myhost.AbsoluteBSD.com]: 5 分钟最大可用用交换空间
Legend4[myhost.AbsoluteBSD.com]: 5 分钟最大可用交换空间
Options[myhost.AbsoluteBSD.com]: growright, gauge
PageTop[myhost.AbsoluteBSD.com.swamp]: <H1>myhost.AbsoluteBSD.com 的可用交换空间（总共 128M）</H1>
```

# 磁盘分区

测量磁盘分区上使用空间的方法也类似，你需要知道磁盘分区的 `MIB`（参见本章前面“索引数字”中的示例）。请确保在 `PageTop` 空间中获取了正确的大小。

```
Target[myhost.AbsoluteBSD.com.root]: .1.3.6.1.4.1.2021.9.9.1&1.3.6.1.4.1.2021.9.1.9:public@myhost.AbsoluteBSD.com
Title[myhost.AbsoluteBSD.com.root]: Myhost.AbsoluteBSD.Com root 分区使用 %
MaxBytes[myhost.AbsoluteBSD.com.root]: 100
WithPeak[myhost.AbsoluteBSD.com.root]: wmy
Suppress[myhost.AbsoluteBSD.com.root]: y
Legend1[myhost.AbsoluteBSD.com.root]: % 使用率
Legend0[myhost.AbsoluteBSD.com.root]: % 使用率
YLegend[myhost.AbsoluteBSD.com.root]: 使用百分比
ShortLegend[myhost.AbsoluteBSD.com.root]: 已使用
Options[myhost.AbsoluteBSD.com.root]: gauge, growright
PageTop[myhost.AbsoluteBSD.com.root]: <H1>myhost root 分区（总共 128M）已使用</H1>
```

# 网络流量

为了完整起见，让我们来看一个如何测量网络流量的示例。这假设网络连接为 `10Mbps`；如果你使用的是 `100BaseT`，请将 `MaxBytes` 乘以 10。

```
Title[myhost.AbsoluteBSD.com.traffic]: myhost.AbsoluteBSD.com 网络流量
MaxBytes[myhost.AbsoluteBSD.com.traffic]: 125000
WithPeak[myhost.AbsoluteBSD.com.traffic]: wmy
Target[myhost.AbsoluteBSD.com.traffic]: public@myhost.AbsoluteBSD.com
Options[myhost.AbsoluteBSD.com.traffic]: growright, bits
PageTop[myhost.AbsoluteBSD.com.traffic]: <H1>myhost.AbsoluteBSD.com 的网络流量</H1>
```

# 监控非 BSD 系统

`MRTG` 可以监控任何使用 `SNMP` 的系统；`SNMP` 是几乎每个网络设备和操作系统厂商都遵循的标准。要做到这一点，你需要该产品支持的 `MIB` 列表及其含义。`MIB` 解释表（包含如何读取 `MIB` 树的简单文本文件）通常可以从供应商那里获得。每个文件的开头如下：

```
IPV-6-MIB DEFINITIONS ::= BEGIN

IMPORTS
MODULE-IDENTITY, OBJECT-TYPE, NOTIFICATION-TYPE,
mib-2, Counter32, Unsigned, Integer32,
Gauge32 FROM SNMPv2-SMI
DisplayString, Address, TrueValue, Timestamp,
VariablePointer, RowPointer FROM SNMPv2-TC
MODULE-COMPLIANCE, OBJECT-GROUP,
NOTIFICATION-GROUP FROM SNMPv2-CONF
IPv6Index, Ipv6address, Ipv6AddressPrefix,
IPv6AddressIdentifier FROM SNMPv6-TC;
IPv6IndexOrZero
```

将这些定义文件复制到系统上的一个目录。接下来，设置环境变量 `MIBDIRS` 指向该目录，`snmp` 就会识别它们。

# 第 20 章：系统崩溃与崩溃（Crashes and Panics）

当系统发生崩溃（`panic`）时，它会停止运行。与其通常的控制台消息相比，控制台会显示如下内容：

```
系统崩溃（panic）

致命异常 12：在内核 模式下发生页错误

故障虚拟地址 = 0x080c00153a

错误代码 / 监管模式，页不存在
```

由于 `FreeBSD` 的一个用处是它的可靠性，但一旦它崩溃，它就会进入死机状态。

## 什么会导致崩溃（Panics）？

当系统发生崩溃（`panic`）时，它会停止运行。与其通常的控制台消息相比，控制台会显示如下内容：

```
系统崩溃（panic）

致命异常 12：在内核 模式下发生页错误

故障虚拟地址 = 0x080c00153a

错误代码 / 监管模式，页不存在
```

由于 `FreeBSD` 的一个用处是它的可靠性，但一旦它崩溃，它就会进入死机状态。

## 响应崩溃（Panic）

如果你收到一个类似的错误消息，由于 `FreeBSD` 的一个用处是它的可靠性，但一旦它崩溃，它就会进入死机状态。

## 崩溃（Panic）看起来像什么样？

当系统发生崩溃（`panic`）时，它会停止运行。与其通常的控制台消息相比，控制台会显示如下内容：

```
致命异常 12：在内核 模式下发生页错误

故障虚拟地址 = 0x080c00153a

错误代码 / 监管模式，页不存在

指令指针 = 0x08:0xc15aa84

栈指针 = 0x10:0c37e7c

帧指针 = 0x10:0c37e80

代码段 =
base 0x0, limit 0xffff, type 0x1b
DPL 0, pres 1, def 1, gran 1
中断启用, 恢复, IOPL=0
5 (syncer)
处理器标志 =
当前进程 =
中断掩码 =
bio
异常数量 =
12
panic: page fault
```

如果你是一个意外的系统管理员，这样的消息可能会让你心惊胆战，但别担心。`FreeBSD` 提供了一些友好的消息描述了问题所在，提供了一个开始查找的具体位置，或者至少可以搜索。我见过有些崩溃提供了非常具体的指令，说明应该设置哪些内核选项以防止再次发生。其他崩溃消息，像这种，要更令人困惑。

在这次崩溃消息中，唯一看起来熟悉的词是倒数第四行，我们看到当前进程被称为“`syncer`”。大多数人不知道 `syncer` 是什么，而那些认识它的人也比修复它要懂得多。“神秘崩溃”是 `FreeBSD` 中最糟糕的情况之一。

内核崩溃（`panic`）可能会发生。请在安装服务器时对其进行配置。这样，一旦发生崩溃，你将自动获得回溯信息（`backtrack`）。这听起来可能是一个新颖的想法，而且 `FreeBSD` 文档中确实没有强调这一点，但为灾难做好准备是有意义的。如果它从未发生，你也就无可抱怨了。如果你遇到了 `panic`，你已经准备就绪，能够在问题出现时为 `FreeBSD` 的人员提供完整的调试转储（`dump`）。

## 前提条件

为了给内核崩溃做好准备，你需要安装源代码。你还需要一个（或多个）交换分区（`swap` `partitions`），其大小至少比你的物理内存大 `1MB`，最好是你 `RAM` 的两倍。如果你有 `512MB` 的 `RAM`，你需要一个 `513MB` 或更大的交换分区，以 `1024MB` 为佳。（在服务器上，你应该在多个驱动器上设置多个交换分区！）如果你的交换分区不够大，你将不得不添加另一个具有足够交换分区的硬盘，或者重新安装。（虽然拥有一个有可用空间的 `/var` 分区很有帮助，但这是必要的。）

如果你遵循了书开头的安装建议，那么你就一切就绪了。

## 崩溃转储过程

内核崩溃捕获过程的工作原理大致如下：如果一个配置适当的系统崩溃，它将保存系统内存的内核转储（`core` `dump`）。你无法将其保存到文件，因为崩溃的内核不知道文件；它只知道分区。写入此转储的最简单位置是交换分区，转储被放置在尽可能靠近交换分区的末尾。一旦内核保存了核心数据，它就会重启计算机。

在重启期间，`/etc/rc` 会启用交换分区。然后它（可能）会对崩溃的磁盘运行 `fsck`。它必须在运行 `fsck` 之前启用交换功能，因为 `fsck` 可能需要使用交换空间。希望你有足够的交换空间，以便 `fsck` 能够完成所有操作，而不会覆盖潜伏在你交换分区中的转储文件。

一旦系统有了一个可以保存核心转储的地方，它就会检查交换分区是否有转储。一旦发现核心转储，`savecore` 会将转储从交换分区复制到适当的文件中，清除交换分区中的转储并让重启继续。你可以利用它来获取回溯轨迹（`backtrace`）。

## 调试内核

标准的 `FreeBSD` 内核在安装之前会移除内核中所有的调试信息，包括符号（`symbols`），符号提供了机器码和源代码之间的映射。这种映射表可能比实际程序还要大，没有人想要一个运行体积比实际需要大三倍的内核！然而，我们需要这种映射以及其他调试信息来诊断崩溃中发生了什么错误。

该映射还包含一份完整的源码行号列表，因此开发者可以确切地知道问题发生在哪里。没有这些信息，开发者将陷入手动将内核映射到源码的困境，这就像在没有图片的情况下尝试组装一个百万拼图，甚至不知道你是否拥有了所有的碎片。总的来说，这是一项糟糕的工作。当你考虑到需要做这项工作的开发者是一个志愿者时，这变得更糟糕了。这就是为什么你的调试内核应该包含它的符号。

为了保留符号，请在你的内核配置中添加以下几行：

```
options DDB
makeoptions DEBUG=-g
```

`DDB` 选项会安装 `DDB` 调试器。（这并不是绝对必要的，但它可以很有帮助，而且不占用多少空间。）你在这里设置的 `makeoptions` 告诉系统构建调试内核。

## Panic 后的行为

在配置系统时，你需要决定你希望系统在 `panic` 之后如何表现。你是希望计算机自动重启，还是希望它停留在 `panic` 界面，直到你手动触发重启？如果系统位于远程位置，你几乎肯定希望计算机自动重启，但如果你在控制台调试内核更改，你可能希望它等待你的指令。

要实现自动重启，请包含内核选项 `DDB_UNATTENDED`：

```
options DDB_UNATTENDED
```

如果你不包含此选项，系统将等待你告诉它进行重启。

## kernel.debug

一旦你按照自己想要配置了内核，你会在内核编译目录中找到一个名为 `kernel.debug` 的文件。这是带有符号的内核；请将其保存到某处。下次你升级系统或自定义内核时，这个调试内核会被新的调试内核覆盖。如果你为了测试构建了自定义内核，你想要确保你的那个已知的、良好的调试内核是可用的。
