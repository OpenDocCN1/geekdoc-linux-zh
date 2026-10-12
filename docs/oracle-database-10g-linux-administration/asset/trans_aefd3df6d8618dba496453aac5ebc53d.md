
指定比 rcp 或 scp 更大的块大小。在 Linux 系统中，以下命令在将数据文件从一个系统复制到另一个系统时非常高效：

```
dd bs=64k if=<data file spec> | ssh_standby "( dd bs=64K of=<data file spec>)"
```

如果你正在使用 OCFS，请对前述命令进行如下修改：

```
dd -O_DIRECT=64k if=<data spec> | ssh_standby " 
( dd -O_DIRECT=64k of=<data file spec>)"
```

使用 dd 的速度可以比使用 scp 或 rcp 快十倍。

## 为备用数据库创建控制文件

在主数据库上使用 `ALTER DATABASE CREATE STANDBY CONTROLFILE AS '<filename>'` 创建备用控制文件。该备用控制文件将被复制到本节描述的备用数据库系统中。必须在该数据库处于 MOUNT 模式且位于最新备份数据文件时间戳之后创建此备用控制文件。

## 创建备用初始化参数

备用服务器的参数集将与主服务器使用的参数集相似；然而，某些参数的设置有所不同。备用数据库的 `DB_UNIQUE_NAME` 必须与主服务器不同。此外，在备用数据库服务器上，`FAL_CLIENT` 和 `FAL_SERVER` 参数是相反的。特定于 Data Guard 的其他参数包括 `LOG_ARCHIVE_DEST_2`、`LOG_ARCHIVE_DEST_STATE_2`、`LOG_ARCHIVE_CONFIG` 和 `STANDBY_FILE_MANAGEMENT`。

Oracle 10g 的一个新功能是，像 `LOG_ARCHIVE_DEST_2` 这样的参数，以前在角色切换时需要更改，现在具有额外属性来指定它们适用的角色。这使得每个站点都可以使用相同的初始化参数文件（尽管站点之间的文件必须不同），无论数据库角色如何。

**提示**
*创建一个 PFILE 并在初始配置步骤中使用该 PFILE 通常更容易。一旦备用服务器正确设置，就可以创建一个 SPFILE。*

## 将文件复制到备用服务器

接下来，将备份文件（如果你还没有在本章前面所示的备份过程中这样做）、备用控制文件（复制到与主控制文件相同的位置和名称）以及初始化参数文件复制到备用系统。为了创建相同的主站点和备用站点，你还需要复制用于环境设置的初始化脚本（例如 .profile 和其他脚本）以及 DBA 脚本。这些文件可以通过 scp 或 sftp 复制，或者通过挂载 NFS 卷来复制。正如本章前面所述，还应复制 /etc/oratab 文件。除非你正在备用站点上使用 OUI 从头安装 Oracle 10g，否则你还需要将 `ORACLE_HOME` 目录、`admin` 目录（包括子目录 bdump、cdump、create、pfile 和 udump）以及 `/etc/hosts` 文件复制到备用站点（你可能需要为任何专门用于重做流量的新 NIC 在 /etc/hosts 文件中添加新条目）。在将系统配置为 Data Guard 时，网络参数可能很重要。

如前所述，数据文件可以作为备份过程的一部分进行复制，如下所示：

```
dd bs=64k if=<data file spec> | ssh standby "( dd bs=64k of=<data file spec>)"
```

如果你正在使用 OCFS，请对前述命令进行如下修改：

```
dd -O_DIRECT=64k if=<data file spec> | ssh standby "
(dd -O_DIRECT=64k of=<data file spec>)"
```

如前所述，使用 dd 的速度可以比使用 scp 或 rcp 快十倍。

最后，同步 OS 时钟。如果不这样做，以后在比较包含时间戳的日志文件（特别是 alert 日志）时会变得非常混乱，因为它们很可能无法紧密衔接。如果服务器尚未同步，你可能希望系统管理员实施企业范围内的同步软件（例如 NTP），以保持所有服务器时钟始终同步。

## 设置网络环境

一旦所有所需文件都在备用服务器上，请为为主数据库和备用数据库配置监听器的 Oracle 网络服务名进行配置，以供日志传输服务使用。配置文件包括 listener.ora、tnsnames.ora 和 sqlnet.ora 文件。在主站点上，要么使用第二个连接字符串用于当前数据库监听器的重做数据，指定不同的端口；要么创建一个与用于连接主数据库的监听器不同的独立监听器。为了准备角色切换，在两个系统上执行相同的操作。还为 tnsnames.ora 文件中的重做日志传输添加别名。你可能希望在 tnsnames.ora 文件中使用 Oracle Net 参数 SDU（会话数据单元）将传输大小设置为 32k。更多信息，请参阅 *Data Guard Concepts and Administration, 10g Release 1, Section A.6*。为了启用断开的连接检测，按照 Oracle 的建议设置 `SQLNET.EXPIRE_TIME = 2`（分钟）。在配置 Oracle Net 服务时，需要在 sqlnet.ora 文件中设置 `SQLNET.EXPIRE_TIME`。

## 附加步骤

在此时，可以执行以下可选步骤（如果希望的话）：

- 创建备用重做日志（SRLs）。即使是在最大性能模式下，对于所有保护模式，都强烈建议执行此步骤。备用重做日志文件使用 ALTER DATABASE 命令创建，如下所示：

```
SQL> ALTER DATABASE ADD STANDBY LOGFILE THREAD 10
2> ('<log file spec 1>', '<log file spec 2>') SIZE 100M;
```

- 在备用上创建/清理在线重做日志文件，为角色切换做准备（可选）。当备用成为主时，在线重做日志文件会自动为你创建。可以通过在备用系统上创建重做日志文件来提前完成此步骤。通过 `ALTER DATABASE CLEAR LOGFILE` 语句可以非常简单地完成此操作。操作如下：

```
ALTER DATABASE CLEAR LOGFILE GROUP 1;
ALTER DATABASE CLEAR LOGFILE GROUP 2;
...
ALTER DATABASE CLEAR LOGFILE GROUP n;
```

- 启动 DG Broker。通过在两个站点上将初始化参数 `DB_BROKER_START` 设置为 TRUE，在每个站点上启动 Data Guard 监控（DMON）进程。现在你需要创建并启用 broker 配置。

- 启用闪回数据库作为额外保护。

## 启动备用数据库

数据库几乎准备就绪，可以开始作为备用数据库运行；然而，备用数据库需要额外的临时空间。主站点文件上的所有临时表空间和临时数据应在备用站点上创建。你可以使用在备用数据库上从主数据库运行 `ALTER DATABASE BACKUP CONTROLFILE TO TRACE` 生成的文本控制文件中的 `CREATE TEMPORARY TABLESPACE` 命令。要创建临时表空间，需要使用命令 `STARTUP OPEN READ ONLY` 以只读模式启动备用数据库。在此模式下，可以添加到数据库额外的临时文件。

在此时，你可以准备开始备用模式。这是通过发出 SQL 命令 `ALTER DATABASE RECOVER MANAGED STANDBY DATABASE DISCONNECT [FROM SESSION]` 来启动重做应用完成的。`DISCONNECT` 语句使该命令在后台会话中运行。

## 测试备用数据库

通过在主服务器上发出 `ALTER DATABASE SWITCH LOGFILE` 命令并确保重做数据传输并应用于备用服务器，可以测试 Data Guard 日志传输和应用服务。此外，可以使用以下步骤来验证 Data Guard 是否正常工作：

1. 识别备用上的现有归档日志文件：
   - `SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME FROM`
   - `V$ARCHIVED_LOG ORDER BY SEQUENCE#;`

2. 强制主切换日志以归档当前在线重做日志文件：
   - `ALTER SYSTEM ARCHIVE LOG CURRENT;`

3. 验证新的重做数据已在备用上归档：
   - `SELECT SEQUENCE#, FIRST_TIME, NEXT_TIME FROM`
   - `V$ARCHIVED_LOG ORDER BY SEQUENCE#;`

在继续之前，验证 Data Guard 是否正常运行很重要。不要假设一切正常工作。

## 部署后

一旦基本的物理备用数据库创建完成，还可以执行一些额外的可选任务。现在，你应该创建临时数据文件。应创建额外的临时数据文件；每个当前数据库中的临时数据文件对应一个。操作如下：

```
STANDBY> ALTER TABLESPACE TEMP ADD TEMPFILE
'D:\oracle\oradata\stby\temp02.dbf'
SIZE 20M REUSE;
```

新的临时数据文件将在备用成为主的情况下使用。

如果需要，你可以更改数据保护模式。如前所述，这些是可以使用的数据保护模式：

- **最大保护** 在此模式下，事务只有在写入主服务器的重做日志以及至少一个备用重做日志后，才会在主服务器上提交。

- **最大可用性** 此模式类似于最大保护模式；然而，在发生故障的情况下，主服务器上的事务处理不会停止。

- **最大性能** 这是默认模式；它以非同步方式将数据传输到备用重做日志文件。

除了设置数据保护模式外，测试和验证备用数据库的操作也是个好主意。
