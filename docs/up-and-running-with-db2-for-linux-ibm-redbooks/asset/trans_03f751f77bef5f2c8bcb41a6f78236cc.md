

11:09:13 AM      190.00
11:09:15 AM     1013.50
11:09:17 AM     1349.00
11:09:19 AM     2071.00
11:09:21 AM     2132.00
11:09:23 AM     1643.50
11:09:25 AM     2194.00
Average:        1399.83

[root@UDBLNX06 root]# sar -n DEV -s 11:09:25 -f sartest.bin|egrep "eth0|IFACE"
11:09:25 AM     IFACE       rxpck/s   txpck/s    rxbyt/s    txbyt/s
11:09:27 AM     eth0     1187.00   2459.00   1511133.00   3007010.50
11:09:29 AM     eth0     1218.00   2528.50   1558313.00   3078301.00
11:09:31 AM     eth0     1219.00   2534.00   1558488.00   3085869.00
11:09:33 AM     eth0     1209.00   2504.50   1541410.50   3051547.50
11:09:35 AM     eth0     1181.00   2502.50   1504659.50   3050603.50
Average:        eth0     1202.80   2505.70   1534800.80   3054666.30

如第 6.3.3 节第 250 页所述的 “Iostat”，sar 工具包含在 sysstat 软件包中；在使用此命令之前，您需要确保 sysstat 软件包已安装在您的系统中。

有关使用 sar 命令的详细信息，请参阅 sar 的 man 帮助页或其它 Linux 文档。

## 6.3.5 其他系统监控工具

还有大量可用于监控 Linux 系统资源使用的 Linux 系统监控工具可供使用，例如几乎人人都知道的 ps 命令用于报告进程状态，pstree 可用于显示进程树，netstat 用于打印网络相关信息，nfsstat 用于 NFS 特定统计信息，等等。此外，pgrep 和 pkill 命令在您想要根据进程名称和其他进程属性查找或向进程发送信号时非常有帮助。如果您喜欢带有图形用户界面的监控工具，gnome-system-monitor 和 ksysguard 等实用程序也可以使用。有关更多信息，请参阅 Linux 特定文档。

## DB2 集成工具和向导

本章讨论了 Linux 平台上用于管理和开发目的的一些 DB2 集成工具。DB2 UDB 提供了大量工具，使安装和管理数据库系统、持续管理不断增长的数据量、处理用户数量的巨大增长、提供更好的性能并支持不同类型的应用程序等变得更加容易和高效。

除了 GUI 工具之外，DB2 还提供了许多命令行工具来帮助您管理数据库系统，例如您可以使用 DB2 命令行处理器执行 DB2 管理命令和 SQL 语句，使用 db2mtrk 按实例和数据库跟踪 DB2 内存使用情况，以及 db2 代理，并使用 db2look 提取重现数据库对象所需的 DDL 语句。

一些工具和向导已在本书记其它章节中讨论过，如表 7-1 第 256 页所示。有关这些工具和向导的信息，请参阅相关章节。

## 表 7-1 本书其它章节中涵盖的工具和向导

| Tool/Wizard | Usage | Chapter Number |
|---|---|---|
| db2setup | DB2 installation and instance creation | 2 |
| db2_install | DB2 package installation | 2 |
| Configuration Advisor | DB2 instance and database parameter configuration | 3 |
| Command Center | GUI tool for db2 commands and SQL statements execution | 3 |
| License center | Manage db2 licenses information | 3 |
| Backup/Restore | Database backup and recovery | 5 |
| Reorg | Reorganize table and indexes | 5 |
| Runstats | Statistics information collection | 5 |
| Export/Import | Table data export and import | 5 |
| Load | Load data into database | 5 |
| Task Center | Task setup and scheduling | 5 |
| Health Center | System health monitor configuration | 6 |
| Development Center | Integrated tool for stored procedure, UDF development | 8 |

在本章中，我们挑选了几个工具和向导进行详细讨论。有关完整的 DB2 UDB 工具和向导集合，请参阅 IBM DB2 UDB Guide to GUI Tools for Administration and Development，SC09-4851。该书侧重于介绍 GUI 工具，并涵盖了许多工具。此外，您还可以阅读 IBM DB2 UDB Command Reference V8，SC09-4828，以获取有关系统和 DB2 CLP 命令提供的工具和实用程序的更多信息。

通常，要在 Linux 平台的 DB2 UDB 中调用 GUI 工具，您可以从 DB2 控制中心启动它们。要启动 DB2 控制中心，请单击 Linux 桌面上可用的控制中心图标，或从命令行输入命令 “db2cc”，然后按回车。大多数 GUI 工具可以从控制中心调用，如图 7-1 所示；有一个工具菜单可供您选择所需的工具。此外，如果您单击工具菜单中的 “Wizards...” 项目，将会弹出另一个包含向导选择的窗口

