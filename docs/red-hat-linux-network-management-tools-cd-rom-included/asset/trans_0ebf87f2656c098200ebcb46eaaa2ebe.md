
对象名称: psProcessUserName

OID: psEntry.8

对象类型: Display String [16]

访问模式: read-only

描述: 显示与此进程关联的用户名

对象名称: psProcessUserID

OID: psEntry.9

对象类型: counter

访问模式: read-only

描述: 显示与 psProcessUserName 字符串关联的数值用户 ID

对象名称: psProcessName

OID: psEntry.10

对象类型: Display String [64]

访问模式: read-only

描述: 显示此进程的命令字符串名称

对象名称: psProcessStatus

OID: psEntry.11

对象类型: Counter

访问模式: read-write

描述: 指示要发送到此进程的信号

## Sun SNMP 代理

407

## Sun 主机性能组

sunHostPerf 组包含一系列系统性能相关对象，从进程使用的总时间滴答数到总网络冲突数不等。由于这些对象的数量相当多，只会描述最有用的对象。如果您正在寻找该组中所有可用对象的完整列表，请查阅 Sun MIB 文件 /var/snmp/mib/sun.mib 以获取更多信息。

sunHostPerf 组中更有用的对象包括与系统交换、设备中断和网络流量相关的对象。图 7.13 以层级形式展示了这些对象与主 sun 分支的关系。流量对象是计数器，表示整个系统的总数，不受网络连接数量的影响，与 netstat 命令的输出类似。例如，rsIfInPackets 对象提供系统上所有网络接口从网络获得的总输入数据包数。

sunHostPerf 组包含以下对象：

对象名称: rsVpagesIn
OID: sunHostPerf.9
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来从磁盘读入的总页数

对象名称: rsVpagesOut
OID: sunHostPerf.10
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来写入磁盘的总页数

![](img/f265c9d1f2610aca197c430cbfcd51f5_439_0.png)

**图 7.13** *sunHostPerf* 视图。

对象名称: rsVSwapIn
OID: sunHostPerf.11
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来换入的总页数

对象名称: rsVSwapOut
OID: sunHostPerf.12
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来换出的总页数

对象名称: rsVIntr
OID: sunHostPerf.13
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来设备中断的总次数；包括磁盘和其他外围设备等所有设备的中断。

对象名称: rsIfInPackets
OID: sunHostPerf.14
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来从网络获得的总输入数据包数

对象名称: rsIfOutPackets
OID: sunHostPerf.15
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来传输到网络的总输出数据包数

对象名称: rsIfInErrors
OID: sunHostPerf.16
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来从网络产生的总输入错误数

对象名称: rsIfOutErrors
OID: sunHostPerf.17
对象类型: Counter
访问模式: read-only
描述: 尝试传输到网络时遇到的总输出错误数，自上次重启以来

对象名称: rsIfCollisions
OID: sunHostPerf.18
对象类型: Counter
访问模式: read-only
描述: 自上次重启以来在网络上记录的总输出冲突数

## SNMP 工具

第 4 章“核心系统实用程序和工具”以及第 5 章“其他系统实用程序和工具”讨论了操作系统工具和实用程序。本章更侧重于网络工具，这些工具可以帮助管理系统和网络元素，例如交换机、路由器、探针、集线器和其他设备。它们都基于 SNMP，可用于查询任何 SNMP 兼容代理以获取大量信息。

本章涵盖以下工具：

| 命令 | 页码 |
|---|---|
| snmpdelta | 422 |
| snmpget | 425 |
| snmpgetnext | 427 |
| snmpnetstat | 429 |
| snmpset | 434 |
| snmpstatus | 437 |
| snmptable | 440 |
| snmptest | 443 |
| snmptranslate | 443 |
| snmptrap | 445 |
| snmptrapd | 446 |
| snmpwalk | 450 |
| snmpbulkwalk | 451 |
| snmpconf | 454 |
| tkmib | 458 |

### 监控/管理功能

本节介绍的工具可访问各种代理信息，在监控和管理方面特别有用。可以从设备收集的最重要信息包括以下内容：

- SNMP 系统心跳
- 系统上下线消息
- 协议统计
- 接口性能测量
- 系统进程活动
- 路由
- 性能统计

其中一些工具也可以用于配置网络设备。以下各节描述了这些用途。

## 系统心跳

系统心跳是管理器用来确定代理和系统的总体可达性的 SNMP get-request。例如，网络管理器可能会轮询代理的系统时钟 MIB 变量，以确定每次轮询都比上一次更新。每次轮询都应表明时间在向前移动。网络管理器可能轮询的 MIB 变量是 unixTime 对象，是 Sun 系统代理的 sun-System 组的一部分。作为替代，网络管理器可以轮询来自 MIB-2 系统组的 sysUpTime 对象，该对象应可从所有 SNMP 代理获得。

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

## 一般描述

UCD 包不仅提供了一个强大而强大的 SNMP 代理，还提供了一系列可用于管理 SNMP 启用网络设备的便捷工具。这些工具支持 SNMPv1、SNMPv2 和 SNMPv3。您可以使用命令行选项选择使用的版本。此外，这些实用程序可用于构建脚本或其他程序，以完成复杂的网络管理功能或自定义任务。例如，**snmpget** 命令可以监控某些关键接口，以确定其中一个或多个是否变得不可操作。在这种情况下，适当的支持人员可以自动收到通知。
