
```
udp    0    0 0.0.0.0:1024    0.0.0.0:*    406/named
udp    0    0 10.0.2.201:53    0.0.0.0:*    406/named
udp    0    0 127.0.0.1:53    0.0.0.0:*    406/named
udp    0    0 0.0.0.0:518    0.0.0.0:*    362/netd
udp    0    0 0.0.0.0:517    0.0.0.0:*    362/netd
udp    0    0 0.0.0.0:111    0.0.0.0:*    255/PORTMAP
```

`snmpd` 进程以**粗体**显示，包含的信息与 `udpTable` 相同。有关 `netstat` 命令的完整说明，请参阅第 4 章“核心系统实用程序和工具”。

## EGP 组

`egp` 组包含与系统中外部网关协议的操作和实现相关的计数器和对象。由于大多数 UNIX 系统不实现此组，因此未包含其说明。但请注意，某些网络设备（如提供路由服务的设备）将支持此 MIB 组。

## 传输 (dot3) 组

`dot3` 组包含的对象提供了关于系统上每个已定义接口的低级数据链路媒介的详细信息。实际上，`dot3` 组并非真正的组，而是 MIB-II 分支层次结构下的一个节点。该组的主要目的是以特定接口 MIB 的形式提供特定于接口的信息。回顾一下，`interfaces` 组提供适用于给定系统上所有接口的通用信息。`dot3` 下的特定接口 MIB 包含与特定数据链路协议（如以太网）相关的信息。

以太网 MIB 在 RFC1643 中定义，定义了一组代表类以太网通信媒介属性的对象。EtherLike MIB 包含三种不同的访问方法（或 `ifType`），包括 `ethernet-csmacd`、`iso88023-csmacd` 和 `starlan`。`ethernet-csmacd` 方法适用于使用基带同轴电缆介质在 10Mbps 下运行的以太网标准。`iso88023-csmacd` 方法涵盖 IEEE 802.3 委员会制定的所有标准和国际标准 ISO 8802-3。其中包括的拓扑和布线介质有快速以太网，它使用 UTP 和光纤以及千兆以太网。`starlan` 方法涵盖已废弃的 1 Mbps LAN 拓扑。请注意，只有以太网等网络技术使用此 MIB。其他网络介质类型（例如 FDDI）没有冲突。支持这些类型接口的设备通常不支持此 MIB 组。

### 图 6.14 dot3 传输组视图。

![](img/f265c9d1f2610aca197c430cbfcd51f5_338_0.png)

`dot3StateTable` 表记录代理与物理网络媒介之间观察到的流量统计信息。需要使用表而不是一组特定的计数器，因为工作站、服务和其他网络设备可能包含不止一个网络接口。因此，系统上每个已定义的接口都有一个表条目。该表由 `dot3StateIndex` 对象索引。`dot3StateTable` 表对象如图 6.15 所示。

### 图 6.15 dot3StateTable 视图。

![](img/f265c9d1f2610aca197c430cbfcd51f5_339_0.png)

#### dot3StateTable 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dot3StateEntry | dot3StateTable.1 | Sequence | read-only | 类以太网网络接口的统计信息 |
| dot3StateIndex | dot3StateEntry.1 | Integer | read-only | 标识 dot3StateTable 表中的一个接口 |
| dot3StateAlignmentErrors | dot3StateEntry.2 | Counter | read-only | 从网络读取的、包含在正确字节边界内的帧 |
| dot3StateFCSErrors | dot3StateEntry.3 | Counter | read-only | 从网络读取的、未通过帧检验序列 (FCS) 的帧 |
| dot3StateSingleCollisionFrames | dot3StateEntry.4 | Counter | read-only | 在网络上传输且恰好导致一次冲突的帧 |
| dot3StateMultipleCollisionFrames | dot3StateEntry.5 | Counter | read-only | 在网络上传输且导致多次冲突的帧 |
| dot3StateSQETestErrors | dot3StateEntry.6 | Counter | read-only | SQE 测试检查生成的频率 |
| dot3StateDeferredTransmission | dot3StateEntry.7 | Counter | read-only | 因网络争用而导致首次传输尝试延迟的帧数 |
| dot3StateLateCollisions | dot3StateEntry.8 | Counter | read-only | 传输时在 12 比特时间间隔检测到冲突的次数 |
| dot3StateExcessiveCollisions | dot3StateEntry.9 | Counter | read-only | 因过度冲突而失败的传输帧数 |
| dot3StateInternalMacTransmitErrors | dot3StateEntry.10 | Counter | read-only | 因内部媒体访问控制 (MAC) 错误而失败的传输帧数 |
| dot3StateCarrierSenseErrors | dot3StateEntry.11 | Counter | read-only | 传输帧时载波侦听 (CS) 条件丢失或未断言的次数 |
| dot3StateFrameTooLong | dot3StateEntry.13 | Counter | read-only | 超过最大帧长度的接收帧数 |
| dot3StateInternalMacReceiveErrors | dot3StateEntry.16 | Counter | read-only | 因内部媒体访问控制 (MAC) 错误而失败的接收帧数 |
| dot3StateEtherChipSet | dot3StateEntry.17 | Counter | read-only | 与该接口关联的芯片组名称 |

`dot3CollTable` 表包含代理与网络媒介之间观察到的冲突活动记录。它为系统上定义的一组接口存储一个直方图。`dot3CollCount` 对象包含每个接口的单个直方图点。`dot3CollFrequencies` 对象存储在关联的 `dot3CollCount` 对象中恰好经历特定冲突次数的接口上的传输帧数。

#### dot3CollTable 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dot3CollEntry | dot3CollTable.1 | Sequence | read-only | 一组网络接口的冲突直方图集合 |
| dot3CollCount | dot3CollEntry.1 | Counter | read-only | 特定接口的一个直方图点。特定接口的冲突总数 |
| dot3CollFrequencies | dot3CollEntry.2 | Counter | read-only | 接口上经历关联 dot3CollCount 对象中确切冲突次数的帧数 |

剩下的两个表 `dot3Tests` 和 `dot3Errors` 用于测试接口和报告错误。`dot3Tests` 表包含两个对象 `dot3TestTDR` 和 `dot3TestLoopBack`，用于标识可针对网络媒介调用的特定测试。`dot3TestTDR` 对象调用时域反射仪 (TDR) 测试，而 `dot3TestLoopBack` 对象提供硬件环回测试。`dot3Errors` 表也包含两个对象 `dot3ErrorInitError` 和 `dot3ErrorLoopbackError`，用于存储与从 `dot3Tests` 表执行的任何测试相关的错误信息。

#### dot3Tests 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dot3TestTDR | dot3Tests.1 | Counter | read-only | TDR 测试 |
| dot3TestLoopBack | dot3Tests.2 | Counter | read-only | 环回测试 |

#### dot3Errors 对象

| 对象名称 | OID | 对象类型 | 访问模式 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dot3ErrorInitError | dot3Errors.1 | Counter | read-only | 初始化错误 |
| dot3ErrorLoopbackError | dot3Errors.2 | Counter | read-only | 环回错误 |
