
- `--replicate-rewrite-db=master_db->slave_db`

  告诉复制从服务器将一个数据库视为另一个数据库。在主服务器上对原始数据库 *master_db* 进行的更新将作为对从服务器上数据库 *slave_db* 的更新进行复制。重写仅在 *master_db* 是默认数据库且仅针对操作该数据库中表的语句时生效。在命令行给出时，选项值应包含在引号内，以防止命令解释器将 '`>`' 字符视为输出重定向运算符。可以多次给出此选项。服务器按顺序尝试它们，并使用第一个 *master_db* 值匹配的规则。此选项在其他 `--replicate-xxx` 选项指定的动作测试之前应用，因此如果您使用它，那些选项应使用 *slave_db* 作为数据库名。

- `--replicate-same-server-id` *(布尔值)*

  如果启用此选项，服务器将不会跳过包含其自身服务器 ID 的复制事件。默认情况下，此选项被禁用以防止复制循环，但在某些特殊情况下可以启用。

- `--replicate-wild-do-table=pattern`

  告诉复制从服务器仅复制名称与给定模式匹配的表。要将复制限制在一系列模式，请为每个模式重复使用该选项一次。

- `--replicate-wild-ignore-table=pattern`

  告诉复制从服务器不复制名称与给定模式匹配的表。要忽略多个模式，请为每个模式重复使用该选项一次。

- `--report-host=host_name`

  向主服务器报告从服务器主机是 *host_name*。

- `--report-password=pass_val`

  向主服务器报告从服务器账户密码是 *pass_val*。

- `--report-port=port_num`

  向主服务器报告从服务器端口是 *port_num*。

- `--report-user=user_name`

  向主服务器报告从服务器账户名称是 *user_name*。

- `--rpl-recovery-rank=n`

  此选项未被使用。

- `--server-id=n`

  复制服务器 ID 值。该值必须在 1 到 2^32-1 的范围内，并且必须在相互通信的复制服务器之间唯一。

### F.12.3 mysqld 变量

要查看显示 `mysqld` 将默认使用的系统变量值的完整帮助消息，请使用以下命令：

```plain
% mysqld --verbose --help
```

要查看当前正在运行的 `mysqld` 正在使用的系统变量值，请使用以下命令：

```plain
% mysqladmin variables
```

您也可以通过执行 `SHOW VARIABLES` 语句来检查当前的系统变量值。各个系统变量在附录 D 中进行了描述。可以在启动时按照 F.2.1.2 节“设置程序变量”中给出的说明设置系统变量值。此外，许多系统变量可以动态修改；有关更多信息，请参阅 12.5.1 节“设置和检查系统变量值”以及附录 E 中 `SET` 语句的条目。

### F.13 mysqld_multi

`mysqld_multi` 脚本使在单个主机上运行多个 `mysqld` 服务器变得更加容易。它可以启动或停止服务器，或确定它们是否正在运行：

```
mysqld_multi [选项] 命令 服务器列表
```

`command`（命令） 是 `start`、`stop` 或 `report` 之一。`server_list`（服务器列表）参数指示您要操作哪些服务器。有关使用 `mysqld_multi` 的更多说明，请参阅 12.11.4 节“使用 mysqld_multi 进行服务器管理”。

#### F.13.1 mysqld_multi 支持的标准选项

```
--help --silent --verbose
--password --user --version
```

从 MySQL 5.0.2 开始，`--silent` 和 `--verbose` 可用。

当 `mysqld_multi` 需要停止服务器或确定它们是否正在运行时，它会将 `--user` 和 `--password` 选项值传递给 `mysqladmin`。

#### F.13.2 mysqld_multi 特有的选项

- `-config-file=file_name`

  从 MySQL 5.0.42/5.1.18 开始，该选项已弃用；请改为使用标准的 `-defaults-extra-file` 选项。对于早期版本，该选项指定从中读取以获得 `mysqld_multi` 操作的服务器选项的选项文件；如果没有 `-config-file`，`mysqld_multi` 将读取 `/etc/my.cnf` 和主目录中的 `.my.cnf` 文件以获取服务器选项。（`mysqld_multi` 读取标准选项文件以获取其自身选项。此选项不会改变该行为。）

- `-example`

  显示一个示例选项文件，演示适用于与 `mysqld_multi` 一起使用的选项文件组。

- `-log-file=file_name`

  `mysqld_multi` 应记录其操作的目标日志文件的名称。如果日志已存在，输出将被追加到该日志中。默认日志文件位于数据目录中，名为 `mysqld_multi.log`。要禁用日志记录，请使用 `--no-log`。

- `-mysqladmin=file_name`

  您要使用的 `mysqladmin` 二进制的文件路径名。如果 `mysqld_multi` 无法自行找到 `mysqladmin`，或者您想使用特定版本，这可能很有用。

- `-mysql=file_name`

  您要使用的 `mysqld` 二进制的文件路径名。如果 `mysqld_multi` 无法自行找到 `mysqld`，或者您想使用特定版本，这可能很有用。允许将指向 `mysqld` 或 `mysqld_safe` 的路径名指定为该选项的值。

- `--no-log`

  显示日志输出，而不是将其写入日志文件。如果您想在屏幕上看到输出，必须使用此选项，因为默认是记录到文件。

- `--tcp-ip`

  默认情况下，`mysql` 和 `mysqladmin` 尝试使用 Unix 套接字文件连接到服务器。此选项使连接尝试改用 TCP/IP。当服务器正在运行但其套接字文件已被删除时，这可能很有用，在这种情况下，服务器只能通过 TCP/IP 访问。

### F.14 mysqld_safe

`mysqld_safe` 启动 `mysqld` 服务器并对其进行监控：

```
mysqld_safe [选项]
```

如果服务器停止运行，`mysqld_safe` 将重启它。`mysqld_safe` 是一个 shell 脚本，在 Unix 上可用。还有一个编译版本可用于 NetWare。

#### F.14.1 mysqld_safe 支持的标准选项

```
--help
```

从 MySQL 5.0.3 开始，`--help` 可用。

#### F.14.2 mysqld_safe 特有的选项

可以与 `mysql` 一起使用的选项也可以与 `mysqld_safe` 一起使用，后者只是将它们传递给 `mysqld`。此外，`mysqld_safe` 理解其自身的以下选项：

- `-basedir=dir_name`

  MySQL 基础目录的文件路径名。

- `-core-file-size=n`

  如果服务器崩溃，将核心文件的大小限制为 *n* 字节。

- `-datadir=dir_name`

  MySQL 数据目录的文件路径名。

- `-err-log=file_name`

  这是 `-log-error` 选项的旧形式。

- `--ledir=dir_name`

  查找服务器的目录。（它被认为是 "libexec" 目录的位置。）

- `--log-error=file_name`

  用于错误日志的文件。相对名称是相对于调用 **mysqld_safe** 的目录进行解释的。如果未指定此选项，则默认错误日志是数据目录中的 *HOSTNAME.err*，其中 *HOSTNAME* 是当前主机的名称。

- `--mysqld=file_name**

  **mysqld** 程序的路径。

- `--mysqld-version=suffix`

  此选项的值是一个后缀字符串。如果给出该选项，后缀将添加到基名 **mysqld** 中，中间用连字符分隔，以生成 **mysqld_safe** 应启动的服务器名称。

- `--open-files=n`, `--open-files-limit=n`

  **mysqld** 应保留的文件描述符数量。

- `--pid-file=file_name`

  **mysqld** 进程 ID 文件的名称。

- `--port=port_num`

  服务器应监听 TCP/IP 连接的端口号。
