
可用于确保您已从服务器获取了所有二进制日志信息。（但是，如果您将事件发送到同一服务器进行处理，这可能会导致无限循环。）

### F.10.3 mysqldbinlog 变量

以下 `mysqldbinlog` 变量可以按照第 F.2.1.2 节“设置程序变量”中给出的说明进行设置。

- `open_files_limit`：要预留的文件描述符数量。默认值为 64。

## F.11 mysqlcheck

`mysqlcheck` 是一个用于检查和修复表的客户端程序。它提供了 `CHECK TABLE`、`ANALYZE TABLE`、`OPTIMIZE TABLE` 和 `REPAIR TABLE` 语句的命令行界面。它与 `myisamchk` 有些相似，但它是在服务器运行时使用的，并且对非 MyISAM 表提供一定程度的支持。`mysqlcheck` 通过向服务器发送管理 SQL 语句以供执行来工作。这与直接操作表文件的 `myisamchk` 形成对比，后者要求您协调服务器对表的访问或者停止服务器。

所有 `mysqlcheck` 选项都支持 MyISAM 表。`mysqlcheck` 还可以检查和分析 InnoDB 表。

`mysqlcheck` 可以在三种模式中的任何一种下运行：

```bash
mysqlcheck [options] db_name [tbl_name] ...
mysqlcheck [options] --databases db_name ...
mysqlcheck [options] --all-databases
```

在第一种情况下，`mysqlcheck` 检查给定数据库中指定的表。如果没有指定表名，`mysqlcheck` 将检查该数据库中的所有表。在第二种情况下，所有参数都被视为数据库名称，`mysqlcheck` 将检查每个数据库中的所有表。在第三种情况下，`mysqlcheck` 将检查所有数据库中的所有表。

### F.11.1 mysqlcheck 支持的标准选项

- `--character-sets-dir`
- `--help`
- `--shared-memory-base-name`
- `--compress`
- `--host`
- `--silent`
- `--debug`
- `--password`
- `--socket`
- `--debug-check`
- `--pipe`
- `--user`
- `--debug-info`
- `--port`
- `--verbose`
- `--default-character-set`
- `--protocol`
- `--version`

`--debug-check` 和 `--debug-info` 在 MySQL 5.1.21 中可用。`mysqlcheck` 还支持标准的 SSL 选项。

### F.11.2 mysqlcheck 特有的选项

`mysqlcheck` 支持以下选项来控制其处理表的方式。在此列表之后，对这些选项及其对应的 SQL 语句的等价关系进行了说明。

- `--all-databases`, `-A` *(布尔值)*
  处理所有数据库中的所有表。

- `--analyze`, `-a`
  通过发出 `ANALYZE TABLE` 语句执行表分析。（例如，这将分析键值的分布。）分析结果可以帮助查询优化器更快地执行基于索引的查找和连接。

- `--all-in-1`, `-1` *(布尔值)*
  如果没有此选项，`mysqlcheck` 会为每个表发出单独的语句。此选项使 `mysqlcheck` 按数据库对表进行分组，并在每个数据库中的单条语句中列出所有表。

- `--auto-repair` *(布尔值)*
  如果发现要检查的表存在问题，在检查阶段完成后运行第二阶段以修复它们。

- `--check`, `-C`
  发出 `CHECK TABLE` 语句以检查错误。如果未明确指定操作，这是默认操作。

- `--check-only-changed`, `-c`
  仅检查自上次检查以来已更改或未被正确关闭的表。

- `--check-upgrade`, `-u`
  检查表是否与当前版本的 MySQL 兼容，在升级后很有用。如果使用 `--auto-repair`，当发现不兼容时，会尝试自动修复表。此选项是在 MySQL 5.0.19/5.1.7 中引入的。

- `--databases`, `-B` *(布尔值)*
  将所有参数解释为数据库名称，并检查每个数据库中的所有表。

- `--extended`, `-E` *(布尔值)*
  执行扩展表检查。如果与 `--repair` 一起使用，则使用比单独使用 `--repair` 时更广泛但更慢的修复方法。

- `--fast`, `-F` *(布尔值)*
  仅检查未被正确关闭的表。

- `--fix-db-names` *(布尔值)*
  检查数据库名称，并将其转换为 MySQL 5.0 和 5.1 之间所做的名称编码更改。此选项是在 MySQL 5.1.7 中引入的。

- `--fix-table-names` *(布尔值)*
  检查表名称，并将其转换为 MySQL 5.0 和 5.1 之间所做的名称编码更改。此选项是在 MySQL 5.1.7 中引入的。

- `--force`, `-f` *(布尔值)*
  即使发生错误也继续执行。

- `--medium-check`, `-m`
  使用一种比 `--extended` 更快但稍欠彻底的方法来执行表检查。对于大多数情况，此检查模式应该足够了。

- `--optimize`, `-o`
  通过发出 `OPTIMIZE TABLE` 语句执行表优化。

- `--quick`, `-q` *(布尔值)*
  对于表检查，此选项跳过检查数据行中的链接。与 `--repair` 一起使用时，此选项仅修复索引文件，而不触及数据文件。与此选项指定两次不同的行为相反，`mysql` 在该选项指定两次时行为会有所不同。

- `--repair`, `-r`
  通过发出 `REPAIR TABLE` 语句执行表修复。此修复模式应能纠正大多数问题，除了本应仅包含唯一值的索引中出现重复值的情况。

- `--tables`
  覆盖 `--databases`，使得随后的参数被解释为表名。

- `--use-frm` *(布尔值)*
  与 `--repair` 一起使用时，执行使用表的 `.frm` 文件来重新初始化索引文件并确定如何解释数据文件内容的表修复操作，以便重建索引。如果索引已丢失或不可恢复地损坏，这可能很有用。然而，它应被视为最后的手段，并且仅当您当前的 MySQL 版本与创建该表时使用的版本相同时才应使用。

- `--write-binlog` *(布尔值)*
  将 `ANALYZE TABLE`、`OPTIMIZE TABLE` 和 `REPAIR TABLE` 语句写入二进制日志（这意味着它们将被发送到复制从库）。此选项默认启用；使用 `--skip-write-binlog` 可以禁用它。此选项是在 MySQL 5.1.18 中引入的。

下表显示了 `mysqlcheck` 选项与其发出的 SQL 语句之间的关系。

表检查选项（仅适用于 MyISAM 和 InnoDB 表）：

| **选项** | **对应语句** |
| :--- | :--- |
| `--check` | `CHECK TABLE tbl_list` |
| `--check-only-changed` | `CHECK TABLE tbl_list CHANGED` |
| `--extended` | `CHECK TABLE tbl_list EXTENDED` |
| `--fast` | `CHECK TABLE tbl_list FAST` |
| `--medium-check` | `CHECK TABLE tbl_list MEDIUM` |
| `--quick` | `CHECK TABLE tbl_list QUICK` |

对于 InnoDB 表，前表中所有选项都视为 `--check`；InnoDB 不支持不同类型的检查。

表分析选项（仅适用于 MyISAM 和 InnoDB 表）：

| **选项** | **对应语句** |
| :--- | :--- |
| `--analyze` | `ANALYZE TABLE tbl_list` |

表修复选项（仅适用于 MyISAM 表）：

| **选项** | **对应语句** |
| :--- | :--- |
| `--repair` | `REPAIR TABLE tbl_list` |
| `--repair --quick` | `REPAIR TABLE tbl_list QUICK` |
| `--repair --extended` | `REPAIR TABLE tbl_list EXTENDED` |
| `--repair --use-frm` | `REPAIR TABLE tbl_list USE_FRM` |

表优化选项（仅适用于 MyISAM 表）：

| **选项** | **对应语句** |
| :--- | :--- |
| `--optimize` | `OPTIMIZE TABLE tbl_list` |

## F.12 mysqld

`mysqld` 是 MySQL 服务器。它为客户机程序提供数据库访问权限，因此它必须处于运行状态，否则客户机无法使用由服务器管理的数据库。当 `mysqld` 启动时，它会打开用于监听的网络接口，然后等待客户机连接。

`mysqld` 是多线程的，并使用单独的线程处理每个客户机连接，以提供客户机之间的并发性。写入数据库的语句是原子性地执行的；当服务器开始执行此类语句时，直到当前语句完成之前，它将不会执行涉及该数据的任何其他语句。例如，不能有两个客户机同时修改表中的同一行。

通常的调用序列很简单，只需服务器名称后跟任何所需的选项：

```bash
mysqld [options]
```

在 Windows 上，可以将服务器安装为服务运行。例如，可以安装服务器使其在系统启动时自动运行，或者按以下方式将其作为服务移除：

```bash
C:\> C:\mysql\bin\mysqld --install
C:\> mysqld --remove
```

安装命令使用服务器的完整路径名。如果服务器安装在不同位置，请相应修改路径名。默认的服务名称为 MYSQL。您可以提供选项后的服务名称：

```bash
C:\> C:\mysql\bin\mysqld --install service_name
C:\> mysqld --remove service_name
```

这允许在不同的服务名称下运行多个服务器。如果没有 `service_name` 参数或服务名称为 MySQL，服务器将使用 MYSQL 作为服务名称，并从标准选项文件中读取 `[mysqld]` 组。如果 `service_name` 参数不同于 MySQL，服务器将使用该名作为服务名称，并从标准选项文件中读取 `[mysqld]` 和 `[service_name]` 组。

您还可以在提供 `--defaults-file` 选项来指定服务器在启动时要读取的附加选项文件：

```bash
C:\> C:\mysql\bin\mysqld --install service_name --defaults-file=file_name
```

在这种情况下，`service_name` 参数不是可选的。

前面关于 `--install` 的说明也适用于 `--install-manual`。

### F.12.1 mysqld 支持的标准选项

- `--character-sets-dir`
- `--debug`
- `--help`
- `--port`
- `--shared-memory-base-name`
- `--socket`
- `--user`
- `--verbose`

