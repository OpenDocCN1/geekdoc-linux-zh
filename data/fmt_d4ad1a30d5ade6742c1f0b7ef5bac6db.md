
正如我们的示例所示，`db2pd`命令是用于确定问题的极其强大的工具。使用`db2pd -h`查看所有选项。

更多示例和信息请参见《故障排除指南》(Troubleshooting Guide) GI11-7857，以及《DB2 Linux, UNIX 和 Windows 命令参考》SC23-5846-01。

## 7.5.3 DB2 snapshot 命令

与`db2pd`命令类似，你可以使用快照监控器在特定时间捕捉数据库及任何连接应用程序的信息。如果你定期间隔捕捉信息，快照对于观察趋势和不可预见的潜在问题也很有用。有多种快照请求类型，每个快照请求返回特定类型的监控数据。

在分区数据库环境中使用该命令时，可以在实例的任何分区或全局拍摄快照。全局快照聚合了在每个分区收集的数据并返回一组单一的值。示例 7-21 通过两个样本显示了差异。

### 示例 7-21 全局快照

```
db2inst1@mensa:> db2_all 'db2 get snapshot for all on itsoddb | grep 'Locks held currently'

Locks held currently = 1
mensa: db2 get snapshot for ... completed ok

Locks held currently = 8
gemini: db2 get snapshot for ... completed ok

db2inst1@mensa:> db2 get snapshot for all on itsoddb global | grep "Locks currently"
held currently = 9

db2inst1@mensa:> db2_all 'db2 get snapshot for all on itsoddb | grep "Lock list*'

Lock list memory in use (Bytes) = 5888
mensa: db2 get snapshot for ... completed ok
Lock list memory in use (Bytes) = 3392
gemini: db2 get snapshot for ... completed ok

db2inst1@mensa:> db2 get snapshot for all on itsdb global | grep "Lock list"
Lock memory in use (Bytes) = 9280
```

在 6.2.2 第 280 页“手动表维护”中，我们使用了 DB2 命令行 (CLP) 的 GET SNAPSHOT 命令来监控就地表重组。你可以从管理视图、SQL 表函数或通过在 C 或 C++ 应用程序中使用快照监控 API 来捕捉快照。

有多个快照管理视图供你查询快照信息。示例 7-22 显示了列表。

### 示例 7-22 Snapshot™ 管理视图

```
db2inst1@mens:> db2 select substr(tabchema,1,10) tabschema, substr(tabname,1,30) tabname from syscat.tabname like 'SNAP*'
```

| SYBSCHEMA | TABNAME |
|---|---|
| SYBSIMADM | SNAPAGENT |
| SYBSIMADM | SNAPAGENT_MEMORY_POOL |
| SYBSIMADM | SNAPAPPL |
| SYBSIMADM | SNAPAPP_INFO |
| SYBSIMADM | SNAPBP |
| SYBSIMADM | SNAPBP_PART |
| SYBSIMADM | SNAPCONTAINER |
| SYBSIMADM | SNAPDB |
| SYBSIMADM | SNAPDBM |
| SYBSIMADM | SNAPDB_MEMORY_POOL |
| SYBSIMADM | SNAPDB_MEMORY_POOL |
| SYBSIMADM | SNAPDETA |
| SYBSIMADM | SNAPFCM |
| SYBSIMADM | SNAPFCM_PART |
| SYBSIMADM | SNAPHOR |
| SYBSIMADM | SNAPLOCK |
| SYBSIMADM | SNAPWAIT |
| SYBSIMADM | SNAPSTMT |
| SYBSIMADM | SNAPSTORAGE_PATHS |
| SYBSIMADM | SNAPSECTION |
| SYBSIMADM | SNAPSWT |
| SYBSIMADM | SNAPTAB |
| SYBSIMADM | SNAP_REORG |
| SYBSIMADM | SNAPBSP_PART |
| SYBSIMADM | SNAP_QUIES |

`db2ls`命令列出系统上安装 DB2 产品的路径以及 DB2 产品级别。要获取有关系统中已安装的每个 DB2 产品的更多信息，您可以使用示例 7-26 所示的命令。

### 示例 7-26 列出产品信息

```
db2inst@mensa:/dbhome/db2inst> db2ls -q -p /opt/ibm/db2/V9.5
```

安装路径：`/opt/ibm/db2/V9.5`

| 产品响应 ID | 级别 | 补包 | 产品描述 |
| :--- | :--- | :--- | :--- |
| ENTERPRISE_SERVER_EDITION | 9.5.0.0 | 0 | DB2 企业版 |

```
db2inst@mensa:/dbhome/db2inst> db2ls -q -b /opt/ibm/db2/V9.5
```

安装路径：`/opt/ibm/db2/V9.5`

| BASE_CLIENT | 级别 | 补包 | 功能描述 |
| :--- | :--- | :--- | :--- |
| BASE_CLIENT | 9.5.0.0 | 0 | 基础客户端支持 |
| JAVA_SUPPORT | 9.5.0.0 | 0 | Java 支持 |
| SQL_PROCEDURES | 9.5.0.0 | 0 | SQL 过程 |
| BASE_DB2_ENGINE | 9.5.0.0 | 0 | 基础服务器支持 |
| JDK | 9.5.0.0 | | 用于 Java(TM) IBM DB2 开发工具包 (SDK) |
| CONNECT_SUPPORT | 9.5.0.0 | 0 | 连接支持 |
| COMMUNICATION_SUPPORT_TCPIP | 9.5.0.0 | 0 | 通信支持 - TCP/IP |
| REPL_CLIENT | 9.5.0.0 | 0 | 复制工具 |
| CONTROL_CENTER | 9.5.0.0 | 0 | 控制中心 |
| DB2_DATA_SOURCE_SUPPORT | 9.5.0.0 | 0 | DB2 数据源支持 |
| LDAP_EXPLOITATION | 9.5.0.0 | | DB2 LDAP 支持 |
| INSTANCE_SETUP_WIZARD | 9.5.0.0 | | DB2 实例设置向导 |
| XML_EXTENDER | 9.5.0.0 | 0 | XML 扩展 |
| APPLICATION_DEVELOPMENT_TOOLS | 9.5.0.0 | 0 | 基础应用开发工具 |
| FIRST_STEPS | 9.5.0.0 | 0 | 入门指南 |
| DB2_SAMPLE_DATABASE | 9.5.0.0 | 0 | 示例数据源 |

## 7.5. db2support

`db2support`实用程序旨在自动收集所有的 DB2 和系统诊断数据。该程序生成有关 DB2 服务器的信息，包括其配置和系统环境信息。该程序的输出存储在一个名为`db2support.zip`的压缩文件中，该文件位于命令行处理器下调用的命令时指定的目录中。通过一步操作，该工具可以收集数据库管理器快照、配置文件和操作系统参数，这可以帮助您更快地确定问题。

您可以使用命令`db2support -h`显示完整的命令选项列表。以下调用通常足够收集诊断问题所需的大部分信息：

```
db2support outputpath -d dbname
```

例如，执行以下命令来收集数据库 ITS0DB 的信息：

```
db2support -d ITS0DB
```

压缩文件`db2support.zip`位于当前目录。您可以将此文件发送给您的 DB2 技术服务代表进行分析。

> 注意：如果使用`-c`选项，实用程序将建立与数据库的连接。

## 7.6 Linux 系统监控工具

有许多可用的 Linux 系统监控工具可以帮助识别性能或系统设置问题发生的地方。您可以使用这些工具监控系统资源使用情况，例如磁盘 I/O、内存消耗、CPU 活动和网络状态。通过利用这些操作系统工具提供的综合信息，结合 DB2 的数据库系统工具，您可以更清楚地了解您的系统。例如，您可以识别哪些空间容器正处于高 I/O 压力下、过多的排序堆内存（sort heap）分配是否是导致大量分页空间活动的瓶颈、网络带宽是否导致了客户端应用程序响应时间变差等。然后，您可以对应用程序、数据库系统或操作系统进行相应调整，以提高系统性能。

在本节中，我们将讨论 Linux 平台上最常用的监控工具：`iostat`、`vmstat`和`sar`。

### 7.6.1 top 实用程序

`top`实用程序是一个非常有用的工具，可以在一个屏幕上提供大量信息。`top`可以显示哪个进程占用了最多的处理器时间（百分比）和最大的内存（百分比），以及系统运行的时间和空闲内存。默认情况下，该实用程序每 3.0 秒刷新一次显示。您可以通过命令选项`-d`覆盖默认刷新间隔。用户需要注意，`top`命令没有正确报告用于 DB2 的总内存。`top`会通过多次计算共享内存来高估内存使用量。

> 注意：在 Linux 中，DB2 不会自动释放内存。要释放共享内存，您需要重启 DB2。

表 7-1 列出了`top`的选项：

| 选项 | 描述 |
| :--- | :--- |
| d | 指定更新间隔。 |
| i | 仅显示运行中的进程。 |
| n | 启动时不显示空闲行。 |
| q | 退出。 |
| f | 配置显示字段。 |
| A | 按年龄排序。 |
| P | 按 CPU 排序。 |
| M | 按内存占用排序。 |
| W | 将输出写入文件。 |

关于`top`输出字段的描述，请参考帮助页面。另一个使用`top`监控指定进程的示例：

```
top -d -p 1785,2928
```

您可以为`top`指定多达 20 个进程。在示例中，我们使用`-p`命令获取 db2samp 的 ID。

以下列表显示了`vmstat`生成的输出报告的字段描述。要获取有关此命令的更多信息，请参阅`vmstat`的帮助页面或其他 Linux 文档：

- 进程（Procs）：
  - r: 等待运行的进程数
  - b: 处于不可中断睡眠状态（Uninterruptible sleep）的进程数
  - w: 已交换出但仍在等待的进程数
- 内存（Memory）：
  - swpd: 使用的虚拟内存量 (kB)
  - free: 空闲内存量 (kB)
  - buff: 作为缓冲区使用的内存 (kB)
- 交换（Swap）：
  - si: 从磁盘交换入内存的量 (kB/s)
  - so: 从内存交换磁盘的量 (kB/s)
- I/O：
  - bi: 发送到块设备的块数 (blocks/s)
  - bo: 从块设备接收的块数 (blocks/s)
- 系统（System）：
  - in: 每秒中断次数（包括时钟中断）
  - cs: 每秒上下文切换次数
- CPU：
  - us: 用户时间
  - sy: 系统时间
  - id: 空闲时间

示例 2-29 显示了由`vmstat`生成的示例报告。命令`vmstat 2 10`显示了 10 次虚拟内存统计，间隔为 2 秒。

### 示例 2-29 使用 `vmstat` 观察虚拟内存统计

```
$db2inst1@home/db2inst1$ vmstat 2 10
procs -----------memory---------- --swap----io---- -system -cpu-----
r b swpd free buff cache si so bo in cs us sy wa st
0 0 618568 274036 2838968 0 0 6 24 13 0 0 99 1 0
0 0 618568 274036 2838968 0 0 0 38 624 3 1 0 99 1 0
0 0 618568 274036 2838968 0 0 0 12 621 2 1 0 100 0
0 0 618568 274036 2838968 0 0 0 36 616 301 0 100 0
0 0 618568 274036 2838968 0 0 0 50 792 529 0 98 2 0
0 0 618568 274036 2838968 0 0 0 24 613 293 0 100 0
0 0 618568 274036 2838968 0 0 0 24 624 310 0 99 1 0
0 0 618578 274036 2838968 0 0 0 36 614 301 0 100 0
```

418 在 Linux 上运行 DB2 *

### 7.6.3 iostat

`iostat`命令用于报告中央处理单元（CPU）统计数据，并监控设备和分区的系统 I/O 设备统计数据。你可以使用`iostat`命令生成的报告来帮助你更改系统配置，以便更好地平衡跨物理磁盘的 I/O 负载。

> 注意：`iostat`命令包含在`sysstat`软件包中（该软件包也包含在此内）。在使用这些命令之前，你需要安装此软件包。

`iostat`命令生成的第一份报告提供了有关自系统启动以来的统计信息。随后的每份报告都涵盖了自上一份报告生成以来的时间段。

你可以配合`iostat`命令使用几个非常有用的选项。例如，使用`-k`以千字节而不是块显示统计数据，使用`-x`获取设备的扩展统计信息，使用`-t`打印显示的每份报告的时间等。更多详细信息，请参阅`iostat`的 man 页或 Linux 文档。

示例 7-30 显示了使用`iostat`命令监控 CPU 和设备 I/O 统计数据。`iostat 2`命令显示当前的 CPU 负载平均值和磁盘 I/O 信息 5 次，间隔为 2 秒。

```
Example 7-30 Using iostat to get CPU and I/O statistics
db21@mensa:/db2home/db21$ iostat 2 5
Linux 
avg-cpu:     user     system    idle     iowait     %steal     softq
             0.00      0.00    99.46      0.00      0.00      0.00

             0.00      0.00    99.54      0.00      0.00      0.00 
device:               r/s  w/s  kB_read  kB_w  kB_read/s  kB_w/s  sz  ..ra-  
sda      0.00     0.00       0.00       0.00      0.00      0.00   0   0.00  0.00 
sdb      0.00     0.00       0.00       0.00      0.00      0.00   0   0.00  0.00 
```

| | | | | | | | | | |
|---|---|---|---|---|---|---|---||}{|
| 14:35:26 | 1.00 | | | | | | | | |
| 平均: | 0.80 | | | | | | | | |
| 14:34:46 | 14:34:51 | 787.03 | | | | | | | |
| 14:34:56 | 1479.36 | | | | | | | | |
| 14:35:01 | 617.80 | | | | | | | | |
| 14:35:06 | 1562.20 | | | | | | | | |
| 14:35:11 | 600.60 | | | | | | | | |
| 14:35:16 | 1559.92 | | | | | | | | |
| 14:35:21 | 627.29 | | | | | | | | |
| 14:35:26 | 1510.82 | | | | | | | | |
| 平均: | 1092.50 | | | | | | | | |
| mensa/tmp # sar -n DEV -s 14:36:00 - fartest.bin|egreg eth0|IFACE | IFACE | rxkpc | tpcks | rxubyt | txbyt | rxcmp | rxmcst | rxmcst |
| 14:36:06 | eth0 | 883.40 | 1207.60 | 62838.40 | 147150.20 | 0.00 | 0.00 | 0.00 |
| 14:36:11 | eth0 | 19.80 | 18.60 | 3153.20 | 17137.40 | 0.00 | 0.00 | 0.00 |
| 14:36:16 | eth0 | 832.06 | 1154.51 | 65476.92 | 145219.90 | 0.00 | 0.00 | 0.00 |
