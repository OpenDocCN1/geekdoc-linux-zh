
停止自动显示每条语句生成的任何警告。此命令在 `MySQL` 5.0.6 中引入。

- `pager [program]`, `\P [program]`

  通过 `program` 指定的分页程序发送输出，或者如果设置了 `PAGER` 环境变量且未指定 `program`，则通过该变量指定的程序发送输出。此命令在 Windows 下不可用。

- `print`, `\p`

  打印当前语句（语句本身的文本，而不是执行它获得的结果）。

- `prompt [arguments]`, `\R [arguments]`

  重新定义主要 `mysql>` 提示符。`prompt` 关键字后第一个空格之后的所有内容都成为提示符字符串的一部分，包括其他空格。该字符串可以包含特殊序列，如第 F.5.5 节“`mysql` 提示符定义序列”中所述。要将提示符恢复为默认设置，请不带参数指定 `prompt` 或 `\R`。

- `quit`, `\q`

  退出 `mysql`。

- `rehash`, `\#`

  重新计算数据库、表和列名补全所需的信息。参见 `--auto-rehash` 选项的说明。

- `source file_name`, `\.` `file_name`

  读取并执行指定文件中包含的语句。对于包含反斜杠（`\`）路径分隔符的 Windows 文件名，请加倍使用它们，或使用斜杠（`/`）代替指定。

- `status`, `\s`

  从服务器获取并显示状态信息。如果您想检查服务器版本、默认数据库、连接是否安全等，这将很有用。

- `system command`, `\!` `command`

  使用您的默认命令解释器执行 `command`。此命令在 Windows 下不可用。

- `tee [file_name]`, `\T [file_name]`

  将输出复制到指定文件的末尾。

- `use db_name`, `\u` `db_name`

  选择给定的数据库使其成为默认数据库。

- `warnings`, `\W`

  自动显示每条语句生成的任何警告。此命令在 `MySQL` 5.0.6 中引入。

### F.5.5 mysql 提示符定义序列

可以使用 `MYSQL_PSI` 环境变量、`--prompt` 选项或 `prompt` 命令来重新定义 `mysql` 打印的主要 `mysql>` 语句提示符。例如，要在提示符中包含默认数据库的名称，请按照以下方式使用 `prompt` 命令，然后选择不同的数据库以查看提示符如何跟随当前选择：

```
% mysql
mysql> prompt \d>\
PROMPT set to '\d>\,'
(none)> USE sampledb;
Database changed
sampledb> USE test;
Database changed
test>
```

提示符关键字后跟提示符定义字符串。在定义内部，以反斜杠开头的转义序列表示特殊的提示符选项。`\d` 和 `\_` 序列分别表示默认数据库名称和一个空格。（如果使用环境变量或 `--prompt` 选项设置提示符，您可能需要在使用提示符字符串时加倍使用反斜杠。）下表显示了可用选项的完整列表。

| 序列 | 含义 |
| :--- | :--- |
| `\c` | 当前输入行号 |
| `\d` | 默认数据库名称，如果未选择数据库则为 "(none)" |
| `\D` | 完整日期和时间 |
| `\h` | 当前主机 |
| `\l` | 当前分隔符（自 MySQL 5.0.25/5.1.12 起） |
| `\m` | 分钟 |
| `\o` | 月份数字 |
| `\O` | 月份名称，三个字母 |
| `\p` | 当前端口号、套接字文件名、命名管道名称或共享内存名称 |
| `\P` | 时间值的 am 或 pm 指示器 |
| `\r` | 小时（12小时制） |
| `\R` | 小时（24小时制） |
| `\s` | 秒 |
| `\S` | 分号 |
| `\t` | 制表符 |
| `\u` | 当前用户名，不包括主机名 |
| `\U` | 当前用户名，包括主机名 |
| 序列 | 含义 |
|---|---|
| `\v` | 服务器版本 |
| `\w` | 星期几名称，三个字母 |
| `\y` | 年份（两位数） |
| `\Y` | 年份（四位数） |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\_` | 空格字符 |
| `\ ` | 空格字符（序列为反斜杠加空格） |
| `\\` | 字面量 `'` |
| `\n` | 换行符（行尾换行） |
| `\x` | 对于未在其他地方列出的任意 `'x'`，表示字面量 `'x'` |

### F.6 mysql.server

`mysql.server` 通过调用 `mysqld_safe` 来启动和停止 `mysqld` 服务器。`mysql.server` 是一个 shell 脚本，仅可在 Unix 上使用。`mysql.server` 理解 `start` 或 `stop` 形式的命令行参数：

- `mysql.server start`
- `mysql.server stop`

通常，在那些使用 `/etc` 目录层级结构的 Unix 系统中，`mysql.server` 被安装在运行级别目录中。（安装后的版本通常命名为 `mysql` 而不是 `mysql.server`。）系统通过在系统启动时以 `start` 参数调用该脚本来启动服务器。系统通过在系统关闭时以 `stop` 参数调用该脚本来关闭服务器。也可以手动以相应的参数调用该脚本来启动或停止服务器。

#### F.6.1 mysql.server 支持的选项

`mysql.server` 对标准 MySQL 选项的支持是有限的。它不从命令行读取任何标准选项。在选项文件中的 `[mysql.server]` 组内，它读取 `basedir`、`datadir` 和 `pid-file` 选项并将其传递给 `mysqld_safe`。自 MySQL 5.0.40/5.1.17 起，`service-startup-timeout=n` 选项指示脚本应等待服务器启动的秒数。默认值为 900。值为 0 表示“不等待”，负值表示“永久等待”。

### F.7 mysql_config

`mysql_config` 实用程序是辅助开发用 C 语言编写的基于 MySQL 的程序的一个工具。可以调用它来获取编译 C 源文件或链接 MySQL 库所需的正确标志：

```
mysql_config [options]
```

#### F.7.1 mysql_config 特有的选项

- `--cflags`

  显示访问 MySQL 头文件及其他可能必要的 C 编译器所需的 include 目录标志。

- `--embedded, --embedded-libs`

  这些选项是 `--libmysql-libs` 的同义词。

- `--include`

  显示访问 MySQL 头文件所需的 include 目录标志。

- `--libmysql-libs`

  显示链接嵌入式服务器库 `libmysql` 所需的库标志。

- `--libs`

  显示链接客户端库所需的库标志。

- `--libs_r`

  显示链接线程安全客户端库所需的库标志。

- `--plugindir`

  显示默认插件目录。此选项在 MySQL 5.1.24/6.0.5 中引入。

- `--port`

  显示默认 TCP/IP 端口号。

- `--socket`

  显示默认 Unix 套接字文件路径名。

- `--version`

  显示 MySQL 版本字符串。

### F.8 mysql_install_db

`mysql_install_db` 脚本创建服务器的数据目录，初始化包含权限表的 `mysql` 数据库，并创建一个空的 `test` 数据库：

```
mysql_install_db [options]
```

`mysql_install_db` 使用初始账户填充权限表，这些账户属于 `root` 用户和匿名用户。有关这些账户以及如何通过设置密码来保护您的安装的详细信息，请参阅第 12 章“常规 MySQL 管理”。

`mysql_install_db` 在 Windows 上不可用，但这并不必要，因为 Windows 发行版包含一个预初始化的数据目录。

#### F.8.1 mysql_install_db 支持的标准选项

`--help` `--user`

`--help` 自 MySQL 5.0.4/5.1.21 起可用。

在 Unix 上，`--user` 选项使用指定用户的登录账户运行服务器。如果您以 Unix `root` 用户身份运行 `mysql_install_db`，这有助于确保服务器创建的任何目录和文件都归该用户所有。

#### F.8.2 mysql_install_db 特有的选项
