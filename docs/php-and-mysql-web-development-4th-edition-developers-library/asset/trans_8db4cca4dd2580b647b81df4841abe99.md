

减少客户端阻塞的发生量。（第 5.5 节“调度与锁问题”详细讨论了 `INSERT DELAYED`。）

- `max_allowed_packet` 是用于客户端通信的缓冲区允许增长到的最大尺寸。此变量可设置的最大值为 1GB。服务器的默认缓冲区大小为 1MB。某些客户端拥有自己的 `max_allowed_packet` 变量。如果您的客户端向服务器发送非常长的语句（例如，包含大型 `BLOB` 或 `TEXT` 值的语句），则可能需要增加服务器端和客户端端的该变量。例如，要以 64MB 数据包限制启动服务器，您可以向服务器选项文件中添加这些行：

```
[mysqld]
max_allowed_packet=64M
```

对于需要以 64MB 数据包限制调用 `mysql` 或 `mysqldump` 的情况，请像这样操作：

```
mysql --max_allowed_packet=64M ...其他选项...
mysqldump --max_allowed_packet=64M ...其他选项...
```

要始终使用这些设置，请将以下行添加到您的选项文件中：

```
[mysql]
max_allowed_packet=64M

[mysqldump]
max_allowed_packet=64M
```

- `max_connections` 是服务器允许的同时客户端连接数。如果服务器负载较重，您可能需要增加此值。例如，如果您的 MySQL 服务器被一个活跃的 Web 服务器用于处理由 DBI 或 PHP 脚本生成的许多语句，如果此变量设置得过低，访问您网站的访客可能会发现请求被拒绝。

- `table_cache`（自 MySQL 5.1.3 起为 `table_open_cache`）

表缓存的大小。增加此值可以通过减少必须执行的文件打开和关闭操作的数量，使 `mysqld` 能够同时保持打开更多的表。

如果您增加 `max_connections` 或 `table_cache` / `table_open_cache` 的值，服务器将需要更大数量的文件描述符。这可能会引起与操作系统中每进程文件描述符数量限制有关的问题，在这种情况下，您需要增加限制或绕过它。增加文件描述符数量限制的程序因系统而异。您可以尝试为 `mysqld` 设置 `open_files_limit` 变量。如果无法使用这些方法之一将打开文件限制设置得足够高，您可能需要配置系统以允许更多的文件描述符。某些系统只需编辑系统描述文件并重新启动即可配置。对于其他系统，您必须编辑内核描述文件并重新构建内核。请参阅您的系统文档以了解如何操作。

绕过每进程文件描述符限制的一种方法是将您的数据目录拆分为多个数据目录，并运行多个服务器。这实际上将可用的文件描述符数量乘以您运行的服务器数量。另一方面，这种策略可能会导致复杂性。例如，您无法从单个服务器访问不同数据目录中的数据库，并且需要为需要访问多个服务器的用户在多个服务器的授权表中设置权限。

减少文件描述符要求的另一种可能性是为主 MySQL 服务器设置到一个或多个从服务器的复制。所有更新都应指向主服务器，但仅执行检索请求的客户端请求可以分发到所有服务器。这减轻了主服务器的客户端负载，并减少了其文件描述符要求。

某些变量控制按客户端分配的资源。如果许多客户端同时连接到它，增加这些变量可能会极大地增加服务器的资源需求。您可能希望增加以改善性能的两个值是 `read_buffer_size` 和 `sort_buffer_size` 变量的值，它们决定了在读取和排序操作期间使用的缓冲区的大小。但是要小心：这些缓冲区是为每个连接分配的，因此如果您将相应变量的值设置得很大，由于系统资源消耗巨大，性能实际上可能会受到影响。

最好逐步更改每个连接的缓冲区大小，然后测试您的更改，而不是一次性大幅增加。这样做可以评估每次更改的影响，并降低严重性能下降的可能性。请务必使用现实的测试条件。这些缓冲区仅在需要时分配，而不是在客户端连接时立即分配。例如，除非客户端执行需要排序操作的查询，否则不会为客户端分配排序缓冲区。`join_buffer_size` 变量控制用于表之间无索引连接缓冲区的尺寸，但不执行连接的客户端不需要连接缓冲区。（相反，执行复杂的多表连接的客户端可能需要同时使用多个连接缓冲区。）您的测试条件应使用同时连接并执行复杂语句的客户端，以便您可以查看对服务器内存需求的实际影响。

### 12.6.3 检查状态变量值

服务器维护状态变量，使您能够监控其运行时操作。您可以使用 `SHOW STATUS` 语句显示这些变量：

```
mysql> SHOW STATUS;
```

| 变量名 | 值 |
|---|---|
| Aborted_clients | 0 |
| Aborted_connects | 1 |
| Binlog_cache_disk_use | 0 |
| Binlog_cache_use | 3 |
| Bytes_received | 125 |
| Bytes_sent | 151 |
| Com_admin_commands | 0 |
| ... | ... |

从 MySQL 5.0.2 开始，状态变量（与系统变量一样）具有全局和会话特定的值，因此该语句可以采用 `GLOBAL` 或 `SESSION` 修饰符：

```
SHOW GLOBAL STATUS;
SHOW SESSION STATUS;
```

`GLOBAL` 显示整个服务器的状态（所有连接在一起）。`SESSION` 显示当前连接的状态。默认值为 `SESSION`。`LOCAL` 是 `SESSION` 的同义词。

要编写使用修饰符但可移植到早于 5.0.2 的 MySQL 版本的 `SHOW STATUS` 语句，请将修饰符放在版本特定的注释中。例如：

```
SHOW /*50002 GLOBAL */ STATUS;
```

如果某个变量仅具有全局值，则 `GLOBAL` 和 `SESSION` 的值相同。附录 ID 指示每个状态变量具有哪些值。

类似于 `SHOW VARIABLES`，`LIKE` 子句将输出限制为名称与给定 SQL 模式匹配的变量。例如，要检查 MyISAM 键缓存变量的值，请使用此语句：

```
mysql> SHOW GLOBAL STATUS LIKE 'Key%';
*************************** 1. 行 ***************************
Variable_name            Value
Key_blocks_not_flushed   0
Key_blocks_unused        7247
Key_blocks_used          13
Key_read_requests        41
Key_reads                14
Key_write_requests       40
Key_written              2
***************************
```

从 MySQL 5.0.2 开始，可以使用 `WHERE` 子句来指定选择行的通用条件。

从 MySQL 5.1.12 开始，您还可以查询名为 `GLOBAL_STATUS` 和 `SESSION_STATUS` 的 `INFORMATION_SCHEMA` 表以获取状态变量信息。例如：

```
SELECT * FROM INFORMATION_SCHEMA.GLOBAL_STATUS
WHERE VARIABLE_NAME LIKE 'Qcache%' OR VARIABLE_NAME LIKE 'Key%';
```

状态变量仅由服务器设置，因此对于用户而言是只读的，不能像系统变量那样使用 `SET` 进行修改。

MySQL 服务器支持多种存储引擎，并且就使哪些引擎可用而言高度可配置。通用存储引擎特性在第 2 章“使用 SQL 管理数据”中讨论。以下讨论描述了如何配置服务器使用的引擎。它还提供了 MyISAM、InnoDB 和 Falcon 存储引擎的具体配置信息。

### 12.7.1 选择服务器支持的存储引擎

MySQL 服务器提供了对哪些存储引擎可用的灵活控制：

- 如果您从源代码构建 MySQL，您可以确定要构建哪些可选存储引擎。
- 对于任何服务器，无论您是否自行编译，您都可以在启动时有选择地启用或禁用一些已构建的可选存储引擎。您可以禁用不需要的引擎，以减少服务器内存需求。（请记住，如果您禁用某个引擎，则无法访问该引擎可能已经创建的任何表。）
- 您可以运行时查明哪些引擎可用，以及哪个是默认引擎。

表 12.7 显示了在从源代码构建 MySQL 时使用 *configure* 包含或排除每个引擎的选项。某些引擎，如果已构建，如果您不想使用它们，可以在 *mysqld* 启动时使用选项禁用。Falcon 需要 MySQL 6.0 或更高版本。*--skip-archive* 选项需要 MySQL 5.1 或更高版本。

| 引擎 | 配置选项 | 运行时选项 |
|---|---|---|
| ARCHIVE | --with-archive-storage-engine, --without-archive-storage-engine | --skip-archive |
| BLACKHOLE | --with-blackhole-storage-engine, --without-blackhole-storage-engine | |
| CSV | --with-csv-storage-engine, --without-csv-storage-engine | |
| EXAMPLE | --with-example-storage-engine, --without-example-storage-engine | |
| Falcon | --with-falcon-storage-engine, --without-falcon-storage-engine | --skip-falcon |
| FEDERATED | --with-federated-storage-engine, --without-federated-storage-engine | |
| InnoDB | --with-innodb, | --skip-innodb |

