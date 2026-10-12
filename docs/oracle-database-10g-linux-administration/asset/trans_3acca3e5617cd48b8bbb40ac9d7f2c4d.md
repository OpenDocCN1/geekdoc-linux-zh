
Linux 上的 RAC 集群支持多达 64 个集群节点。集群中的每个节点都有不同的物理 Internet Protocol (IP) 地址。然而，用户（或客户端）可以通过虚拟数据库服务名连接到数据库。Oracle 可以自动在集群的多个节点之间平衡用户负载，或 DBA 可以手动平衡用户负载。不同节点上的 RAC 数据库实例订阅全部或部分数据库服务的子集。这使您可以选择是否允许连接到特定数据库服务的特定应用程序客户端连接到部分或全部数据库节点。如果向集群添加更多节点，新节点的 CPU 和内存资源会立即提供给集群的其余部分。数据无需重新分区。这使您可以根据需要添加节点。RAC 集群的组件如图 7-2 所示。

![](img/9479df2d00f5e62b87366b125224950f_201_0.png)

FIGURE 7-2. *Oracle RAC 集群的组件*

在 Oracle RAC 中，磁盘访问和管理数据的资源是共享的。所有实例都有共同的数据和控制文件。每个节点都有自己的专用系统内存、操作系统、数据库实例和应用程序软件。每个实例还具有单独的重做日志文件。

每个单独的服务器运行自己的 Oracle 实例。这些实例共同构成一个 RAC 数据库。一组节点上可以安装多个 RAC 数据库。这些数据库的实例可以使用集群中的全部或部分活动节点。

Oracle RAC 使用一种称为 Cache Fusion 的共享缓存系统。Cache Fusion 使用集群中所有节点的集体缓存来满足数据库请求（见图 7-3）。现在对数据块的请求可以由本地缓存或任何其他缓存来满足（而不是必须访问磁盘）。只有在集体缓存中都不包含必要数据时，或当更新事务执行需要磁盘写入保证的 COMMIT 操作时，才会执行大量的磁盘 I/O。Cache Fusion 使集群上的节点能够使用高速集群互连高效地同步其内存缓存，从而使磁盘 I/O 最小化。关键在于 Cache Fusion 使集群上的所有节点都能共享访问磁盘上的所有数据。数据无需在节点之间进行分区。Oracle 是唯一具有此功能的开放系统数据库。

![](img/9479df2d00f5e62b87366b125224950f_202_0.png)

FIGURE 7-3. Oracle RAC Cache Fusion 架构

174 Oracle Database 10g Linux 管理

## Oracle RAC 10g 组件

Oracle RAC 10g 由多个组件组成。这些组件包括 Cluster Ready Services、服务和自动工作负载管理、虚拟 Internet 协议以及 Oracle Cluster Registry。

### 集群就绪服务 (CRS)

Oracle Real Application Clusters (RAC) 10g 在所有 Oracle Database 10g 平台上引入了完整的集成集群软件管理解决方案。该集群软件称为 Cluster Ready Services (CRS)，包括集群连接、消息传递和锁定以及集群控制和恢复的机制，以及工作负载管理框架。Oracle 10g 不需要第三方集群软件管理软件，尽管 Oracle 在某些平台上仍继续支持一些第三方工具。

CRS 是 Oracle 10g 相对于 9i 的核心变化。CRS 提供了一种在所有平台上保持一致的简单集群软件技术。在 Linux 上的 Oracle 9i 中，集群软件是一个复杂的部分，如果在安装开始时未正确配置，可能导致需要从头重新安装的问题。CRS 必须在安装 RAC 之前安装并运行。使用 Oracle RAC 10g，所有平台均支持多达 64 个节点。用户还可以在所有平台上对高可用性挑战（如服务器节点故障和集群互连故障）获得一致的响应。

CRS 由以下部分组成：CRS home，即 Cluster Ready Services 的单独主目录；Oracle Cluster Registry (OCR)；以及 CRS 投票磁盘。CRS 主目录应位于本地驱动器上。由于在 RAC 集群中的任何 Oracle 实例启动之前都需要访问 OCR 和投票磁盘，因此不能使用 Automatic Storage Management (ASM) 来存储这两个文件。CRS 文件必须驻留在共享文件系统上，例如 OCFS 或 RAW 设备。

与 CRS 关联的守护进程有三个：Cluster Ready Services Daemon (CRSD)、Oracle Cluster Synchronization Server Daemon (OCSSD) 和 Event Manager Daemon (EVM)。CRSD 执行高可用性恢复和管理操作，例如维护 OCR。它还管理应用程序资源；即启动、停止和使应用程序资源失效。CRSD 以 root 身份运行，并在失败时自动重启。CRSD 将集群状态信息和配置配置文件保存在 OCR 中。

OCSSD 管理集群节点成员关系并以 oracle 用户身份运行。该守护进程维护心跳，其失败将导致系统重启。这是为了防止在发生脑裂的情况下数据损坏而设计的功能。它提供节点成员关系、组访问和基本集群锁定。OCSSD 可以与非 RAC 系统一起运行。它可以与第三方集群产品集成，也可以不集成到供应商集群软件中运行。OCSSD 也是使用 ASM 的单实例的一部分。

EVMD 是启动 RACGEVT 进程的事件管理器守护进程。当集群发生事情时，该守护进程会生成事件。它生成一个永久的子进程 emvlogger。EVMD 扫描 callout 目录并调用 callout。与 CRSd 类似，该守护进程在失败时自动重启，但它以 oracle 用户身份运行。

还有第四个守护进程 OPRCD，它仅在不使用供应商集群软件与 CRS 的平台上出现。OPRCD 是集群的进程监视器。无论运行多少个 Oracle 实例，每个节点上都只有一个这样的守护进程集在运行。

每个守护进程都有一个日志文件集，位于以下位置：

| 守护进程 | 日志文件位置 |
|---|---|
| CRSd | $CRS_HOME/crs/log |
| EVMD | $CRS_HOME/evm/log |
| OCRD | $CRS_HOME/ocr/log |

CRS 在系统每次重启时都会自动启动。DBA 或系统管理员也可以通过执行以下命令手动停止和启动 CRS：

```
/etc/init.d/init.crs start
/etc/init.d/init.crs stop
```

CRS 需要投票磁盘和 OCR，如果其中任何一个文件不可用，CRS 将无法启动。CRS 必须处于运行状态，然后 Oracle RAC 实例才能挂载。CRS 需要三个网络地址：公共 IP 地址、私有互连 IP 地址和虚拟 IP 地址 (VIP)。在安装 CRS 之前，必须在 DNS 中设置 VIP 和公共地址。

查看 CRS 状态的命令是 crs_stat。该命令输出的格式难以阅读，因此我建议运行脚本以更好地格式化输出。以下是示例脚本，可将 crs_stat 二进制文件的输出以更易读的形式返回。

```
crs_stat.sh
#!/usr/bin/ksh

# Sample 10g CRS resource status query script
#
# Description:
# - Returns formatted version of crs_stat -t, in tabular
#   format, with the complete rsc name and filtering keywords
# - The argument, $RSC_KEY, is optional and if passed to the script, will
#   limit the output to HA resources whose names match $RSC_KEY.

# Requirements:
# - SORA_CRS_HOME should be set in your environment
RSC_KEY=$1
QSTAT=bu
AWK=/bin/awk # if not available use /usr/bin/awk
# Table header:echo **
$AWK \
'{BEGIN {printf "%-45s %-10s %-18s\n", "HA Resource", "Target", "State";
printf "%-45s %-10s %-18s\n", "-------------------", "-------", "------";}
# Table body:
SORA_CRS_HOME/bin/crs_stat $QSTAT | $AWK \
'{BEGIN { FS="*"; state = 0; }
$1~/NAME/ && $2-~/\$RSC_KEY/ { appname = $2; state=1;}
state == 0 {next;}
$1~/TARGET/ && state == 1 {apptarget = $2; state=2;}
$1~/STATE/ && state == 2 {appstate = $2; state=3;}
state == 3 {print "%-45s %-10s %-18s\n", appname, apptarget, appstate; state=0;}'
```

## 服务和自动工作负载管理

使用 Oracle 10g，应用程序工作负载可以定义为服务，以便可以单独管理和控制。DBA 控制在正常操作期间以及响应故障时分配给每个服务的处理资源。可以按服务跟踪性能指标。可以设置阈值，以便在超过这些阈值时自动生成警报。这些服务的资源消耗控制和 CPU 资源分配由 Resource Manager 管理。Oracle 设施和工具（如 Parallel Query、Job Scheduler 和 Oracle Streams Advanced Queuing）也使用服务来管理其工作负载。

工作负载共享配置可以以多种不同的方式定义。例如，假设您有一个五节点 RAC 集群，其中两个实例 A 和 B 作为 OracleAS 10g 应用程序的首选实例。同一个集群可以有实例 C、D 和 E 作为客户关系管理 (CRM) 应用程序的首选实例。如果 CRM 的一个或多个首选实例变得不可用，则实例 A 和 B 是 CRM 的可用实例。如果 AS 10g 的一个或多个首选实例变得不可用，则实例 C、D 和 E 是 AS 10g 的可用实例。此配置使每个服务都可以使用一组实例，该组实例既充当首选实例，也充当可用恢复实例。故障后，客户端在其同一组中的另一个实例上恢复其连接。使用此配置，在正常操作期间，RAC 按服务将应用程序会话路由到单独的实例组。如果首选实例变得不可用，则 CRS 在提供该服务的剩余 RAC 实例之间重新定位连接。工作负载管理的配置通过根据服务路由连接来实现最高性能和可用性。一个域上的计划内和计划外中断可以与其他域隔离，并且受影响的服务可以单独恢复或升级。
