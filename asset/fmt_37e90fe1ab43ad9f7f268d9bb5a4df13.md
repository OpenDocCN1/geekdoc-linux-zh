
- 0 - 不捕获任何管理通知消息。（不建议此设置）。
- 1 - 仅限严重错误。仅记录致命和不可恢复的错误。为了从这些某些情况中恢复，你可能需要 DB2 服务的协助。
- 2 - 所有错误。记录需要系统管理员或数据库管理员立即关注的情况。如果情况未解决，可能会导致致命错误。非常重大的非错误活动（例如恢复）的通知也在此级别上被记录。
- 3 - 捕获健康监控器（Health Monitor）警报。记录不具威胁且不需要立即采取行动但可能表明系统未优化的状况。此级别将捕获健康监控器警报、健康监控器警告和健康监控注意。这是默认值。
- 4 - 所有错误、警告和信息消息。

默认的 `DIAGLEVEL` 通常适用于 DB2 运行。然而，在 DB2 初始化或发生错误时，可以将 `DIAGLEVEL` 更新为 4，以便收集尽可能的信息：注意，你必须将 `notifylevel` 设置为 2 或更高，以便健康监控器向定义的联系人发送通知。

```
UPDATE DBM CFG USING DIAGLEVEL 4
```

## DB2 通用数据库中的跟踪

有时问题发生在 DB2 或使用 DB2 的应用程序中，且 FFDC 信息不足以确定问题源。此时，DB2 客户服务可能会要求 DBA 对应用程序、CLI/ODBC/JDBC 驱动或数据库本身运行跟踪。

以下是 `db2trc` 命令的语法：

## 诊断与问题确定 747

![](img/ca7cfad01341360e684d5dd2379b19e9_770_0.png)

跟踪或调试 DB2 应用程序主要是创建该程序的开发人员的任务。DB2 嵌入 SQL 程序使用 SQLCA 提供报告功能。这允许应用程序开发人员监控在 DB2 上执行的代码。

跟踪 DB2 本身与 CLI/ODBC/JDBC 跟踪有些相似。你指定跟踪输出的去向以及何时开启。跟踪对 DB2 的性能有显著影响。然而，在 DB2 内部进行跟踪时你具有一定的灵活性。你可以过滤你想监控的内容。你可以指定内存缓冲区的大小以及跟踪保留多少条错误。针对 DB2 的跟踪可以使用 `db2trc` 命令启动。你可以指定某些选项来收集跟踪信息。获取 DB2 跟踪分为四个步骤：

- 开启跟踪（`db2trc ON`）。
- 转储跟踪输出（`db2trc DMP`）。
- 关闭跟踪（`db2trc OFF`）。
- 格式化跟踪输出（`db2trc FLW` 或 `db2trc FMT`）。

## 第 12 章 监控与调

- `-m` 掩码您想要跟踪的特定记录类型。
- `-e` 指定跟踪程序保留的 DB2 错误数量限制。
- `-r` 指定跟踪记录的大小限制。
- `-s` 或 `-f` 指定跟踪输出应保留在共享内存中还是直接写入文件。
- `-l` 或 `-i` 指定存储跟踪信息的内存缓冲区的大小。`-l` 选项将保留跟踪的最后记录。`-i` 选项将保留初始记录。

在您使用 DB2 DMP 命令和 DB2TRC OFF 命令后，可以对跟踪输出进行格式化。执行 DB2TRC FMT 命令，例如：

```c
C:\SQLIB\BIN> db2trc fmt mytrace.dmp mytrace
Trace wrapped :YES
Size of trace :3996054 bytes
Records in trace :39450
Records formatted :39450
```

**图 12-43** DB2TRC 命令

由 DB2TRC FMT 命令生成的跟踪信息可能类似于图 12-44 所示的片段。

| ID | 详情 |
| :--- | :--- |
| 14719 | DB2 fnc_retcode Sw-query graph sqlnq_ftb::new (1.33.60.55)<br>pid 138; tid 117; cid 139; time 7951153; trace_point 254<br>return_code = 000000 = 0 |
| 14720 | DB2 fnc_entry Sw-query graph sqlnq_ftb::sqlnq_ftb (1.30.60.56)<br>pid 138; tid 117; cid 139; time 7951153; trace_point 0<br>called_from_008F618 |
| 14721 | DB2 cei_entry oper_system_services sqlgmbk (1.20.15.82)<br>pid 138; tid 117; cid 139; time 7951153; trace_point 0<br>called_from_10047AE3 |
| 14722 | DB2 cei_data oper_system_services sqlgmbk (1.25.15.82)<br>pid 138; tid 117; cid 139; time 7951153; trace_point 1<br>4c05 9601 8c00 0000 0000<br>....................<br>L................ |

**图 12-44** DB2 跟踪记录示例

有关 DB2 数据库中跟踪的更多信息，请参阅 DB2 信息中心。

## 诊断与问题确定

### CLI/ODBC/JDBC 跟踪设施

DB2 CLI 和 DB2 JDBC 跟踪文件分析可以从多个方面使应用程序受益。首先，细微的程序逻辑和参数初始化错误通常在跟踪中显而可见。其次，DB2 CLI 和 DB2 JDBC 可能为更好地调优应用程序及其访问的数据库提供建议。例如，如果 DB2 跟踪显示某个表在特定属性集上被多次查询，则可以在表上创建对应属性的索引以提高应用程序性能。最后，DB2 CLI 和 DB2 JDBC 跟踪文件可以帮助应用程序开发者理解第三方应用程序或接口的行为。

DB2 CLI 和 DB2 JDBC 驱动程序提供了全面的跟踪设施。默认情况下，这些跟踪是禁用的，不消耗额外的计算资源。启用后，每当应用程序访问相应的驱动程序（DB2 CLI 或 DB2 JDBC）时，跟踪设施会生成一个或多个日志文件。这些日志提供了详细信息：

- 应用程序调用 CLI 或 JDBC 函数的顺序
- 传递给或从 CLI 或 JDBC 函数接收的输入输出参数
- CLI 或 JDBC 函数生成的返回码以及任何错误或警告消息

## DB2 CLI 和 DB2 JDBC 跟踪配置

DB2 CLI 和 DB2 JDBC 跟踪设施的配置参数均从 DB2 CLI 配置文件 `db2cli.ini` 读取。默认情况下，该文件位于 Windows 平台上的 `\sqlib` 路径，以及 Linux 或 Unix 平台上的 `/cfg` 路径。您可以通过设置 `DB2CLIINIPATH` 环境变量来覆盖默认路径。在 Windows 平台上，如果存在使用 ODBC 驱动程序的用户定义数据源，则可以在用户的配置（或主）目录中找到额外的 `db2cli.ini` 文件。此 `db2cli.ini` 文件将覆盖默认文件。

从命令行处理器查看当前的 `db2cli.ini` 跟踪配置参数，请执行以下命令：

```cli
CLI CFG FOR SECTION COMMON
```

例如，从命令行处理器执行以下命令可更新 `db2cli.ini` 文件并启用 JDBC 跟踪设施：

```sql
UPDATE CLI CFG FOR SECTION COMMON USING jdbtrace 1
```

**注意：** 跟踪 CLI/JDBC 应用程序会显著降低应用程序的性能。此外，大量数据写入输出跟踪文件可能会占用大量的磁盘空间。

## DB2 CLI 跟踪选项与 db2cli.ini 文件

当使用 DB2 CLI 驱动程序的应用程序开始执行时，驱动程序会检查 `db2cli.ini` 文件 `[COMMON]` 部分的跟踪设施选项。这些跟踪选项是在 `db2cli.ini` `[COMMON]` 部分中设置为特定值的特定跟踪关键字。

可以定义的 DB2 CLI 跟踪关键字（详细信息请参阅 *DB2 V8 信息中心*）：

- `TRACE=0|1` - 启用或禁用跟踪
- `TRACEFILENAME=0|<任何正整数>` - 指定跟踪信息写入 DB2 CLI 跟踪日志文件的频率
- `TRACEPATH=<完全限定的跟踪路径>` - 指定所有 DB2 CLI 跟踪信息的写入位置。没有默认的日志文件路径，指定的路径必须在应用程序执行时存在（DB2 CLI 驱动程序不会创建路径）。
- `TRACEFLUSH=0 | <任何正整数>` - 指定跟踪信息写入 DB2 CLI 日志文件的频率
- `TRACEREFRESHINTERVAL=0 |任何正整数>` - 任何大于0 的值都会使 DB2 CLI 跟踪设施按照指定的间隔（每隔 n 秒）从 `db2cli.ini` 文件重新读取 `TRACE` 和 `TRACELIST` 关键字。

选项，DB2 跟踪选项以关键字/值对的形式指定，位于 db2cli.ini 文件的 [COMMON] 节部分下。

可以定义的 DB2 JDBC 跟踪关键字有：

- `JDBCTRACE=0|1` - 启用或禁用跟踪
