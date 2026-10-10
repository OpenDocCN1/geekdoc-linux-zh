

# ## 设置 MySQL 选项

MySQL 维护一个独立于 CentOS 维护的用户名和密码列表。如果未在命令行中提供用户名（如上文所示的 `-u root`），MySQL 将假设您希望使用当前的 CentOS 用户名登录到 MySQL。但是，您仍需提供该用户的 MySQL 密码（而不是 CentOS 密码）才能使用 MySQL 服务。

如果您想要进行 MySQL 管理，只需在正在运行的 MySQL 命令的命令行中添加 `-u root` 参数即可。在创建 MySQL root 账户后，Linux root 用户账户与 MySQL root 用户账户之间没有任何关联。您通常会为这两个账户使用不同的密码。

> 为了避免每次运行 MySQL 客户端命令时都要输入密码的麻烦，您可以在其中一个选项文件的 `[client]` 组下添加密码选项。最安全的做法是在 root 用户的主目录中创建一个仅 root 可访问的 `.my.cnf` 文件（输入 `chmod 600 /root/.my.cnf`），并包含以下内容（将最后一行显示为您的密码）：

```
[client]
password=mypassword
```

通过使用选项文件或命令行参数，您可以设置影响 MySQL 应用程序行为的选项。MySQL 服务器（以及其他管理工具）在启动时读取以下选项文件（如果这些文件存在）：

- `/etc/my.cnf` — 包含由 `mysqld`（服务器守护进程）和 `mysql.server`（启动服务器守护进程的脚本）读取的全局选项。
- `--defaults-extra-file` — 您可以在命令行上指定一个包含服务器要使用的选项的文件。例如，以下命令将在读取全局选项之后、读取用户特定选项之前读取文件 `/home/timothy/my.cnf` 中的选项：
  ```
  mysqld --defaults-extra-file=/home/timothy/my.cnf
  ```
- `$HOME/my.cnf` — 包含用户特定的选项。（`$HOME` 指代用户的主目录，例如 `/home/timothy`。）

表 23-1 显示了读取选项文件（按前一个项目符号列表中显示的顺序）并在处理过程中使用这些选项的 MySQL 命令。选项包含在由括号内的单个单词标识的组中。表中还显示了每个命令读取的组名称。

# 第四部分 网络

### 表 23-1
与 MySQL 命令相关的选项组

| 命令 | 描述 | 组名称 |
| :--- | :--- | :--- |
| mysqld (in /usr/libexec) | MySQL 服务器守护进程 | [mysqld] [server] |
| mysqld_safe | 由 mysqld 启动脚本运行以启动 MySQL 服务器 | [mysql] [server] [mysqld.server] |
| mysql | 提供用于显示和操作 MySQL 数据库的命令行界面。 | [mysql] [client] |
| mysqladmin | 用于创建和维护 MySQL 数据库 | [mysqladmin] [client] |
| myisamchk | 用于检查、修复和优化 MyISAM 数据库（_my 后缀） | [myisamchk] |
| myisampack | 用于压缩 MyISAM 数据库表 | [myisampack] |
| mysqldump | 提供用于备份 MySQL 数据库的基于文本的界面 | [mysqldump] [client] |
| mysqlimport | 将纯文本数据文件加载到 MySQL 数据库中 | [mysqlimport] [client] |
| mysqlshow | 显示您选择的 MySQL 数据库和表 | [mysqlshow] [client] |

### 创建 my.cnf 配置文件

影响 MySQL 服务器和相关客户端程序运行的全局选项在 `/etc/my.cnf` 文件中定义。默认的 `my.cnf` 文件仅包含让小型 MySQL 配置运行所需的少量设置。以下是 CentOS 的 `mysql` 包中附带的 `/etc/my.cnf` 文件的一个示例。

```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
user=mysql

# Default to using old password format for compatibility with mysql 3.x
# clients (those using the mysqlclient10 compatibility package).
old_passwords=1
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
```

### 设置 MySQL 数据库服务器

默认 **my.cnf** 文件中的大多数设置定义了 `mysqld` 服务器所需的文件和目录位置。每个选项都与某个特定的组相关联，每个组由方括号中的名称标识。上述选项与 `mysqld` 守护进程（`[mysqld]`）以及启动 `mysqld` 守护进程的 `safe_mysqld` 脚本（`[mysqld_safe]`）相关联。（有关这些组的列表，请参阅表 23-1。）

默认的 **datadir** 值表示 `/var/lib/mysql` 是存储您创建的 MySQL 数据库的目录。**socket** 选项将 `/var/lib/mysql/mysql.sock` 识别为用于创建与 `mysqld` 服务器相关的 MySQL 通信端点的套接字。**user** 选项将 `mysql` 识别为具有管理 MySQL 服务权限的用户账户。根据 **old_passwords**=`1` 值，您的 MySQL 数据库将使用以前 MySQL 3.x 数据库使用的密码格式。

**log-error** 和 **pid-file** 选项告诉 `safe_mysqld` 脚本错误日志（`/var/log/mysqld.log`）和存储 `mysqld` 守护进程运行时的进程 ID 的文件（`/var/run/mysqld/mysqld.pid`）的位置。`safe_mysqld` 脚本实际上是从 `mysqld` 启动脚本启动 `mysqld` 守护进程的。

> **注意**
> 跟在组名后面的每个选项都被分配给该组。组分配在新组开始或到达文件末尾时结束。

### 选择选项

MySQL 服务器使用了许多未在 **my.cnf** 文件中明确定义的值。查看 MySQL 服务器和客户端可用选项的最简单方法是使用 **--help** 选项运行每个命令。例如，要查看可用的 `mysqld` 选项（以及其他信息），请从终端窗口输入以下内容：

```
/usr/libexec/mysqld --verbose --help | less
```

然后按空格键逐屏查看信息。（下一节中显示了此输出的示例。）

您也可以使用 `man` 命令查找可用的选项。例如，要查看 `mysqld` 守护进程可用的设置选项，请输入以下内容：

```
man mysqld
```

很可能您可以尝试运行您的 MySQL 数据库服务器而无需更改任何选项。但是，在将 MySQL 数据库服务器设置为生产环境后，您几乎肯定希望调整服务器以匹配服务器的使用方式。例如，如果它是专用的 MySQL 服务器，您将希望允许 MySQL 消耗比默认情况下更多的系统资源。

以下列表显示了一些您可能想为 MySQL 设置的额外选项示例：

- `password=yourpwd` — 将此选项添加到用户 `$HOME/.my.cnf` 文件中的 `[client]` 组，允许用户在运行 MySQL 客户端命令时无需每次输入密码。（将 `yourpwd` 替换为用户的密码。）
- `port=#` — 定义 MySQL 服务监听 MySQL 请求的端口号。（将 `#` 替换为您想使用的端口号。）默认情况下，MySQL 在 TCP 和 UDP 协议上监听端口号 3306。
- `safe-mode` — 告诉服务器在启动时跳过某些优化步骤。
- `tmpdir=path` — 指定一个目录（除默认 `/tmp` 外），供 MySQL 用于写入临时文件。（将 `path` 替换为完整路径名。）

除了您可以设置的选项外，MySQL 客户端还有许多您可以设置的变量。变量设置缓冲区大小、超时值和可接受的包长度等。这些变量也列在 `--help` 输出中。要更改变量值，可以使用 `--set-variable` 选项，后跟变量名和值。例如，要将 `sort_buffer` 变量设置为 10 MB，您可以在您的 `[mysqld]` 组下添加以下选项：

```
[mysqld]
set-variable=sort_buffer=10M
```

以下列表识别了您可以为服务器设置的其他变量。通常，提高这些变量的值可以改善性能，但也会消耗更多的系统资源。因此，在并非专用于 MySQL 或内存资源有限的机器上提高这些值时需要小心。

> **注意** 对于需要您输入大小的变量，使用 M 表示兆字节（例如，10M）或使用 K 表示千字节（例如，256K）来表示大小。

- `key_buffer_size=size` — 设置用于保存所有线程使用的索引块的缓冲区大小。这是提高 MySQL 性能需要提高的关键值。
- `max_allowed_packet=size` — 限制单个数据包的最大大小。如果需要处理非常大的列，请提高此限制。
- `myisam_sort_buffer_size=size` — 设置用于在修复索引、创建索引或更改表时排序的缓冲区大小。
- `sort_buffer=size` — 定义分配给需要执行排序的每个线程的缓冲区大小。提高此值会使排序线程运行得更快。
- `table_cache=#` — 限制所有线程可以同时打开的表总数。此变量的数量代表 MySQL 可以同时打开的文件描述符总数。

