
This appendix discusses some commonly used DB2 commands in a multiple partition environment (MPE). These commands are very useful when you need to collect information from multiple database partitions or machines, or make specified commands running against multiple partitions or machines. The commands that are discussed in this appendix include `db2_ps`, `db2_all`, `rah`, `db2_call_stack`, and so on.

# `db2_all` 和 `rah`

在多分区环境中，您可能希望在实例中的多个机器或分区上运行命令，而不想在每个相关机器或分区上重复相同的命令——为此，您可以使用 `rah` 命令或 `db2_all` 命令。

`rah` 命令允许您在实例分布的所有机器上发出要运行的命令。如果您希望命令在实例的数据库分区级别运行，则运行 `db2_all` 命令。

要使用 `rah` 在所有机器上运行命令，一般的命令语法为：

```
rah [ commands ]
```

要将命令在您指定的所有数据库分区上运行，请使用 `db2_all` 命令。一般的命令语法为：

```
db2_all [ commands ]
```

如果要运行的命令未跟随 `rah` 或 `db2_all`，您将被 `rah` 和 `db2_all` 提示输入命令。一般来说，如果您将命令作为命令行参数指定，当它包含以下特殊字符中的任何一个时，必须用双引号将其括起来：

| & ; < > ( ) { } [ ] 未替换的 $

要获取有关 `db2_all` 或 `rah` 语法的帮助信息，请输入：

```
db2_all "?"
```

或，

```
rah "?"
```

对于 `db2_all` 和 `rah` 存在一些命令前缀序列（此处前缀序列为一个或多个特殊字符），可用于控制命令运行模式，例如，在所有相关机器或分区上按顺序或并行运行命令，在前台或后台运行，是否在执行指定命令前执行环境设置脚本等等。表 A-1 显示了一些常用的命令前缀序列。有关这些前缀序列的详细说明或其他可用的前缀序列，请参阅“Administration”指南（在第 303 页的“Other publications”中列出）。

## 表 A-1 `db2_all` 和 `rah` 常用命令前缀序列

| Sequence | Description |
|---|---|
| `l` | Runs the commands in sequence in the background. |
| `l&` | Runs the commands in sequence in the background and terminates the command after all remote commands have completed. |
| `ll` | Runs the commands in parallel in the background. |
| `ll&` or `;` | Runs the commands in parallel in the background and terminates the command after all remote commands have completed. |
| `<` | Commands sent to all the machines for running except this one. |
| `<<-nnn<` | Commands sent to all other database partitions but not the database partition `nnn` for running. |
| `<<+nnn<` | Commands sent to only database partition `nnn` for running |
| `>` | Substitutes occurrences of `<>` with the machine name. |
| `"` | Substitutes occurrences of `()` by the machine index, and substitutes occurrences of `##` by the node number. |

以下示例中的第一个命令显示了如何为实例中的所有数据库分区更新数据库配置参数；第二个命令显示了如何为替换目的使用前缀序列，以及使用前缀序列 `'`（单引号）回显将要执行的命令。

### 示例：A-1 在多分区环境中使用 `db2_all`

```
$ db2_all "db2 update db cfg for sample using logprimary 10 logsecond 15"

DB20001I The UPDATE DATABASE CONFIGURATION command completed successfully.
UDBLNX06: db2 update db cfg for sample using logprimary 10 logsecond 15 completed ok

DB20001I The UPDATE DATABASE CONFIGURATION command completed successfully.
UDBLNX07: db2 update db cfg for sample using logprimary 10 logsecond 15 completed ok

$ db2_all "'">echo Machine Name: <> Partition Number: ##"
echo Machine Name: <> Partition Number: ##

Machine Name: UDBLNX06 Partition Number: 0
UDBLNX06: echo Machine Name: <> Partition Number: ## completed ok

Machine Name: UDBLNX07 Partition Number: 1
UDBLNX07: echo Machine Name: <> Partition Number: ## completed ok
```

请注意，在我们的示例中，前缀序列 `"`（双引号）前面有一个反斜杠 `\`。这里反斜杠用作转义字符。此外，示例中 DB2 实例所有者的登录 shell 是 `bash`，而不是 DB2 原本支持的 `ksh`。

## `db2_ps`

您可以使用 `db2_ps` 命令列出所有逻辑分区上的所有 db2 引擎进程。

## `db2_call_stack`

此命令在基于 UNIX 的平台上，会导致所有数据库分区服务器上运行的所有进程将调用跟踪写回 `syslog`。一般来说，除非 DB2 支持人员要求，否则您无需运行此命令。

有关此处提及的命令的更多信息，请参阅“Administration”指南（在第 303 页的“Other publications”中列出），或参阅 `db2_all` 或 `rah` 提供的在线帮助。

# DB2 Tools Catalog 创建

本附录提供了手动创建 DB2 Tools Catalog 的示例以及与 Tool Catalog 创建相关的信息。此外，此处还简要介绍了通知设置。

如果您在安装 DB2 时未创建工具目录，可以使用 DB2 Control Center 或命令行处理器创建。如果使用 DB2 Control Center，则在调用 DB2 Control Center 后，可以选择 Tools --> Tools Settings --> Scheduler Settings，并创建一个新的 Tools Catalog。

这里我们提供了使用 DB2 CLP 手动创建 Tools Catalog 的示例，同时还包括在创建 Tools Catalog 之前和之后检查 DAS 配置变化的步骤，以及 `CREATE TOOLS CATALOG` 命令自动创建的新表空间和缓冲池。

在创建 Tools Catalog 之前，我们使用 `GET ADMIN CFG` 获取 DAS 的当前配置，如示例 B-1 所示。您可以看到，与 Tools Catalog 相关的一些参数目前为空，包括 `TOOLSCAT_DB`、`TOOLSCAT_INST` `TOOLSCAT_SCHEMA`。我们将使用此信息在稍后比较 `CREATE TOOLS CATALOG` 命令所做的 DAS 配置更改。

## 示例：B-1 检查当前 DAS 配置
