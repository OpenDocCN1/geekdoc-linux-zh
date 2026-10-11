
第一个包显示 `jaguar` 发关于 `cs.colorado.edu` `xor.com` 的 DNS 查询请求。响应是该名称作为别名的机器真实名称，即 `mroe.cs.colorado.edu`。第三个包是对 `mroe` IP 地址的反向查找，第四个包包含了预期的响应。

### Ethereal: 可视化嗅探器
如果你更倾向于使用点击式程序进行数据包嗅探，那么 `Ethereal` 可能适合你。`Ethereal` 根据 `www.ethereal.com` 的公共许可提供，是一个基于 `GTK+` (GIMP 工具包) 的 GUI 嗅探器，其功能比大多数商业嗅探产品都要多。你可以在 Linux 桌面上运行它，或者如果你的笔记本电脑在 Windows 的黑暗时代痛苦地挣扎，你可以下载该版本的二进制文件。

`tcpdump` 的 `man` 页包含几个高级过滤的示例，以及原语的完整列表。

- `tcpdump`
- `NAI's Sniffer™`
- `Sniffer™ Pro`
- `NetXray™`
- `snoop`
- `Shimomi Surveyor`
- `Microsoft's Network Monitor`
- `Novell's LANAnalyzer`
- `Cisco Secure IDS idpos`

除了嗅探数据包外，`Ethereal` 还有一些让它变得格外顺手的功能。一个很棒的功能是 `Ethereal` 可以读取和写入许多其他数据包跟踪格式，包括但不限于：

第二个额外方便的功能是，你可以点击 TCP 流中的一个包，并要求 `Ethereal` “重组”（拼接）流中所有数据包的有效负载数据。如果你想检查整个 TCP 对话期间传输的数据（例如跨越网络携带电子邮件消息的连接），此功能非常有用。

## 20.6 网络管理协议

在过去的十年中，网络在规模和价值上都迅速增长，随着这种增长，对有效管理网络的需求也随之而来。商业

你可以使用 `tcpflow` 工具在命令行中从 `tcpdump` 跟踪文件中实现类似的壮举。

![](img/4baff4a9)

## 20.7 SNMP：简单网络管理协议

当 `SNMP` 在 20 世纪 90 年代初首次广泛使用时，引发了一场小型金热。数百公司推出了 `SNMP` 管理包。此外，许多硬件和软件供应商会将 `SNMP` 代理作为其产品的一部分发布。

在我们深入研究 `SNMP` 的细节之前，我们应该注意到，与它相关的术语是网络领域中发现的最糟糕的技术术语之一。`SNMP` 概念和对象的标准名称会主动地误导你对所发生情况的理解。造成这种局面的人应该被砸碎键盘。

### SNMP 组织

`SNMP` 数据按照标准化的层次结构排列。这种强制性的组织使得数据在理论上既具有通用性又具有扩展性。大部分部分被留作未来扩展，而特定厂商的添加内容则被本地化以防止冲突。命名层次结构由“信息库”（`MIB`）组成，这些是结构化的文本文件，描述了可以通过 `SNMP` 访问的数据。`MIB` 包含数据变量的描述，这些变量通过称为对象标识符（`OID`）进行引用。

翻译成英文，这意味着 `SNMP` 定义了一个层次化的值命名空间，其值与系统的“有趣”参数相关联。

一个 `SNMP` 变量可以包含的基本数据类型有整数、字符串和空。这些可以组合成基本类型的序列，并且序列可以反复实例化以形成表格。大多数实现都支持各种其他数据类型，如

`SNMP` 层次结构非常类似于文件系统。使用点作为分隔符，每个节点都被赋予一个数字而不是名称。按照惯例，节点也被赋予了文本名称以备参考，但这种命名实际上只是高层的便利性，而不是层次结构的特征（就像主机名到 IP 地址的映射一样简单）。

例如，引用系统运行时间的 `OID` 是 `1.3.6.1.2.1.1.3`。这个 `OID` 也有一个人类可读的名称：

- `iso.org.dod.internet.mgmt.mib-2.system.sysUpTime`

`SNMP` 的顶层是政治产物，通常不包含有用数据。事实上，目前有用数据只能在 `OID` `iso.org.dod.internet.mgmt` 之下找到（数值上为 `1.3.6.1..`）

用于 `TCP/IP` 的基础 `SNMP MIB` (`MIB-1`) 定义了对常用管理数据的访问：关于系统、其接口、地址转换和协议操作（`IP`, `ICMP`, `TCP`, `UDP` 等）的信息。此 `MIB` 的稍后且更完整的重构（称为 `MIB-II`）定义在 `RFC1213` 中。大多数厂商提供一个

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_678_0.png)

## SNMP 服务器支持 MIB-II。表 20.1 展示了 MIB-II 命名空间的节点示例。

| OID* | 类型 | 内容 |
| --- | --- | --- |
| system.sysDesc | string | 系统信息：厂商、型号、操作系统类型等。 |
| system.sysLocation | string | 机器的物理位置 |
| system.sysContact | string | 机器所有者的联系信息 |
| system.sysName | string | 系统名称，通常是完整的 DNS own |
| interfaces.ifNumber | int | 存在的网络接口数量 |
| interfaces.ifTable | table | 关于每个接口的信息位表 |
| ip.ipForwarding | table | 如果是网关则为 1；否则为 2 |
| ip.ipAddrTable | table | IP 地址数据表（掩码等） |
| ip.ipRouteTable | table | 系统的路由表 |
| icmp.icmpRedirects | int | 接收到的 ICMP 重定向包数量 |
| icmp.icmpEchos | int | 接收到的 ping 数量 |
| tcp.cpConnTable | table | 当前 TCP 连接表 |
| udp.udpTable | table | 有服务器监听的 UDP 套接字表 |

* 相对于 `iso.org.domain.internet.mgmt.mib-2`。

除了基础 `MIB` 之外，还有针对各种硬件接口和协议的 `MIB`。有针对单个厂商的 `MIB` 和针对特定硬件产品的 `MIB`。一个你的 `MIB`，一个我的 `MIB`，抓住树后的那个 `MIB`。

`MIB` 仅仅是关于管理数据命名的约定。要使其有用，`MIB` 必须由代理端代码支持，代码在 `SNMP` 命名空间和设备的实际状态之间进行映射。基础 `MIB`（现在是 `MIB-II`）的代码随标准 Linux 代理提供。代理可以扩展以包含补充 `MIB`，有些则不能。

### SNMP 协议操作

只有四种基本的 `SNMP` 操作：`get`、`get-next`、`set` 和 `trap`。

`Get` 和 `set` 是读取和写入由特定 `OID` 标识的节点的基本操作。`Get-next` 用于逐个遍历 `MIB` 层次结构以及读取表格内容。

`Trap` 是从服务器（代理）到客户端（管理器）的非请求的、异步通知，用于报告有趣事件或状态的发生。定义了若干种标准 `trap`，包括“我刚刚启动”通知、报告网络链路故障或恢复的 `trap`，以及针对各种路由和身份验证问题的 `trap`。许多其他非标准的 `trap` 也在常用使用中，包括-某些仅监控其他 `SNMP` 变量值并触发的

### 网络管理与调试

由于 `SNMP` 是网络管理的标准，因此知道如何调试它非常重要。调试 `SNMP` 的基本方法是使用 `snmpwalk` 工具，它允许你查询 `SNMP` 代理并查看响应。另一个实用工具是 `snmpget`，它允许你查询特定的 `OID`。还有 `snmpset`，允许你设置特定 `OID` 的值。

调试 `SNMP` 最高级的方法是使用数据包嗅探器，它允许你在网络上捕获 `SNMP` 流量并进行分析。当你试图解决无法通过基本工具解释的复杂问题时，这种方法特别有用。

### RMON：远程监控

`RMON`（Remote Monitoring）是监控网络设备的标准。它允许你监控网络性能和统计，而无需不断查询每个设备。`RMON` 定义在 `RFC2813` 中，包含了几个 `MIB`。

## 20.9 网络管理应用程序

我们从探索最简单的 `SNMP` 管理工具开始：`NET-SNMP` 软件包提供的命令。这些命令对于熟悉 `SNMP` 非常有用，也适合对特定 `OID` 进行一次性检查。接下来，我们查看 `MRTG`，这是一个生成 `SNMP` 取值图表的程序，

以及 `NOCOL`，一个基于事件的监控系统。最后，我们对购买商业系统时需要注意的事项给出了一些建议。

### NET-SNMP 工具

即使你的系统自带 `SNMP` 服务器，你可能仍然想要从 `NET-SNMP` 包中编译并安装表 20.3 所列的客户端工具。

### 表 20.3 NET-SNMP 包中的命令行工具

| 命令 | 功能 |
| --- | --- |
| snmpdelta | 监控 SNMP 变量随时间的变化 |
| snmpgetf | 通过 SNMP 监控远程主机的磁盘空间 |
| snmpget | 从代理处获取 SNMP 变量的值 |
| snmpnext | 获取序列中的下一个变量 |
| snmpset | 在代理上设置 SNMP 变量 |
| snmptable | 获取 SNMP 变量表 |
| snmptranslate | 在 MIB 层次结构中搜索并描述 OID |
| snptrap | 生成陷阱（trap）告报 |
| snmpwalk | 从特定的 OID 开始遍历 MIB |

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_682_0.png)

除了在命令行中的价值外，这些程序在简单脚本中也非常有用。让 `snmpget` 每隔几分钟将感兴趣的数据值保存到文本通常很有帮助。（使用 `cron` 来实现调度；参见第 9 章“周期性进程”。）

`snmpwalk` 是另一个实用的工具。该命令从指定的 `OID`（或默认从 `MIB` 开始）开始，反复向代理发送“get next”调用。这种行为会返回可用 `OID` 及其关联值的完整列表。以下是来自团体字符串 `"public"` 的主机 `snmpwalk` 示例：

```
