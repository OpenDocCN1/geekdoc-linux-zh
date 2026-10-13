
对于所有这些 MySQL 命令行操作，有很多选项可用。这些选项也可以在 `my.cnf` 文件的 `[client]` 分组中指定，并通过使用 `--help` 标志进行查找。

在成功登录客户端后，可以使用多种 MySQL 客户端特定的命令。以下是你使用帮助命令时应该收输出：

MySQL commands:

- `?` (`h`): `help` 的同义词。
- `clear` (`c`): 清空命令。
- `connect` (`r`): 重新连接服务器。
- `dimiter` (`d`): 设置查询分隔符。
- `edit` (`e`): 使用 `$EDITOR` 编辑命令。
- `ego` (`G`): 将命令发送到 MySQL 服务器，垂直显示结果。
- `exit` (`q`): 退出 mysql。等同于 `quit`。
- `go` (`g`): 将命令发送到 MySQL 服务器。
- `help` (`h`): 显示此帮助。
- `opager` (`n`): 禁用分页器，打印到标准输出。
- `notee` (`t`): 不写入输出文件。

# 执行 MySQL 管理

- `pager` (`\P`) 设置 `PAGER` [`to_pager`]。
- `print` (`\p`) 通过 `PAGER` 查询结果。
- `prompt` (`\R`) 更改你的 mysql 提示符。
- `quit` (`\q`) 退出 mysql。
- `rehash` (`\#`) 重建补全哈希表。
- `source` (`\.`) 执行一个 SQL 脚本文件。以文件名作为参数。
- `status` (`\s`) 从服务器获取状态信息。
- `system` (`\!`) 执行系统 shell 命令。
- `tee` (`\T`) 设置输出文件 [`to_outfile`]。将所有内容追加到指定的输出文件中。
- `use` (`\u`) 使用另一个数据库。以数据库名作为参数。

如需更详细的描述，请参考 MySQL 文档。目前，你应该了解这些选项以及如何使用 `quit` 命令从 SQL shell 退出。`MySQLadmin` 会对你说“bye”，然后你将返回到你的 Linux shell。

## mysqladmin

在本章的早些部分，我们涵盖了 `mysqladmin` 命令的众多用法之一，向你展示了如何更改用户密码。在本节中，我们汇总了一份你可以通过 `mysqladmin` 指定的命令列表，这将让你能够对服务器执行管理任务并检查当前状态。该命令的正确用法如下：

```
mysqladmin [options] [command-option] command ...
```

你可以像往常一样使用 `--help` 标志来查找完整的选项列表。现在，请熟悉此命令行程序的功能，以便在你需要管理服务器时可以回来使用此命令作为参考。使用这些命令可能比登录客户端并执行许多复杂的命令来实现相同的结果要简单得多：

- `create databasename` 创建新数据库。
- `drop databasename` 删除数据库及其所有数据表。
- `extended-status` 显示服务器变量及其值。
- `flush-logs` 刷新所有日志。
- `flush-privileges` 重新加载权限表（等同于 `reload`）。
- `flush-status` 清空状态变量。
- `flush-tables` 刷新所有表。
- `flush-threads` 刷新线程缓存。（在 MySQL 3.23.16 中添加。）
- `kill id,id,...` 杀死服务器线程。
- `password new-password` 设置新密码。这将为你用于 `mysqladmin` 连接服务器的账户密码更改为 `new-password`。
- `ping` 检查服务器是否存活。
- `processlist` 显示活动服务器线程列表。这类似于 `SHOW PROCESSLIST` 语句的输出。如果给出 `--verbose` 选项，输出将类似于 `FULL PROCESSLIST`。
- `reload` 重新加载权限表。
- `refresh` 刷新所有表，关闭并打开日志文件。
- `shutdown` 停止服务器。
- `start-slave` 在从服务器上启动复制。（在 MySQL 3.23.16 中添加。）
- `status` 显示简短的状态消息。
- `stop-slave` 停止从库服务器上的复制。（在 MySQL 3.23.16 中添加。）
- `variables` 显示服务器系统变量及其值。
- `version` 显示服务器的版本信息。

## mysqlbinlog

此命令允许你检查二进制日志文件的内容。*二进制日志文件* `binary log file` 存储了修改过任何数据的命令历史。因此，如果执行了更新命令但没有匹配到并更新任何行，则它不会出现在日志文件中。这些发生的情况会与各种其他信息（如时间戳、发布线程、语句文本等）一起存储。

`mysqlbinlog` 使用的正确语法如下：

```
mysqlbinlog [options] log_file ...
```

还可以将这些结果管道到 MySQL 客户端进行执行。这将允许对数据库应用自某个时间（自上次备份以来）之后的所有更改。这是一个极好的工具，我们将在“备份和恢复数据库”部分进行更深入的介绍。

## mysqlcheck 命令

`mysqlcheck` 命令用于分析、优化和修复 MyISAM 表。该命令必须在数据库服务器运行时使用。在生产环境中，这具有巨大的优势，因为你无法为了检查或修复单个数据库而关闭整个服务器。你可以指定单个数据库、多个数据库或所有数据库进行检查或修复。以下是三种方法：

```
mysqlcheck [options] db_name [tables]
```

```
mysqlcheck [options] --databases DB1 [DB2 DB3 ...]
```

```
mysqlcheck [options] --all-databases
```

`mysqlcheck` 命令的独特之处在于，你可以重命名文件或在不同名称下创建符号链接以指定不同的默认选项。例如，如果你将 `mysqlcheck` 重命名为 `mysqlrepair`，那么该命令将执行 `-r` 操作。你也可以使用 `mysqlanalyze` 执行 `-a`，使用 `mysqloptimize` 执行 `-o`。

## mysqldump

`mysqldump` 命令是一个重要的命令，在你与 MySQL 打交期间可能会频繁使用。你可以通过如下 `mysqldump` 语法指定一个或多个数据库：

```
mysqldump [options] db_name [tables]
```

```
mysqldump [options] --databases DB1 [DB2 DB3 ...]
```

```
mysqldump [options] --all-databases
```

如果你准备转储一个巨大的数据库，应该确保指定 `--quick` 标志。这将导致 MySQL 在转储结果之前不将整个结果加载到内存中。除了 `quick` 选项外，该命令还有许多可用选项。其中许多选项将允许你将数据转储为几乎任何格式。

## mysqlhotcopy

此命令是备份最快的方法。其正确用法如下：

```
mysqlhotcopy [options] database_name
```

有关此命令选项的更多信息，请参考手册。

注意：此程序可能需要安装 DBI（数据库接口）。

## mysqlimport

此命令提供了与 `LOAD DATA INFILE` 语句相同的功能。从命令行你可以告诉 MySQL 加载存储在文件中的数据。为此，你使用以下语法：

```
mysqlimport [options] database textfile ...
```

与 `mysqldump` 一样，你可以指定任何选项来告诉 MySQL 数据格式。建议在覆盖你的实际数据之前，在新表或数据库上尝试此命令并检查结果。

## mysqlshow

此命令可快速检查数据库、表、列和/或表索引的内容。此命令提供了与 `SHOW` SQL 命令相同的功能。使用命令时，应遵循以下语法：

```
mysqlshow [options] [database [table [column]]]
```

在使用此命令时漏掉了任何参数，则假设你使用了通配符。例如，如果漏掉了表名，将显示所有表。此命令也支持对参数使用通配符。

# 执行 MySQL 管理

## replace 工具

`replace` 工具允许你在文件或标准输入中直接更改字符串。例如，以下语句会将 `mine` 和 `yours` 文件中的 `foo` 替换为 `bar`，并将 `bar` 替换为 `foo`。

```
replace 'foo' 'bar' 'bar' 'foo' -- mine yours
```
