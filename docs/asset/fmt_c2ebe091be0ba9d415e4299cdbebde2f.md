
### 12.7.3.2 InnoDB 存储引擎变量

前一部分讨论了如何配置 InnoDB 的表空间。InnoDB 还有自己的日志文件和内存缓冲区，以及几个其他配置参数。以下列表描述了一些常用于影响 InnoDB 存储引擎操作的参数。

- `innodb_buffer_pool_size`
  - 如果你有可用的内存，扩大 InnoDB 缓冲池可以减少访问表数据和索引时的磁盘使用量。

- `innodb_log_buffer_size`
  - InnoDB 试图在内存中缓冲有关每个事务的信息，并在事务结束时通过单次操作将其刷新到磁盘。如果事务较大且超过缓冲区大小，则需要在事务结束前多次刷新缓冲区，这需要更多的磁盘活动。增加缓冲区大小可以允许较大的事务在内存中缓冲而不会过早刷新。默认值为 1MB。最大有用值为 8MB。

- `innodb_log_group_home_dir`
  - InnoDB 有自己的日志文件，如果不存在，它会在服务器启动期间创建这些文件。默认情况下，这些日志创建在数据目录中，并且名称以 `ib_` 开头。`innodb_log_group_home_dir` 可用于设置 InnoDB 应写入其日志文件的目录的路径名。InnoDB 只创建文件，而不创建目录，因此请确保在启动服务器之前日志文件目录存在。

- `innodb_log_file_size`, `innodb_log_files_in_group`
  - 当日志填满时，InnoDB 通过将其刷新到磁盘来检查点缓冲池。使用更大的 InnoDB 日志文件可以减少日志填满的频率，从而减少此刷新发生的次数。（代价是，随着日志变大，崩溃后的恢复时间会增加。）你可以修改 `innodb_log_file_size` 来更改日志文件的大小，或修改 `innodb_log_files_in_group` 来更改文件数量。重要的特征是日志的总大小，即这两个值的乘积。日志的总大小不得超过 4GB。

### 12.7.4 配置 Falcon 存储引擎

Falcon 存储引擎的设计目标是自我调优且相对免维护，以简化管理。例如，Falcon 日志和表空间文件会根据需要自动增长，并在空间变得可用时回收可用空间。

以下列表描述了一些你在配置服务器时可能想要更改的 Falcon 参数：

- `falcon_page_size`
  - Falcon 使用固定的页大小（默认为 4KB）写入表空间。你可以将 `falcon_page_size` 赋值为字节数来选择页大小。允许的值是 1KB、2KB、4KB、8KB、16KB 或 32KB。你必须在 Falcon 创建任何表空间文件之前配置页大小。如果要更改页大小且 Falcon 已创建表空间，你必须备份并删除你的 Falcon 表，停止服务器并删除 Falcon 文件，然后使用新的页大小重新启动服务器并重新加载转储文件。

- `falcon_serial_log_dir`
  - Falcon 创建其日志文件的目录。默认位置是数据目录。

Falcon 允许你为表存储创建额外的表空间。你可能会这样做以将存储分布在多个物理设备上，以提高 I/O 效率，例如。要为 Falcon 表创建新的表空间，请使用 `CREATE TABLESPACE`：

```sql
CREATE TABLESPACE myts
ADD DATAFILE '/usr/local/mysql/data/falcon_myts.ftr'
ENGINE = FALCON;
```

默认情况下，Falcon 表在创建时被分配到默认表空间。要将表放入你的新表空间中，请在 `CREATE TABLE` 语句中使用 `TABLESPACE` 选项：

```sql
CREATE TABLE mytbl (i INT) ENGINE = Falcon TABLESPACE myts;
```

## 12.8 启用或禁用 LOAD DATA 的 LOCAL 功能

`LOAD DATA` 语句的 `LOCAL` 功能无需强制启用。它可以在构建时和运行时按以下方式控制：

- 在构建时，在运行 `configure` 时，可以通过使用 `--enable-local-infile` 或 `--disable-local-infile` 选项来默认启用或禁用客户端库的 `LOCAL` 功能。

- 在运行时，服务器可以通过 `--local-infile` 或 `--skip-local-infile` 选项启动，以启用或禁用服务器端的 `LOCAL` 功能。

如果在服务器端禁用了 `LOCAL`，客户端将完全无法使用此功能。如果在服务器端启用了 `LOCAL`，客户端库在客户端默认可能仍然禁用了 `LOCAL`，但某些程序允许根据需要启用它。例如，`mysql` 有一个 `--local-infile` 选项来启用 `LOCAL`，而 `mysqlimport` 有一个 `--local` 选项。

对于没有明确选项来启用或禁用 `LOCAL` 的程序，如果该程序隐式读取选项文件，你仍然可能控制此功能。这取决于该程序在连接服务器时是否使用 `mysql_options()` C API 函数，并带有 `MYSQL_READ_DEFAULT_FILE` 或 `MYSQL_READ_DEFAULT_GROUP` 选项，这些选项会导致读取选项文件。如果程序以这种方式使用 `mysql_options()`，你可以在适当的选项文件中列出 `local-infile` 或 `disable-local-infile` 选项来启用或禁用 `LOCAL`。`mysql_options()` 函数在附录 G “C API 参考”（在线）中有描述。

其他语言的 MySQL 编程接口也可能能够以这种方式控制 `LOCAL`，如果它们基于 C API 并调用 `mysql_options()`。例如，在 Perl DBI 脚本中，你可以使用数据源名称字符串中的 `mysql_read_default_file` 和 `mysql_read_default_group` 选项来控制脚本如何连接到 MySQL 服务器。

## 12.9 国际化和本地化问题

“国际化”是指软件能够根据任何特定位置的当地惯例进行使用的能力。“本地化”是指从受支持的一组当地惯例中选择一个特定的集合。MySQL 配置的以下方面与国际化和本地化有关：

- 服务器默认时区
- 用于显示诊断和错误消息的语言
- 可用的字符集和默认字符集

### 12.9.1 配置时区支持

在 MySQL 中，服务器通过检查其环境来设置默认时区。通常情况下，这将是服务器主机的本地时区，但你可以在服务器启动时明确指定时区。此外，服务器允许每个连接的客户端覆盖默认设置并设置自己的时区。这使得应用程序可以使用取决于客户端程序运行位置而不是服务器运行位置的时间设置。以下讨论描述了 MySQL 支持多个时区的能力。

两个系统变量保存时区信息：

- `system_time_zone` 表示服务器在启动时确定的服务器主机时区。此变量仅作为全局系统变量存在，并且不能在运行时重置。你可以通过在启动服务器之前将 `TZ` 环境变量设置为所需的时区来影响服务器在启动时如何设置 `system_time_zone`。然而，在某些上下文中（例如，当服务器在系统引导序列期间启动时），保证 `TZ` 被设置可能并不容易。在 Unix 上，通过为 `mysqld_safe` 启动脚本（而不是不理解该选项的 `mysqld`）指定 `--time-zone` 选项来设置时区的另一种方法。最好在选项文件的 `[mysqld_safe]` 组中列出此选项，特别是当你通过不支持命令行选项的 `mysqld_safe` 间接调用 `mysqld` 时。例如，要为 `mysqld_safe` 指定美国中部时区，请将以下内容添加到你的服务器选项文件中：

```
[mysqld_safe]
timezone=US/Central
```

该示例展示了一种广泛使用的语法（例如，它在 Solaris、Linux 和 Mac OS X 上有效）。另一种常见的语法如下：

```
[mysqld_safe]
timezone=CST6CDT
```

请使用系统文档中指示的语法。

- `time_zone` 表示 MySQL 服务器的默认时区。默认情况下，此变量设置为 `SYSTEM`，这意味着“使用 `system_time_zone` 设置”。你可以使用 `mysqld` 的 `--default-time-zone` 选项在启动时设置 `time_zone`。当服务器运行时，它使用 `time_zone` 的全局值来为每个连接的客户端设置会话 `time_zone` 值，该值成为客户端的默认时区。任何客户端都可以通过设置会话 `time_zone` 变量来重置其自身连接的时区。具有 `SUPER` 特权的管理客户端可以设置全局 `time_zone` 变量，以改变此后连接的客户端的默认值。

要确定全局和会话时区变量的当前值，请使用以下语句：

```sql
SELECT @@GLOBAL.time_zone, @@SESSION.time_zone;
```
