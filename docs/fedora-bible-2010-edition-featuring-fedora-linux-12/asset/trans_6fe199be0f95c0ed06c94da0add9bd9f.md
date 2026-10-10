
![Figure 23-1](img/c78bdcb5b7842a0d73dcc98921f872a2_868_0.png)

**图 23-1：使用 MySQL 管理员窗口连接到你的 MySQL 数据库。**

此时，你可以使用 MySQL 管理员窗口来查找有关 MySQL 服务器的信息，备份和恢复数据，或者选择“目录（Catalogs）”以显示每个数据库的信息。你甚至可以选择“健康（Health）”选项来查看有关服务器机器活动和使用情况的各种信息。（如果你想尝试另一种图形化 MySQL 实用工具，请查看 `mysql-query-browser` 软件包。该工具专为设计 MySQL 表和运行查询而制作。）

## 配置 MySQL 服务器

与 Fedora 中的大多数服务器软件一样，MySQL 服务器依赖启动脚本和配置文件来提供服务。服务器活动会记录在 `/var/log` 目录下的 `mysqld.log` 文件中。还有用于管理 MySQL 活动的 `mysql` 用户和组账户。以下各节将描述这些组件如何协同工作。

### 使用 mysql 用户/组账户

安装 MySQL 软件时，它会自动创建一个 `mysql` 用户账户和一个 `mysql` 组账户。这些用户和组账户被分配给 MySQL 文件和活动。这样，某人就可以管理 MySQL 服务器，而无需拥有 root 权限。

`mysql` 用户条目在 `/etc/passwd` 文件中显示如下：

```
mysql:x:27:482:MySQL Server:/var/lib/mysql:/bin/bash
```

刚才显示的 `mysql` 条目表明，`mysql` 用户的 UID 为 27，GID 为 482。识别此用户账户的文本字符串是 **MySQL Server**。主目录是 `/var/lib/mysql`，默认 shell 是 `/bin/bash`。识别出的主目录将包含为你定义的 MySQL 服务器每个数据表持有的目录。

`mysql` 的组条目更简单。`/etc/group` 文件中的以下条目表明 `mysql` 组的组 ID（GID）为 482。

```
mysql:x:482:
```

如果你关心与 MySQL 相关的文件的所有权，你会发现大多数这些文件都将 `mysql` 指定为拥有每个文件的用户账户和组账户。这使得由 `mysql` 用户运行的守护进程能够访问数据库文件。

### 添加管理用户

要管理 MySQL，你必须至少拥有一个管理账户。默认情况下，root 用户对你的 MySQL 服务器数据库拥有完全访问权限，并且没有分配密码。一旦 `mysqld` 服务器正在运行，你可以使用 `mysqladmin` 命令为 root 用户分配密码。要将 root 用户添加为 MySQL 管理员，请登录为 root 用户，并从终端窗口输入以下任一命令（替换为你自己的主机名和密码）：

```
# mysqladmin -u root password 'myownpassw'
# mysqladmin -u root -h myhost.example.com password 'myownpassw'
```

> **提示：** 如果你的密码中包含也被 shell 解释为元字符的字符，请将密码包含在引号中。

运行此命令后，MySQL root 用户可以使用密码运行任何 MySQL 管理命令。如果你忘记了或重置了你的 MySQL 密码，请参阅此处信息：`http://dev.mysql.com/doc/refman/5.0/en/resetting-permissions.html`。

MySQL 维护一个与操作系统维护的列表不同的用户和密码列表。如果在命令行中没有提供用户名（如上所示的 `-u root`），MySQL 假设你想使用当前的 Fedora 用户名登录到 MySQL。然而，你仍然需要提供该用户的 MySQL 密码（而不是 Fedora 密码）才能使用 MySQL 服务。

要进行 MySQL 管理，只需在你要运行的 MySQL 命令的命令行中添加 `-u root` 参数。在创建 MySQL 账户之后，Linux root 用户与 MySQL root 用户账户之间没有关联。通常你会为这两个账户使用不同的密码。

**提示：** 为了避免每次运行 MySQL 客户端命令时都要输入密码的麻烦，你可以在其中一个选项文件的 `[client]` 组下添加一个密码选项。最安全的方法是创建 root 用户主目录中的一个 `.my.cnf` 文件，该文件只能由 root 访问（`chmod 600 /root/.my.cnf`），并包含以下行（将显示的最后参数替换为你的密码）：

```
[client]
password=mypasswd
```

### 设置 MySQL 选项

你可以通过使用选项文件或命令行参数来设置影响 MySQL 应用程序行为的选项。MySQL 服务器（以及其他管理工具）在启动时（如果这些文件存在）会读取以下选项文件：

- `/etc/my.cnf` — 包含由 mysqld（服务器守护进程）和 mysql.server（启动服务器守护进程的脚本）读取的全局选项。
- `--defaults-extra-file=` — 包含作为文件名在命令行上传递给服务器以使用的选项。例如，以下命令会导致在读取全局选项之后、读取用户特定选项之前，读取 `/home/jim/my.cnf` 文件中的选项：

  ```
  # /usr/libexec/mysqld --defaults-extra-file=/home/jim/my.cnf
  ```

- `$HOME/.my.cnf` — 包含用户特定选项。（$HOME 指用户的主目录，例如 `/home/susya`）。

表 23-1 显示了读取这些选项文件（按上述列表中的顺序）并在其处理中使用这些选项的 MySQL 命令。选项包含在由方括号内的单个单词标识的组中。表中还显示了由每个命令读取的组名。

虽然你可以使用任何选项文件来设置 MySQL 选项，但请从配置 `/etc/my.cnf` 文件开始。稍后，如果你想覆盖该文件中设置的任何值，可以使用其他选项文件或命令行参数来执行此操作。

#### 表 23-1：与 MySQL 命令关联的选项组

| 命令 | 描述 | 组名 |
| :-- | :-- | :-- |
| mysqld (in /usr/libexec) | MySQL 服务器守护进程 | [mysqld] [server] |
| mysqld_safe | 由 mysqld 启动脚本运行以启动 MySQL 服务器 | [mysqld] [server] [mysql.server] |
| mysql | 提供用于显示和操作 MySQL 数据库的命令行界面 | [mysql] [client] |
| mysqldadmin | 用于创建和维护 MySQL 数据库 | [mysqldadmin] [client] |
| myisamchk | 用于检查、修复和优化 MySQL 数据库（.my1 后缀） | [myisamchk] |
| myisampack | 用于压缩 MyISAM 数据库表 | [myisampack] |
| mysqldump | 提供基于文本的接口以备份 MySQL 数据库 | [mysqldump] [client] |
| mysqlimport | 将纯文本数据文件加载到 MySQL 数据库中 | [mysqlimport] [client] |
| mysqlshow | 显示你选择的 MySQL 数据库和表 | [mysqlshow] [client] |

### 创建 my.cnf 配置文件

影响 MySQL 服务器和相关客户端程序运行的全局选项在 `/etc/my.cnf` 文件中定义。默认的 `my.cnf` 文件仅包含启动小型 MySQL 配置所需的几个设置。以下是 MySQL 附带的 `/etc/my.cnf` 文件的一个示例：

```
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
user=mysql
# Default to using old password format for compatibility with mysql 3.x
# clients (those using the mysqlclient10 compatibility package).
old-password=1

# To allow mysqld to connect to a MySQL Cluster management daemon, uncomment
# these lines and adjust the connectionString as needed.
#ndbcluster
#ndb-connectstring="nodeId=4;host=localhost:1186"

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid

[ndbd]
# If you are running a MySQL Cluster storage daemon (ndbd) on this machine,
# adjust its connection to the management daemon here.
# Note: ndbd init script requires this to include nodeId:
connect-string="nodeId=2;host=localhost:1186"

[ndb_mgm]
# connection string for MySQL Cluster management tool
connect-string="host=localhost:1186"
```

