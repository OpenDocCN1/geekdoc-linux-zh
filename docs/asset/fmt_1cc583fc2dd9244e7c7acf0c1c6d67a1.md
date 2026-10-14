
http://www.arkeia.com

# 第 17 章. SNMP

SNMP 代表简单网络管理协议（Simple Network Management Protocol）。然而，不要被这个名称所误导；SNMP 可以非常强大且复杂。SNMP 是一种应用层协议，用于促进网络设备之间管理信息的交换。它是传输控制协议/网协议（TCP/IP）协议套件的一部分。

SNMP 实现的两个主要组件是 SNMP 代理（agent）和网络管理应用程序。

- SNMP 代理
  代理是驻留在受管设备上的用于收集管理信息的软件组件。受管设备可以是 UPS、路由器或计算机等任何设备。
- 网络管理应用程序
  网络管理应用程序可以监控和控制运行 SNMP 代理的设备。

SNMP 通信中最常用的三个命令是读取（read）、写入（write）和陷阱（trap）。

- 读取（Read）：用于网络管理应用程序查询 SNMP 代理获取管理信息。
- 写入（Write）：用于网络管理应用程序修改 SNMP 代理维护的变量。
- 陷阱（Trap）：用于 SNMP 代理在达到定义阈值或发生事件时向网络管理应用程序发送警报。

## 17.1 团体字（Community Strings）

代理负责收集的管理信息称为管理信息库（MIB，Management Information Base）。MIB 是按层次结构组织的，由受管对象组成。这些受管对象通过 MIB 层次结构中的对象标识符（OID）来标识。

MIB 树从标准开始：CCITT、ISO 和 internet。我们将查看示例的对象位于 `.iso.dod.mgmt.mib-2` 分支下。

![](img/85b06e2bfb0156a5e744cfac214d4788_365_0.png)

图 306. MIB 树示例

在 `mib-2` 分支下，我们包含了一些关于网络接口的通用信息。通过深入研究 MIB 子集可以获取更具体的细节。例如：

- `.1.3.6.1.2.1.1.1` `sysDesc`：实体的文本描述。
- `.1.3.6.1.2.1.1.2` `sysType`：系统的硬件类型、操作系统和版本。
- `.1.3.6.1.2.1.1.3` `sysUpTime`：系统启动以来的时间（以毫分之一计）。
- `.1.3.6.1.2.1.1.4` `sysContact`：该节点的文本联系方式。
- `.1.3.6.1.2.1.1.5` `sysName`：管理分配的节点名称。
- `.1.3.6.1.2.1.1.6` `sysLocation`：该节点的物理位置。

在标准-2 分支下，我们有许多可以用于跟踪网络状态的 OID。例如：

- `.1.3.6.1.2.1.1.10` `ifInOctets`：接口接收的总字节数。
- `.1.3.6.1.2.1.1.16` `ifOutOctets`：接口发送的总字节数。
- `.1.3.6.1.2.1.1.20` `ifOutErrors`：因错误无法发送的输出数据包数量。
- `.1.3.6.1.2.1.1.8` `ifOperStatus`：接口的当前运行状态（开启、关闭或测试中）。

这些示例包含了关于网络接口的通用信息。通过深入研究 MIB 分支可以获取更多特定的信息。

## 17.2 我为什么应该使用 SNMP？

SNMP 通常用于衡量网络性能、发现并解决网络问题以及规划增长。然而，你也可以使用 SNMP 监控 UPS 的负载、路由器和计算机的 CPU 利用率，甚至是磁盘 I/O 和剩余空间。可能性是无限的。

你不仅限于预定义的 MIB。虽然这超出了本文的范围，但你可以编译自己的 MIB。我敦促你查看 `net-snmp` 软件包中的文档。

> 注意 在紧急情况下，时间至关重要。某些商业 SNMP 包包含分页软件。如果你希望使用分页功能但你的软件没有包含，请查看包含在 SuSE 中的免费应用程序 `HylaFAX`。

## 17.3 在 Linux 上实现 SNMP

SNMP 软件包可以在（网络）软件包选择部分找到：

```
snmp
```

随 SNMP 安装的默认配置适用于我们的目的。欲需更多关于配置文件语法的信息，请参阅 `snmpd.conf` 页面。

启动 `snmpd`，输入：

```
snmpd start
```

恭喜。你已经设置了一个基础 SNMP 代理。对于我们的 SNMP 实现，我们将使用 `snmpget` 命令。该命令查询指定主机上的 SNMP 代理以获取一个或多个 OID 值。语法如下：

```
snmpget HOST COMMUNITY OID
```

尝试以下命令：

```
snmpget localhost public .1.3.6.1.2.1.1.0
```

您应该得到类似的响应：

```
system.sysDesc.0 = OCTET STRING:"Linux Mail 2.2.16 i1686"
```

OID `.1.3.6.1.2.1.1.1` 映射到系统描述。

要查看我们树中的所有可用对象，我们使用 `snmpwalk` 命令。该命令查询整个树而不是单个 OID。

基本语法与 `snmpget` 相同（尽管这两个命令有几个不同的选项）：

```
snmpwalk localhost public .1
```

使用此命令可以“遍历”你可访问的整个 OID 树。你可以从网络上的远程 Linux 主机使用 `snmpwalk` 和 `snmpget` 命令，并获得相同的结果。

这是一个非常简单的 SNMP 实现。SNMP 软件包中包含了一个示例 `snmpd.conf` 文件，其中包含了监控 CPU 利用率、磁盘空间和其他有用示例的方法。这些软件包还提供了设置陷阱（traps）并发送到指定主机的功能。`net-snmp` 的文档非常详尽，请查阅。

### 17.3.1 MRTG

多路由器流量图 (`MRTG`) 是一种利用 SNMP 监控网络链路流量负载的工具。`MRTG` 生成包含图像的 HTML 页面，提供流量的快照视觉化表示。`MRTG` 是使用 SNMP 实现功能的绝佳示例。

![](img/85b06e2bfb0156a5e744cfac214d4788_368_0.png)

图 307. MRTG 运行中

`MRTG` 需要安装 Perl。如果未安装 Perl 包，只需挂载发行版媒体并安装以下 RPM：

```
perl
```

来自 `base system`（基础系统）部分。

虽然 `MRTG` 可以在没有 Web 服务器的情况下使用，但我们建议你安装 Apache Web 服务器。请参阅第 197 页第 7 章“Apache 和 IBM HTTP 服务器”。

从 `n(networking)` 软件包选择部分安装 `mrtg` 软件包。

第 17 章. SNMP 355

在我们的示例中，我们将创建一个配置文件来监控并对 `localhost` 上的网络流量绘制图表。我们将使用 `cfgmaker` 工具来创建该配置文件：

```
cd /usr/local/share/doc/packages/mrtg /cfgmaker publics localhost > /etc/mrtg.conf
```

我们需要编辑新创建的 `mrtg.conf`。在 Global config options 部分，取消注释并修改 UNIX 的 `WorkDir` 条目，将默认的 HTML 目录改为子目录 `mrtg`。在我们的示例中，我们使用的是 Apache Web 服务器，它从 `/usr/local/httpd/htdocs` 提供 Web 页面。打开位于以下目录下的 `mrtg.conf`：

```
WorkDir: /usr/local/httpd/htdocs/mrtg
```

保存文件：

示例 `mrtg.conf` 文件：

```
################################################################

# Description: Linux math 2.2.16 1686

# Contact: jhkins@wlib.com

# Location: Seattle, WA USA

################################################################
```

```
### Interface 2 Descr: 'eth0' | Name: '' | Ip: '192.168.1.1' | 05-44-99

[localhost_2]: 2:public192.168.1.1

MaxBytes[localhost_2]: 96000

Title[localhost_2]: Traffic Analysis for 2 - phu

PageTop[localhost_2]: <html>Traffic Analysis for 2 - phu</html>

<TABLE><TR><TD>System</TD><TD>phu in Seattle</TD></TR>

<TR><TD>Maintainer</TD><TD>jhkins@rwest.net</TD></TR>
```
