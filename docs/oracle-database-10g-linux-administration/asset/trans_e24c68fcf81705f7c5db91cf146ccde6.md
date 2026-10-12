
## 逻辑备用数据库配置

与物理备用数据库的配置类似，逻辑备用数据库的配置可分为三个阶段：准备阶段、配置阶段和配置后阶段。逻辑备用数据库的先决条件比物理备用数据库更严格。

### 准备

在开始创建逻辑备用数据库之前，您应检查先决条件。在此配置中，某些数据类型不受支持。不支持的数据类型包括 BFILE、ROWID、UROWID、REFS、varrays、嵌套表、XML 类型和用户定义的数据类型。如果您在表中使用了这些数据类型中的任何一种，这些表将被 SQL Apply 跳过。如果需要，请在开始配置逻辑备用数据库之前更改主数据库上的数据类型。除了被跳过的数据类型外，还有许多表、序列和视图，以及 DDL 语句（包括尤其是 ALTER DATABASE、ALTER SESSION 和 ALTER SYSTEM）也将被跳过，包括：

- 随 Oracle 数据库一起提供的多数模式
- 使用不支持数据类型的表
- 使用表压缩的表

Oracle PL/SQL 提供的修改系统元数据的包通常不被 SQL Apply 支持。此类包的示例包括 DBMS_JAVA、DBMS_REGISTRY、DBMS_ALERT、DBMS_SPACE_ADMIN、DBMS_REFRESH、DBMS_SCHEDULER 和 DBMS_AQ。

要确定主数据库是否包含任何不支持的对象，请查询 DBA_LOGSTDBY_UNSUPPORTED 视图。与物理备用数据库不同，后者中数据库中每个记录的 ROWID 都是相同的，而逻辑备用数据库中的 ROWID 可能会不同。因此，您必须使用不同的机制将备用数据库上更新的行与主数据库上的行进行匹配。这可以通过主键或唯一索引来实现。

### 部署

创建逻辑备用数据库的第一步是按照本章前面的步骤创建物理备用数据库。此外，您必须确保主数据库上已启用补充日志记录。如果尚未启用补充日志记录，可以通过 ALTER DATABASE ADD SUPPLEMENTAL LOG DATA (PRIMARY KEY, UNIQUE INDEX) COLUMNS 语句启用。这会创建 SQL Apply 服务将使用的额外日志数据。
完成这些步骤后，您即可通过执行以下步骤激活逻辑备用数据库：

1. 通过设置在角色反转时生效的初始化参数，为角色转换准备主数据库和备用数据库。在主数据库和备用数据库上，设置 LOG_ARCHIVE_DEST_1,2,3 和 LOG_ARCHIVE_DEST_STATE_1, 2, 3，以及 UNDO_RETENTION=3600（用于 LogMiner 字典）。在备用数据库上，设置 PARALLEL_MAX_SERVERS=9。（最小值）。在备用数据库上发出 SHUTDOWN IMMEDIATE。
2. 使用 ALTER DATABASE CREATE LOGICAL STANDBY CONTROLFILE AS 'filename'; 创建逻辑备用控制文件；
3. 在备用数据库上，发出 STARTUP MOUNT PFILE=<cpfile>;
4. 通过运行 SQL 语句 ALTER DATABASE RECOVER MANAGED STANDBY DATABASE 为 SQL Apply 准备备用数据库。
5. 通过运行 SQL 语句 ALTER DATABASE ACTIVATE STANDBY DATABASE 激活逻辑备用数据库。
6. 运行 nid (DBNEWID) 实用程序以更改备用服务器上数据库的名称（需要 SHUTDOWN IMMEDIATE 和 STARTUP MOUNT）。
7. 将参数文件中的数据库名称 DB_NAME 更改为 DBNEWID 中使用的名称。
8. 为逻辑备用创建 SPFILE，并使用 ALTER DATABASE OPEN RESETLOGS 重启数据库。
9. 使用 SQL 语句 ALTER DATABASE RENAME GLOBAL_NAME TO newname 更改备用数据库的全局名称。
10. 如同为物理备用数据库所做的一样，创建新的临时文件。
11. 使用 SQL 语句 ALTER DATABASE START LOGICAL STANDBY APPLY 启动 SQL Apply。

### 部署后

一旦创建了基本的物理备用数据库，还可以执行一些可选任务。当然，这包括测试备用数据库。可以通过多种方式监控备用数据库。这些包括以下 Oracle 表和动态性能视图：

- **DBA_LOGSTDBY_LOG**  该表提供有关在备用系统上注册的重做日志文件的信息。
- **DBA_LOGSTDBY_PROGRESS**  该表提供 SQL Apply 整体进度的统计信息。
- **V$LOGSTDBY_STATS**  该视图提供 LogMiner 统计信息。
- **V$LOGSTDBY**  提供有关日志应用进程的信息快照。

与物理备用数据库一样，您可以更改数据保护模式。这些是与物理备用数据库（前面已描述）一起使用的相同数据保护模式，即最大保护、最大可用性和最大性能。

除了设置数据保护模式外，测试和验证备用数据库的操作始终是一个好主意。

### 摘要

除了此处提供的信息外，使用 Oracle Data Guard 还可以配置和调整更多内容。有许多选项和许多操作模式可以配置。您如何配置系统取决于您的需求和要求。与许多 Oracle 功能（如 Oracle RAC）一样，在 Linux 环境中部署 Data Guard 完全取决于细节。仔细的规划和测试将使您的部署成功。

![](img/9479df2d00f5e62b87366b125224950f_370_0.png)

## 第 14 章

Oracle Linux 上的高级复制

复制是将数据库、表或这些或其他 Oracle 对象的子集自动复制到另一系统的过程。复制可以配置为在整个数据库或仅数据库的子集上工作。无论要复制的数据量多少，功能和机制都相同。本章将探讨 Oracle 用于将数据从一个系统复制到另一个系统的各种方法。

虽然最终结果可能看起来与 Oracle Data Guard 相似，但复制实际上完全不同。复制旨在创建数据库或数据库子集的一个或多个副本。这些副本旨在对用户开放并可供使用。复制也可以以双向方式使用，其中存在多个主节点。Data Guard 设计为灾难恢复系统，而复制主要并非为 DR 设计。Data Guard 通过从主系统向备用系统传输和应用重做数据来工作，而复制基于 API 或触发器。

![](img/9479df2d00f5e62b87366b125224950f_371_0.png)

**NOTE**
虽然 Data Guard 需要 Oracle 企业版，但复制随标准版提供。

## Oracle 复制简介

Oracle 高级复制由协同工作以在整个企业中的不同系统上配置、部署和维护数据库对象的进程和实用程序组成。复制对象可以驻留在与源数据库相同的计算机系统上的数据库中，也可以驻留在相距数千英里的系统上。复制对象可以根据您的需求和偏好配置为只读或读写。高级复制是 Oracle 的复制实现。在本章中，术语复制将用于描述高级复制。

Oracle 高级复制用于多种目的。它可用于复制必须在远程位置（如商店）本地可用的只读数据。以这种方式，您可以将价格数据、零件详情、文档等复制到每家商店，在那里即使网络问题可能阻止与主数据中心的通信，这些数据也可以随时可用。这些数据可以在每家商店中自主使用，只有销售数据需要发送回主数据中心。这将允许商店在网络中断或主公司系统出现问题时继续运行。

除了可用性之外，在这种情况下，复制还可以提供更高的性能，因为数据位于本地并且可以快速访问由
