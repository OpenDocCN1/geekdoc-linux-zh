

# 表 24-2：（续）

| 程序 | 描述 |
|---|---|
| mysqltest_embedded | 在嵌入式 MySQL 服务器上运行罐装测试并将结果与预期结果文件进行比较 |
| mysqltestmanager | 一个可以在后台管理多个 MySQL 服务器安装的程序 |
| mysqltestmanagerc | 用于与 mysqltestmanager 程序交互的命令行客户端 |
| mysqltestmanager-pwgen | 生成用于 mysqltest 程序的密码文件 |
| mysql_tzinfo_to_sql | 将系统时区表加载到 MySQL 中 |
| mysql_upgrade | 检查所有表是否与当前版本的 MySQL 不兼容 |
| mysql_upgrade_shell | 在非 UNIX 系统上运行 mysql_upgrade 程序的实用工具 |
| mysql_waitpid | 向具有指定 pid 的进程发送 KILL 信号并等待其退出 |
| mysql_zap | 向匹配指定模式的任何进程发送 KILL 信号 |

正如你所见，Ubuntu 服务器上的 MySQL 安装附带了相当多的实用工具。很可能你永远不会使用其中大部分，但了解它们存在（以及它们的作用）在需要时是有益的。

对于与 MySQL 服务器的大多数正常交互，你将使用 mysql 命令行程序，该程序将在下一节中讨论。

## mysql 命令

mysql 命令为 MySQL 服务器提供了一个交互式界面。当你启动该命令时，你会得到一个交互式提示：

```
$ mysql
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 28
Server version: 5.0.67-Debian6.0 (Ubuntu)

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

从 mysql> 提示符你可以直接向 MySQL 服务器提交 SQL 语句和特殊命令。mysql 命令提供了一些命令行参数，允许你在启动时自定义其行为。表 24-3 显示了这些命令行参数。

# 表 24-3：mysql 命令参数

| 参数 | 描述 |
|---|---|
| --auto-rehash | 启用数据库、表和数据字段名称补全 |
| --batch | 使用制表符作为字段分隔符显示结果，每行单独一行 |
| --character-sets-dir=path | 定义字符集安装位置 |
| --column-names | 在结果中显示数据字段名称 |
| --comments | 保留发送到服务器的注释（默认是抑制注释） |
| --compress | 压缩客户端和服务器之间发送的所有信息 |
| --database=dbname | 指定连接到服务器时使用的默认数据库 |
| --debug=[options] | 启用调试，并指定可选的调试设置 |
| --debug-info | mysql 退出时显示调试信息 |
| --default-character-set=name | 定义默认字符集 |
| --delimiter=char | 定义 SQL 语句分隔符（默认为分号） |
| --disable-named-commands | 禁用从命令行使用长格式 MySQL 命令 |
| --execute=statement | 向 MySQL 服务器发送指定的 SQL 语句并退出 |
| --force | 如果发生 SQL 错误则继续 |
| --host=hostname | 连接到指定的主机 |
| --html | 以 HTML 格式显示所有输出 |
| --ignore-spaces | 忽略函数名后放置的空格 |
| --line-numbers | 显示错误的行号 |
| --local-infile[={0|1}] | 启用或禁用 LOAD DATA INFILE 语句的本地功能 |
| --named-commands | 启用长格式 MySQL 命令 |
| --no-beep | 错误发生时不发出可听信号 |
| --no-tee | 不将输出复制到文件 |
| --one-database | 仅允许对命令行上指定的数据库执行 SQL 语句 |
| --pager=command | 使用指定的命令分页输出（通常是 less、more 或 cat 命令） |
| --password[=passwd] | 指定用于连接到 MySQL 服务器的用户密码（如果未指定密码，mysql 会在连接前提示输入密码） |

# 表 24-3：（续）

| 参数 | 描述 |
|---|---|
| --port=num | 指定远程 MySQL 服务器的 TCP 端口（默认为 3306） |
| --prompt=str | 指定要使用的命令行提示符 |
| --protocol=value | 指定如何连接到 MySQL 服务器，TCP、SOCKET、PIPE 或 MEMORY 之一 |
| --quick | 不缓存每个查询的结果 |
| --raw | 不在查询结果周围显示文本框 |
| --reconnect | 如果与 MySQL 服务器的连接丢失，则自动尝试重新连接 |
| --safe-updates | 仅允许使用 WHERE 子句指定要更新或删除的行 UPDATE 和 DELETE 语句（不允许一次更新或删除所有行） |
| --secure-auth | 不向使用旧格式的服务器发送密码 |
| --show-warnings | 在每个 SQL 语句后显示服务器的任何警告 |
| --sigint-ignore | 忽略中断程序的尝试 |
| --silent | 显示更少的输出，例如启动时的版本信息 |
| --skip-column-names | 不在结果集中显示数据字段名称 |
| --skip-line-numbers | 不为错误显示行号 |
| --socket=path | 指定用于连接到 MySQL 服务器的本地套接字文件 |
| --ssl* | 一系列参数，用于指定到 MySQL 服务器的安全连接（如果受支持） |
| --table | 以表格格式显示输出（交互模式下的默认值，但在批处理模式下不是） |
| --tee=file | 将所有输出复制到指定文件 |
| --unbuffered | 在每个查询后刷新命令缓冲区 |
| --user=user_id | 指定用于连接到服务器的 MySQL 用户账户 |
| --verbose | 显示比正常更多的输出 |
| --version | 显示 mysql 程序的版本 |
| --vertical | 垂直显示数据字段名称和值，每行一个数据字段 |
| --wait | 如果连接服务器失败则重试连接 |
| --xml | 以 XML 格式显示所有输出 |

