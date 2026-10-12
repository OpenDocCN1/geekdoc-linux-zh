
```
12:21:58.14
.iso.3.6.1.2.1.1.4.0 = "Neferelle Maxwell"
.iso.3.6.1.2.1.1.5.0 = "remote-gw"
.iso.3.6.1.2.1.1.6.0 = "Remote Sales Office (Florida)"
.iso.3.6.1.2.1.1.7.0 = 78
```

此输出来自对 Cisco 路由器的查询，正如你所见，MIB 对象路径信息在 `iso` 部分之后仅包含数字字符串。`iso` 字符串被包含在输出中，因为 UCD 工具仅知道 MIB 树的起点。对于非标准或厂商特定的 MIB，只能使用数字形式。为了解决此问题，提供了 `-m` 和 `-M` 选项。`-m` 选项指定在 UCD 工具对代理执行任何 SNMP 查询之前应加载的 MIB 模块列表。当列出多个 MIB 模块时，模块必须用冒号 (:) 分隔。MIB 模块只是一个包含代理 MIB 定义的文件。使用 `-m` 选项，我们可以提供正确的 MIB 模块，以便上面的 snmpwalk 输出包含所有字符串名称。`-M` 选项很有帮助，因为我们可以提供搜索 MIB 文件的目录列表。因此命令

```
# snmpwalk -M /var/mibs_cisco-gw1 public system
```

将搜索目录 `/var/mibs_cisco-gw1`。假设它找到了标准 MIB 文件，它将显示以下内容：

```
system.sysDescr.0 = Cisco Internetwork Operating System Software
IOS (tm) 4500 Software (C4500-J-M), Version 11.1(5), RELEASE SOFTWARE (fc1)
Copyright (c) 1986-1996 by cisco Systems, Inc.
Compiled Mon 05-Aug-96 13:17 by mkasron
system.sysObjectID.0 = OID: enterprises.9.1.50
system.sysUpTime.0 = TimeTicks: (99487614) 11 days, 12:21:16.14
system.sysContact.0 = Neferelle Maxwell
system.sysName.0 = remote-gw
system.sysLocation.0 = Remote Sales Office (Florida)
system.sysServices.0 = 78
```

还有一种简写方式来指定所有 MIB 模块（而不是提供列表）——使用 `all` MIB 命令。这会覆盖下一节中讨论的 `MIBS` 环境变量。

## 环境变量

UCD 工具中的每个工具都使用一组小的环境变量，帮助为某些操作参数建立全局值，并为命令行选项提供快捷方式。包括以下内容：

- PREFIX
- MIBS
- MIBDIR
- SUFFIX

PREFIX 变量提供了一种标准方式来定义 MIB 对象标识符的前缀。默认值是

```
iso.org.dod.internet.mgmt.mib-2
```

如果定义了此变量，则在使用 UCD 工具之一时，变量的内容将被添加到所引用 MIB 对象的开头。定义此值将在使用非标准 MIB 的情况下提供帮助。

MIBS 和 MIBDIR 变量提供了一种加载额外 MIB 模块的方式。变量 MIBS 的功能与 `-m` 命令行选项相同。MIBDIR 变量的功能与 `-M` 选项相同。两者都很方便，因为它们适用于所有 UCD 应用程序。

SUFFIX 变量切换 `-s` 命令行选项，该选项显示 MIB 对象路径的后缀或最后一个组件。

## Snmpdelta 工具

**snmpdelta** 命令从 SNMP 代理实体收集 MIB 整数值的变化。此命令监视指定的整数对象并显示随时间发生的对象变化。这对于跟踪网络错误非常有用。例如，可能需要确定从接口丢弃的数据包数量，如 *ifInDiscards* MIB-II 对象。要从名为 remote-gw 的设备监视此对象，可以使用以下命令：

```
# snmpdelta -R remote-gw public ifInDiscards.1
```

调用时，此命令将产生以下输出：

```
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
ifInDiscards.1 /1 sec: 0
```

在没有用户交互的情况下，上述命令会持续轮询代理，直到用户发出 control+c。注意，在我们使用的命令中，`-R` 选项激活对代理 MIB 的随机访问。这使得获取所需 MIB 对象变得容易。较高的丢弃率可能表明接口存在问题。此问题可能是由与布线相关的硬件问题甚至软件配置错误引起的。在上面的示例中，丢弃率没有变化，这就是所有值都为零的原因。此命令支持除先前讨论的常用选项之外的许多附加命令行参数。表 8.4 列出了可用选项。

表 8.4 snmpdelta 命令行选项的附加选项

| 选项 | 描述 |
|---|---|
| `-f` | 读取配置文件 |
| `-k` | 在输出中显示时间信息 |
| `-l` | 将配置写入文件 |
| `-m` | 显示已检索到的最大值 |
| `-p` | 指定轮询周期 |
| `-P` | 指定报告周期为轮询请求的次数 |
| `-s` | 显示时间戳信息 |
| `-S` | 将数据记录到日志文件 |
| `-t` | 确定时间间隔 |
| `-T` | 生成表格输出 |

使用 `-m` 选项，**snmpdelta** 将显示正在轮询的 MIB 对象获得的最大值。它显示每次轮询的值，并在收到新的高值时将其包含在 `Max` 列中。命令

```
# snmpdelta -R remote-gw public -m ifOutOctets.2
```

产生以下输出：

```
ifOutOctets.2 /1 sec: 25784 (Max: 25784)
ifOutOctets.2 /1 sec: 21287 (Max: 25784)
ifOutOctets.2 /1 sec: 2743 (Max: 25784)
ifOutOctets.2 /1 sec: 8611 (Max: 25784)
ifOutOctets.2 /1 sec: 4473 (Max: 25784)
ifOutOctets.2 /1 sec: 10939 (Max: 25784)
ifOutOctets.2 /1 sec: 1882 (Max: 25784)
ifOutOctets.2 /1 sec: 9258 (Max: 25784)
ifOutOctets.2 /1 sec: 22751 (Max: 25784)
ifOutOctets.2 /1 sec: 28615 (Max: 28615)
ifOutOctets.2 /1 sec: 18599 (Max: 28615)
ifOutOctets.2 /1 sec: 28459 (Max: 28615)
ifOutOctets.2 /1 sec: 2662 (Max: 28615)
```

请注意，当获得新的最大值时，`Max` 列会相应更新。

在监视大量 MIB 对象或数据时，将信息保存到日志文件可能会有所帮助。`-l` 选项以以下格式将数据保存到文件中：

```
(device) - (MIB object)
```

因此，命令

```
# snmpdelta -R monet public -l ifOutOctets.12
```

将记录 `ifOutOctets` 增量到名为 `monet-ifOut-Octets.2` 的文件中。

检查此文件将显示与通常显示的相同格式和数据。

如果需要以更结构化的格式显示 **snmpdelta** 的输出，请使用 `-T` 选项。例如，如果需要监视多个 MIB 对象并将数据添加到电子表格或其他程序中，**snmpdelta** 可以以表格格式显示输出：

```
snmpdelta -R remote-gw public -T ifInDiscards.1 ifInDiscards.2:
```

![](img/f265c9d1f2610aca197c430cbfcd51f5_456_0.png)

输出是两个接口丢弃的数据包数量的显示，以列格式呈现。

## Snmpget 工具

**snmpget** 命令从 SNMP 代理实体检索信息。它使用 SNMP get-request 并将一个或多个 MIB 对象名称作为参数，并返回其关联值。如果发生错误，将显示描述性消息以帮助确定问题。如果在命令行上指定了对象列表，则只返回包含在代理 MIB 中的那些对象。

命令语法如下：

```
 snmpget [<common arguments>] MIB-object [MIB-object]
```

要从 Cisco 路由器检索 MIB 对象 sysDescr 和 sysContact，可以使用以下命令：

```
 # snmpget remote-gw public system.sysDescr.0 system.sysUpTime.0
```

根据路由器型号和配置，此命令将显示如下输出：

```
system.sysDescr.0 = Cisco Internetwork Operating System Software
IOS (c) 3000 Software (I6S-1NR-L), Version 11.0(17), RELEASE
SOFTWARE (fc1) Copyright (c) 1986-1997 by cisco Systems, Inc.
Compiled Thu 04-Sep-97 14:17 by richu
system.sysUpTime.0 = TimeTicks: (134381144) 15 days, 13:16:51.44
```

请注意，Cisco 路由器包含一个相当长的 sysDescr 字符串。这在尝试识别互联网操作系统型号和当前版本时非常有用
