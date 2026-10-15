
## 14.8 LSM 和 `dn_setup` 命令

截至本文撰写时，`dn_setup` 命令不会重新创建 LSM 设备特殊文件。如果您使用 `dn_setup` 命令并带 “-clean” 或 “-init” 选项，您将需要使用第 7 章第 7.5.2.1 节中描述的流程重新创建 LSM 设备特殊文件：“How Can I Reinitialize My /dev and /devices Directories?”

## 14.9 CLSM 事件

虽然 CLSM 没有事件，但 LSM 事件位于 `/usr/share/evm/templates/sys/lsm.volnotify.evt` 文件中。

## 14.10 参考文献

- *TruCluster Server Technical Overview Guide*。
- *TruCluster Server Cluster Administration Guide*。
- *Tru64 UNIX Logical Storage Manager Guide*。
- *Tru64 UNIX File System Administration Handbook*，作者 Steven M. Hancock，Digital Press 出版（ISBN: 1-55558-227-3）。
- 文中注明的参考页。

## 15 设备请求调度器（DRD）

在本章中我们将讨论设备请求调度器集群子系统。设备请求调度器，如你可能已经猜到的，是调度请求到设备的子系统。实际上，它将 I/O 请求调度到集群中的任何存储设备（事实上 Compaq 内部有些工程师更喜欢称其为 DeviceIO Request Dispatcher）。DRD 还使集群能够对连接到集群中任何成员的所有存储设备有一个集群范围的视图。存储设备可以位于集群中任何系统的任何总线上；而且不仅仅是共享总线——私有总线也由 DRD 处理。DRD 不会区别对待；任何存储设备都是其管辖范围。真正棒的是，DRD 从用户的角度来看是完全透明地完成所有这些的。

你可能开始看到这里的一个趋势。每个成员都可以看到所有文件系统，每个成员都可以看到所有设备（即使是私有总线上的设备），而且所有事情都是透明完成的。不仅你的用户不需要特殊培训来使用集群，他们甚至不必知道他们正在使用集群！除少数例外，目标是让所有集群成员协同工作，使得用户将集群视为一个系统。

### 15.1 DRD 概念

DRD 的主要功能是协调对集群中存储设备的访问。这种协调是通过为所有存储设备提供一个集群范围的命名空间、各集群成员的 DRD 组件之间的通信（DRD 是一个客户端/服务器实现），以及审慎使用 I/O 屏障来防止 rogue 节点损坏集群范围存储设备上的数据来实现的。

#### 15.1.1 集群范围设备命名空间

DRD 子系统是使集群中的每个成员都能看到集群中每个存储设备的机制。由于设备在被发现时会被赋予名称，当一个成员加入集群时，其设备会被命名。设备命名已在第 7 章中详细讨论过。

集群中的第一个成员将按检测到的顺序为其检测到的设备分配名称（见图 15-1）。

![](img/a0df85c2e542a8d6c913113908553aa4_398_0.png)

## 图 15-1：集群范围设备命名

必须记住，设备名称与设备的全球唯一标识符（WWID）相关联，而非设备在总线上的位置。有关更多信息，请参阅第 7 章中关于 WWID 的讨论。如图所示，直接连接到 member1 的设备具有最低的设备名称（即 floppy0、cdrom0、dsk0-dsk6 和 tape0）。当第二个成员加入集群时，直接连接到它的设备（并且未直接连接到 member1）将被检测到，命名将继续使用序列中的下一个数字（即 floppy1、cdrom1、dsk7-dsk9）。当第三个成员加入集群时，直接连接到它的设备（并且未直接连接到 member1 或 member2）将被检测到，并按连接到 member2 的设备之后顺序命名（即 floppy2、cdrom2、dsk10-dsk11）。

DRD 会在以下三种情况下查找设备：

- 启动时。
DRD 会在启动时查询硬件管理子系统，以获取其需要管理的设备。

- 设备打开。
如果在请求打开某个设备时 DRD 不知道该设备，它将查询硬件管理子系统以获取该特定设备。

- 设备检测。
当新设备添加到系统时，硬件管理子系统会在检测到时向 EVM 发布事件（例如执行 "`hwmgr -scan scsi`" 命令的结果）。DRD 是硬件管理子系统向 EVM 发布事件的订阅者。

## 图 15-2：TruCluster Server I/O 子系统架构

#### 15.1.2 集群范围的 I/O

集群中对存储设备的所有 I/O 都会经过 DRD 子系统，正如您现在所熟悉的 TruCluster I/O 子系统架构图（图 15-2）所示。直接 I/O（参见第 13 章）、字符 I/O 以及块/文件 I/O 最终都会经由 DRD。图中即使是“客户端”路径，也会通过节点间通信子系统（ICS）发送到另一个集群成员的 DRD。

DRD 是一种按设备实现的客户端/服务器实现。而且，更值得一提的是，某些设备可以由多个成员同时提供服务。那么 DRD 是如何做到这一点的呢？实际上，DRD 可以采用两种方法：间接方法或直接方法。

间接方法使用客户端/服务器（或称受服务）技术，其中一个集群成员充当某设备的 DRD 服务器，所有其他成员都是 DRD 客户端（仅通过该 DRD 服务器访问设备）。这与 TruCluster Production Server 产品中的分布式原始磁盘（另一个 DRD）组件的运作方式类似¹。

直接方法则通过支持直接访问 I/O（DAIO）的设备来实现。DAIO 实现源于为 TruCluster Production Server 1.5 版所做的多节点同时访问（MUNSA）²工作。

##### 15.1.2.1 直接访问 I/O（DAIO）设备

如果设备支持直接访问 I/O，则该设备可以由多个 DRD 提供服务。什么决定设备是否具备 DAIO 能力？

- 设备必须启用硬件坏块替换功能。
- 设备必须支持带标签排队（tagged queuing），以便主机进行命令排序。
- 设备必须支持来自多个发起方的同时访问。

TruCluster Server 5.0A、5.1 和 5.1A 版本支持的所有磁盘设备都具备 DAIO 能力。

图 15-3 说明了在四成员集群中如何访问 DAIO 设备。在图中，您可以看到集群中的每个成员都能直接访问磁盘。每个成员的说明文字展示了在各成员上运行 `drdmgr(8)` 命令时会得到的一个略有不同的视图。由于集群中每个成员都与磁盘所在的总线有物理连接，因此“number of servers”属性的值为 4。服务器列在“server name”字段中。所有四个成员的“server state”均为“Server”，这一事实表明这四个成员都可以主动访问此磁盘。有效的服务器状态为：“Server”和“Not Server”。

尽管该设备有四个活动服务器，但每个成员将一次通过一个服务器访问磁盘。成员当前用于访问设备的服务器由“access member name”指示。默认情况下，如果成员本身也是服务器，则其“access member name”始终为其自身。

在图 15-3 中，每个成员都可以直接访问，因为它们与设备所连接的总线物理相连，并且设备支持 DAIO（如“device type”字段所示）。在撰写本文时，您会在 `drdmgr` 命令的输出中看到四种有效的设备类型：“Direct Access IO Disk”（在图中表示为 DAIO）、“Served Disk”、“Served Tape”和“Served Changer”。

设备可能是 DAIO，但集群中仍有无法直接访问该设备的成员。尽管设备可以拥有多个服务器，但由于物理连接的限制，该设备可能只有一个服务器。图 15-4 展示了私有总线上的 DAIO 设备。DRD

> ¹ 有关分布式原始磁盘和 TruCluster Production Server 的更多信息，请参阅第 2 章。
> ² MUNSA 不包含在正式发布的产品中。它是专门为客户创建的补丁。

```
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
```

```
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
```

```
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
```

```
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
```

## 图 15-3：直接访问 I/O

![](img/a0df85c2e542a8d6c913113908553aa4_401_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_401_1.png)

```
device name: dsk8
device type: DAIO
number of servers: 1
server name: N2
server state: Server
access member name: N2
```

```
device name: dsk8
device type: DAIO
number of servers: 1
server name: N2
server state: Server
access member name: N2
```

## 图 15-4：DAIO 设备，私有总线

并不真正关心设备的物理位置。如果一个成员想要访问它没有物理连接的设备，它会将请求分派给在具有直接连接的成员上的 DRD。

### NOTE:

像 RZ26、RZ28、RZ29 和 RZ1CB-CA 这样的旧 SCSI 设备默认情况下未启用坏块替换，因此如果您添加此类型的设备，可以运行 `clu_disk_install` 脚本来启用坏块替换。如果同时安装多个设备，此脚本的完成可能需要一段时间。

##### 15.1.2.2 Served Devices

如果设备是被服务的设备，则集群中的一个成员会主动将设备服务给其他集群成员，而不管该设备是否可以通过物理连接被多个成员访问（即共享总线）。

磁带和磁带库设备以及所有 CD-ROM、DVD-ROM³、软盘设备，以及一些硬盘设备都是被服务的设备。不过，与磁带和磁带库设备不同，CD-ROM、DVD-ROM 和软盘设备截至目前，无法位于共享总线上。

图 15-5 显示了一个具有共享总线上被服务磁带设备的两成员集群。请注意，有两个潜在的服务器，然而 member1 的服务器状态为“Not Server”。这是因为磁带设备不是 DAIO 设备。换句话说，虽然两个成员都可以服务该设备，但一次只能有一个设备服务该设备；因此该设备的设备类型为“served”——在本例中为“Served Tape”。

![](img/a0df85c2e542a8d6c913113908553aa4_402_0.png)

Figure 15-5: Served Device, Shared Bus

³ DVD-ROM 设备在 V5.1 及更高版本中受支持。

#### 15.1.3 I/O Barriers

I/O Barriers 用于在集群中模拟单系统在关机或故障时如何处理 I/O。换句话说，当独立系统关机或崩溃时，任何未完成的 I/O 在成员重新启动时都不会被传递到设备。

I/O Barrier 是软件和硬件/固件的组合。在软件端，DRD 通过在没有仲裁的节点上阻止 I/O 来创建屏障，而在硬件/固件端，I/O Barriers 在 CAM 层通过总线复位、总线设备复位和持久保留来实现。

当集群正常运行时，所有成员都被允许对集群中的所有存储设备执行 I/O。事情变得有趣起来，当一个成员关机、崩溃或变得无法通信时（注意：当集群正在形成以及成员加入集群时，DRD 也会为集群中所有新设备竖起 I/O Barriers）。

当连接管理器⁴（CNX）感知到一个成员离开集群，无论是自愿还是其他原因，它都会启动集群成员资格转换，以确定哪些节点被允许继续留在集群中，哪些节点不被允许。当成员资格转换开始时，DRD 会阻止并排队任何新的 I/O，同时排出之前排队的任何 I/O。至少这是应该发生的情况。然而，由于成员可能正在经历导致成员资格转换发生的硬件或软件错误，成员可能无法正确排出，而是继续将 I/O 传递到共享存储。

一旦集群成员资格转换完成，CNX 会指示 DRD 在不再是集群成员的任何节点周围竖起 I/O Barrier。I/O Barrier 保证由不再是成员的节点提交给 DRD 的任何 I/O 都不会提交到集群范围内的共享存储。

例如，使用本章前面图 15-1 中的三成员集群，假设 member1 正在向 disk4 写入时发生了导致 member1 关机的情况。表 15-1 显示在时间 T1，所有三个成员都能够对集群中的任何存储设备执行 I/O，当 member1 出现故障导致其关机时。在时间 T2，集群整体必须经过由每个成员上的 CNX 处理的集群成员资格转换，以确定哪些成员可以继续参与集群。此时，DRD 将阻止任何新的 I/O 并将其排队，以便在集群震荡完成后提交。在转换之前排队的任何 I/O 都将被排出。在 CNX 确定新的集群成员资格之后（时间 T3），那些被投票踢出“集群俱乐部”的成员将被锁定——换句话说，I/O Barriers 被竖起，任何分布式锁管理器³（DLM）锁都被重新配置。

你可能会想知道当 DRD “排出”之前排队的 I/O 时会发生什么。我们向 TruCluster Server 工程师之一提出了这个问题，他解释说，待处理的 I/O 请求会被处理（从共享存储设备读取或写入共享存储设备）。如果 I/O 收到错误并且需要重试，则会重新排队。从共享存储设备返回给 DRD 的 I/O 会返回给调用线程。当排出完成后，不再有未完成的 I/O 需要处理，任何新的 I/O 都将被排队。

⁴ 有关连接管理器的更多信息，请参阅第 17 章。

³ 有关分布式锁管理器的更多信息，请参阅第 18 章。

| 集群成员 | 时间 |  |  |  |
|---|---|---|---|---|
|  | T1 | T2 | T3 | T4 |
| member1 | I/O 正常进行 | 新的 I/O 被阻塞并排队，除非因 H/W 和/或 S/W 错误而阻止 | 先前排队的 I/O 被清空，除非因 H/W 和/或 S/W 错误而阻止 | I/O 屏障 | I/O 被拒绝 |
| member2 | I/O 正常进行 | 新的 I/O 被阻塞并排队 | 先前排队的 I/O 被清空 | 新的 I/O 被阻塞并排队 | I/O 正常进行 |
| member3 | I/O 正常进行 | 新的 I/O 被阻塞并排队 | 先前排队的 I/O 被清空 | 新的 I/O 被阻塞并排队 | I/O 正常进行 |
|  | member1、member2 和 member3 是集群成员。可以对任何存储设备执行 I/O。 | CNX 检测到与 member1 的连接问题并开始集群成员资格转换。DRD 将阻塞并排队新的 I/O，直到集群转换完成。DRD 将清空在集群状态转换之前排队的 I/O。 | I/O 屏障被建立，任何 DLM 锁将被重新配置。 | member1 不再是集群成员。时间=T2 后从 member1 提交的任何 I/O 将被拒绝。member2 和 member3 上的 I/O 将继续。 |

## 表 15-1：集群成员资格转换和 I/O 屏障

## 15.2 配置 DRD

由于 DRD 子系统设计为自动配置，因此通常不需要任何设置。然而，你可以做一些事情来修改配置，例如更改设备的访问成员名称或服务器以及重置设备的 DRD 统计信息。

### 15.2.1 更改访问成员名称

通常，设备的访问成员名称不应需要修改；然而，由于有几个实例可能有用，该功能可通过 `drdmgr` 命令使用。你需要更改访问成员名称的一个实例是当你想在集群中跨 DRD 服务器平衡 I/O 时，成员并非都具有对设备进行物理访问的能力，如图 15-6 所示。

在图 15-6 中，member2 和 member3 可以直接访问 `dsk8`，但 member1 和 member4 不能，因此它们必须通过 member2 或 member3 访问 `dsk8`。默认情况下，首先启动的成员将成为其他成员的服务器。在图 15-6 中，member2 很可能

![](img/a0df85c2e542a8d6c913113908553aa4_405_0.png)

在 member3 之前启动，因此是 member1、member4 和其自身的“访问成员”。然而，我们可能希望分发负载，以便 member2 不处理所有远程 DRD 请求。我们可以通过使用 `drdadmin` 命令修改 member1 或 member4 的访问成员来实现。例如，我们将把 member4 上的访问成员从 member2 更改为 member3。
