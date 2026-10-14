

## 图 15-2：TruCluster Server I/O 子系统架构

### 15.1.2 集群范围的 I/O

集群中对存储设备的所有 I/O 都会经过 DRD 子系统，正如您现在所熟悉的 TruCluster I/O 子系统架构图（图 15-2）所示。直接 I/O（参见第 13 章）、字符 I/O 以及块/文件 I/O 最终都会经由 DRD。图中即使是“客户端”路径，也会通过节点间通信子系统（ICS）发送到另一个集群成员的 DRD。

DRD 是一种按设备实现的客户端/服务器实现。而且，更值得一提的是，某些设备可以由多个成员同时提供服务。那么 DRD 是如何做到这一点的呢？实际上，DRD 可以采用两种方法：间接方法或直接方法。

间接方法使用客户端/服务器（或称受服务）技术，其中一个集群成员充当某设备的 DRD 服务器，所有其他成员都是 DRD 客户端（仅通过该 DRD 服务器访问设备）。这与 TruCluster Production Server 产品中的分布式原始磁盘（另一个 DRD）组件的运作方式类似¹。

直接方法则通过支持直接访问 I/O（DAIO）的设备来实现。DAIO 实现源于为 TruCluster Production Server 1.5 版所做的多节点同时访问（MUNSA）²工作。

### 15.1.2.1 直接访问 I/O（DAIO）设备

如果设备支持直接访问 I/O，则该设备可以由多个 DRD 提供服务。什么决定设备是否具备 DAIO 能力？

- 设备必须启用硬件坏块替换功能。
- 设备必须支持带标签排队（tagged queuing），以便主机进行命令排序。
- 设备必须支持来自多个发起方的同时访问。

TruCluster Server 5.0A、5.1 和 5.1A 版本支持的所有磁盘设备都具备 DAIO 能力。

图 15-3 说明了在四成员集群中如何访问 DAIO 设备。在图中，您可以看到集群中的每个成员都能直接访问磁盘。每个成员的说明文字展示了在各成员上运行 drdmgr(8) 命令时会得到的一个略有不同的视图。由于集群中每个成员都与磁盘所在的总线有物理连接，因此“number of servers”属性的值为 4。服务器列在“server name”字段中。所有四个成员的“server state”均为“Server”，这一事实表明这四个成员都可以主动访问此磁盘。有效的服务器状态为：“Server”和“Not Server”。

尽管该设备有四个活动服务器，但每个成员将一次通过一个服务器访问磁盘。成员当前用于访问设备的服务器由“access member name”指示。默认情况下，如果成员本身也是服务器，则其“access member name”始终为其自身。

在图 15-3 中，每个成员都可以直接访问，因为它们与设备所连接的总线物理相连，并且设备支持 DAIO（如“device type”字段所示）。在撰写本文时，您会在 drdmgr 命令的输出中看到四种有效的设备类型：“Direct Access IO Disk”（在图中表示为 DAIO）、“Served Disk”、“Served Tape”和“Served Changer”。

设备可能是 DAIO，但集群中仍有无法直接访问该设备的成员。尽管设备可以拥有多个服务器，但由于物理连接的限制，该设备可能只有一个服务器。图 15-4 展示了私有总线上的 DAIO 设备。DRD

> ¹ 有关分布式原始磁盘和 TruCluster Production Server 的更多信息，请参阅第 2 章。
> ² MUNSA 不包含在正式发布的产品中。它是专门为客户创建的补丁。

device name: dsk8
device type: DAIO
number of servers: 4
server name: N1
server state: Server
server name: N2
server state: Server
server name: N3
server state: Server
server name: N4
server state: Server
access member name: N2

device name: dsk8
device type: DAIO
number of servers: 4
server name: N1
server state: Server
server name: N2
server state: Server
server name: N3
server state: Server
server name: N4
server state: Server
access member name: N3

device name: dsk8
device type: DAIO
number of servers: 4
server name: N1
server state: Server
server name: N2
server state: Server
server name: N3
server state: Server
server name: N4
server state: Server
access member name: N1

device name: dsk8
device type: DAIO
number of servers: 4
server name: N1
server state: Server
server name: N2
server state: Server
server name: N3
server state: Server
server name: N4
server state: Server
access member name: N4

## 图 15-3：直接访问 I/O

![](img/a0df85c2e542a8d6c913113908553aa4_401_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_401_1.png)

device name: dsk8
device type: DAIO
number of servers: 1
server name: N2
server state: Server
access member name: N2

device name: dsk8
device type: DAIO
number of servers: 1
server name: N2
server state: Server
access member name: N2

## 图 15-4：DAIO 设备，私有总线

