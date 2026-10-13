
- 系统上下线消息
- 协议统计
- 接口性能测量
- 系统进程活动
- 路由
- 性能统计

其中一些工具也可以用于配置网络设备。以下各节描述了这些用途。

## 系统心跳

系统心跳是管理器用来确定代理和系统的总体可达性的 SNMP get-request。例如，网络管理器可能会轮询代理的系统时钟 MIB 变量，以确定每次轮询都比上一次更新。每次轮询都应表明时间在向前移动。网络管理器可能轮询的 MIB 变量是 `unixTime` 对象，是 Sun 系统代理的 `sun-System` 组的一部分。作为替代，网络管理器可以轮询来自 MIB-2 系统组的 `sysUpTime` 对象，该对象应可从所有 SNMP 代理获得。

## 系统上下线消息

如果系统因任何原因被关闭并重新启动，将以 SNMP trap 的形式向指定的网络管理系统发送一条消息。请回忆，trap 是代理发出的未请求消息，表示某种特殊条件或事件。通过接收这些消息，管理器会被告知例如系统中断的情况并可采取适当措施。UCD 代理配置文件和额外的工具可用于将 trap 消息转发到一个或多个网络管理系统。

## 协议统计

由于许多 SNMP 代理支持 MIB-II 标准，因此可以进行协议性能监控和系统监控。这包括 IP、ICMP、TCP、SNMP、网络接口计数器以及额外的代理系统性能对象的监控。

## 系统进程活动

借助 Sun MIB 扩展和 UCD 代理，系统进程的监控也是可能的。对象可以通过监控关键进程来建立网络的整体健康状况或单个系统的状况。

## 路由监控

路由监控代理可以确定系统的路由配置并报告发现的任何错误。例如，如果组织已确定每台机器必须具有默认路由，则可以通过探测这些设备中的 SNMP 代理来验证这一点。

## 接口性能

MIB-2 还提供了包含 SNMP 设备中安装的每个接口性能信息的对象。可以检索此信息并监控活动接口的性能。

## 配置控制

许多网络设备（例如路由器和交换机）在网络上有效使用之前必须进行配置。此外，随着网络需求的变化，这些设备中的配置也必须随之变化。这里列出的工具可用于更改设备配置。

## UCD 命令

### 一般描述

UCD 包不仅提供了一个强大而强大的 SNMP 代理，还提供了一系列可用于管理 SNMP 启用网络设备的便捷工具。这些工具支持 SNMPv1、SNMPv2 和 SNMPv3。您可以使用命令行选项选择使用的版本。此外，这些实用程序可用于构建脚本或其他程序，以完成复杂的网络管理功能或自定义任务。例如，`snmpget` 命令可以监控某些关键接口，以确定其中一个或多个是否变得不可操作。在这种情况下，适当的支持人员可以自动收到通知。

Table 8.1 lists the tools and utilities that are supplied with the UCD package.

## 表 8.1 UCD SNMP 工具

| UCD 工具 | 描述 |
| :--- | :--- |
| `snmpdelta` | 监视 SNMP 变量的变化 |
| `snmpget` | 获取一个或多个 MIB 对象 |
| `snmpgetnext` | 持续遍历 SNMP MIB 树并获取所有支持的 MIB 对象 |
| `snmpifstat` | 获取代理接口配置信息 |
| `snmpset` | 将一个或多个 MIB 对象设置为指定值 |
| `snmpstatus` | 获取重要的 MIB 对象信息 |
| `snmptable` | 获取完整的 SNMP 表 |
| `snmptrap` | 与 SNMP 代理实体通信 |
| `snmptranslate` | 将 MIB 对象转换为更有意义的信息 |
| `snmptrap` | 发送 SNMP trap 消息到一个或多个管理器 |
| `snmptrapd` | 从网络检索 SNMP traps |
| `snmpwalk` | 获取一组相关的 MIB 对象 |
| `snmpbulkwalk` | 使用 SNMP 批量请求获取 MIB 对象 |
| `tkmib` | 浏览 MIB 对象。此工具基于 Tcl/Tk。 |

The basic syntax of the UCD tools is the following:

```
snmpcmd protocol_version [additional_options] hostname community object [object]
```

The word `snmpcmd` is a placeholder and represents one of the UCD commands listed in the preceding table. All the UCD tools support this basic command syntax. The word `protocol_version` can be 1, 2c, or 3. This string identifier specifies which SNMP version should be used when sending queries to the agent. Option 1 represents the standard SNMPv1 format. The 2c option indicates differences within the supported SNMP protocol data units, but uses the same community-based approach as in SNMPv1. The 3 option indicates the use of the SNMPv3 security model.

The `additional_options` placeholder represents options that control both display attributes and operational behavior of the tools. The most commonly used command-line options are described below.

The word `hostname` can be replaced with the name of any host on the network that contains an SNMP agent that matches the `protocol_version` information specified on the command line. A valid IP address, expressed in dotted notation, may be used instead of a hostname.

The word `object` represents the MIB OID that should be retrieved (in the case of an SNMP `get-request`) or altered (in the case of an SNMP `set-requests`). It may be expressed in either dotted numeric or dotted named notation. In the case of an SNMP `set-request` operation, additional object information will be required, as discussed in the upcoming “SNMP Set Tool” section. Note that one or more objects may be specified on the command line.

## 常用命令行选项

UCD tools share a number of common command-line arguments. Having a core set of options makes them easier to remember and use. The arguments supported by all the commands are divided into two categories: operational options and display options. The operational options control the behavior of each of the tools, while the display options control how the MIB objects, associated values, and other information are displayed.

### 显示选项
