
## Example 4-7 Migrating the database

```
db2inst1@udblnx02:"/sqllib/db2dump> db2 migrate database itsodb
SQL1103W  The Migrate Database command processing was successful.
```

## 7. 更新统计信息。

DB2 Version 8 有一些统计信息在 DB2 的早期版本中已修改或不存在。为了利用这些统计信息，您可能希望在表上运行 `runstats` 命令，特别是对 SQL 查询性能至关重要的表。`runstats` 命令更新有关表及其相关索引的物理特征的统计信息。优化器使用这些统计信息来找到访问数据的最佳路径。

## 8. 重新绑定包。

迁移期间存储在数据库中的任何包都会失效，但在迁移后 V8 数据库管理器首次使用它们时会被重建。迁移后，运行 `db2rbind` 命令以重新绑定这些包。

## 9. 迁移 DB2 Explain 表。

`migrate database` 命令不会迁移 explain 表。如果您想保留之前收集的 explain 表信息，请执行此任务。如果您不想保留此信息，可以稍后重新创建 explain 表并收集新信息。要迁移 explain 表，请使用 `db2exmigr` 命令，如下所示：

```
db2exmigr -d <database_name> -e <explain_schema> [-u userid password]
```

其中，`database_name` 是存储 explain 表的数据库的名称，`explain_schema` 表示要迁移的 explain 表的模式名称，`userid` 和 `password` 是当前用户的 ID 和密码。`userid` 和 `password` 参数是可选的。

`db2exmigr` 命令执行以下操作：

- 重命名 V6/V7 explain 表。
- 使用 EXPLAIN.DDL 创建一组新的 explain 表。此 EXPLAIN.DDL 位于 `$INSTHOME/sqllib/misc` 目录下。
- 将旧表的内容复制到新表。
- 删除旧的 explain 表。

## 10. 比较迁移前后的 DBM 和 DB 配置设置，以及表空间和包记录，以验证迁移是否成功。

### 4.3.3 多分区迁移

要迁移分区数据库系统，你需要 (1) 在每台机器上安装新的 DB2 V8 服务器，(2) 在实例拥有机器上迁移实例，(3) 在目录节点上迁移数据库，以及 (4) 在分区数据库系统中的每台物理机器上创建新的 V8 DAS。

### 4.3.4 迁移 DB2 管理服务器

在 Version 8 中，DB2 Administration Server (DAS) 已发生重大变化。它不再是一个实例；相反，它现在是一个服务。在分区数据库系统中，通常在集群中的每台机器上运行一个单独的 DAS 服务。这允许每台机器充当从 Control Center 或 Configuration Assistant 发出到实例的请求的协调节点。这减少了当一个管理协调节点分布在实例的多个分区中时存在的开销，并有助于平衡传入连接。由于这些变化，在将 DB2 迁移到 Version 8 时，有几件事需要注意。

- 不要使用现有的 DAS 用户（例如 V7 DAS 用户 `db2as`）用于 Version 8。你必须为 Version 8 DAS 创建一个新的 DAS 用户。
- 如果 V7 和 V8 服务器安装不共存于同一台机器，则在迁移到 Version 8 之前先删除 V7 DAS 实例。但是，如果你想将 V7 脚本和计划迁移到 V8 工具目录，则不要删除 V7 DAS。如果是这种情况，仅在安装 DB2 V8、创建 V8 工具目录并运行 `dasmigr` 命令后才删除 V7 DAS。
- 如果 V7 和 V8 服务器安装要共存，则 V7 DAS 用于管理 V7 实例，而 V8 DAS 用于管理 V8 实例。V8 DAS 只能在端口 523 上运行；因此，V7 DAS 必须在私有端口上运行。要在私有端口上设置 V7 DAS，请执行以下步骤：
  - a. 以 V7 DAS 用户身份登录。
  - b. 通过发出 `db2admin stop` 停止 DB2 Administration Server。
  - c. 通过将其设置为空来取消设置 Version 7 DB2ADMINSERVER 注册表值：
    `db2set DB2ADMINSERVER=`
  - d. 通过输入以下命令更新端口号：
    `db2 update dbm cfg using SVCENAME <port_number>`
    其中 `port_number` 是分配给 V7 DAS 的新端口号。
  - e. 将 V7 DB2ADMINSERVER 注册表变量重置为 Version 7 DB2 Administration Server 实例名。例如：
    `db2set DB2ADMINSERVER=db2as`
  - f. 通过发出 `db2admin start` 重新启动 DB2 Administration Server。
  - g. 使用 Control Center，在客户端编目一个新的管理节点以使用 V7 DAS。

### 迁移 V7 脚本和计划

如果你想在 DB2 Version 8 中使用现有的 pre-V8 脚本和计划（在旧 DAS 中创建），你将需要使用 `dasmigr` 命令迁移 DAS。迁移 DAS 将把这些脚本和计划迁移到新的 V8 DB2 工具目录。在执行此任务之前，你需要有一个现有的 V8 DB2 工具目录。如果你尚未创建工具目录，请参阅第 2.3.3 节，“db2_install utility” 第 68 页以获取说明。要迁移 DAS，请按照以下流程操作：

1. 以 root 用户身份登录。
2. 进入：`/opt/IBM/db2/V8.1/instance`
3. 输入命令：
   `dasmigr previous_das_name new_das_name`
   其中 `previous_das_name` 表示 pre-V8 DAS 实例的名称，而 `new_das_name` 表示新的 V8 DAS 的名称。
   例如，我们将旧 DAS `db2as` 迁移到新的 DAS `dasusr1`：
   `./dasmigr db2as dasusr1`
4. 我们在旧 DAS（`db2as`）中创建的脚本已迁移到新的 DAS。默认情况下，脚本和计划放在 `/db2home/dasusr1/das/tmp/migr/` 目录中，并由 Task Center 管理。

#### 4.3.5 客户端和服务器兼容性

请注意以下 DB2 Version 7 和 Version 8 客户端和服务器兼容性限制：

- 避免让 V8 客户端访问 V7 服务器。存在已知的限制且有文档记录，并且可能存在一些未知限制。
- 你可以使用 V7 32 位客户端访问 V8 32 位服务器，但如果你想使用 DB2 GUI 工具（例如 Control Center、Health Center 等）或数据库命令（例如 BACKUP、RESTORE）针对 V8 服务器，则需要 V8 客户端。

## 管理数据库

本章包含有关 Linux 平台上 DB2 UDB 的一些重要数据库维护任务的信息，例如数据库备份与恢复、表和索引重组，以及通过实用程序（如 `export`、`import` 和 `load` 等）进行数据移动。以下将讨论这些主题：

- 数据库备份与恢复

我们讨论了选择数据库和表空间恢复方法时要考虑的因素，包括备份和恢复数据库或表空间，以及使用前滚恢复。我们还讨论了实用程序的基本用法，例如 `BACKUP`、`RESTORE`、`ROLLFORWARD` 等。

- 表和索引重组及统计信息收集

我们讨论了 `REORG` 实用程序，它可用于对表和索引所占用的数据页进行碎片整理，以及用于统计信息收集的 `RUNSTATS` 实用程序，还有 `REBIND` 任务，以使最新的统计信息适用于现有包。我们还讨论了可用于表和索引重组的各种方法。

- 通过 EXPORT、IMPORT 和 LOAD 进行数据移动

我们讨论了可用于在表或数据库之间或其他所需格式之间移动数据的实用程序；例如，将数据导出为电子表格程序格式或采用 ASC、DEL 或 IXF 等格式的操作系统文件。在本节中，我们还讨论了 `LOAD` 实用程序，特别是新增的在线加载功能，该功能现在仅在表级别获取锁。这些新的加载功能显著提高了数据的可用性，帮助客户应对大数据量的维护，并减少了所需的维护窗口时间。

- 使用任务中心进行作业调度

我们讨论了使用任务中心进行作业调度，并提到了 DB2 工具编目数据库（DB2 Tools Catalog Database），该数据库在 DB2 UDB Version 8 中引入，用于存储与调度相关的数据。

### 5.1 DB2 数据库备份与恢复
