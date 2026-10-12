
`mtop --user=root`

## 让您的 MySQL 服务器

### 通过以下节省时间

- 在您的 MySQL 服务器上设置复制
- 使用 `mysqld` 备份 MySQL 数据
- 使用文件系统工具
- 使用 `MySQL Administrator` 业务

MySQL 是一种快速、强大且低成本的数据库，随大多数 Linux 系统发布。您可以使用 MySQL 存储业务记录、比赛得分、用户帐户信息、网络配置以及任何内容。

我们没有足够的空间提供 MySQL 的全面概述（我们推荐 Paul Dubois 的优秀著作《MySQL New Riders/Sams Publishing》），因此我们提供了一些可以改进数据库的技巧。在本技巧中，我们涵盖了以下主题：

- 轻松安装 MySQL。MySQL 团队将复杂的程序变成了两个步骤的操作。
- 使用 MySQL 复制功能将数据推送到远程分支（或将重负载分散到多个服务器上）。
- 使用 MySQL 专用工具或文件系统工具备份您的数据。
- 使用新兴工具 `MySQL Administrator`。`MySQL Administrator` 是由 MySQL 团队编写的企业级控制中心。它为 MySQL 4 版本及更高版本设计，但许多情况下也适用于旧版本。

# 构建 MySQL 服务器

MySQL 软件采用双重许可方案发布。如果你不是作为闭源软件包的一部分重新分发 MySQL，你可以根据 GNU 公共许可证（GNU Public License）使用 MySQL。如果你将 MySQL 作为专有软件重新分发，或者希望获得 MySQL AB 的保修支持，你将必须购买许可证。我们不是律师，请访问 MySQL 网站 `www.mysql.com` 查看官方政策。

# 启动 MySQL 服务器

在使用 MySQL 之前，你首先需要启动 MySQL 服务器：

1. 打开主菜单并选择系统：服务（`System:Services`）（或者如果你使用 GNOME，选择设置：服务器；`Settings:Server; 服务；Settings:Services`）。
2. 如果提示，输入 `root` 密码。
3. 滚动服务列表（左侧列），找到名为 `mysqld` 的服务。
4. 勾选 `mysqld` 左侧的复选框，然后点击工具栏上的保存（`Save`）。
5. 点击工具栏上的启动（`Start`）。

将出现一条消息，确认 `mysqld` 服务已成功启动。

# 构建 MySQL 服务器

如果你在 MySQL 网站的安装说明上遇到过困难，你会高兴地知道，在 Linux 上创建 MySQL 服务器是非常简单的。MySQL 团队遵循了关于你行为的所有指令，并将所有内容封装在一个整洁的 RPM 包中，为你完成了一切工作。

6. 点击确定并关闭服务配置窗口。

开始之前，使用你的发行版安装 MySQL 服务器、MySQL 客户端以及所有必要的依赖。

你必须在 MySQL 服务器上拥有超级用户权限。打开终端窗口并使用命令赋予所需的权限。

如果你是 Fedora 用户，请使用 Raddit 并选择数据库：其他：MySQL。Rapidrake 会自动安装 MySQL 客户端和整套依赖项。

在 Mandrake 系统上启动 MySQL 服务器，输入以下命令：

```bash
# /etc/init.d/mysql start
```

如果你是 Fedora 用户，请使用添加/删除软件包（`Add/Remove Packages`）并滚动到部分列表。点击 SQL 数据库详情链接并选择 `MySQL-server`。Fedora 会自动为你安装所有依赖项和 MySQL 客户端软件。

在 SUSE 计算机上，使用此命令：

```bash
# /usr/sbin/rcmysql start
```

如果你正在运行 Fedora，使用以下命令：

```bash
# /etc/init.d/mysql start
```

SUSE 粉丝应该使用 `yaST2` 安装 MySQL。你可以在生产力：数据库：服务器中找到 MySQL。像 Fedora 和 Mandrake 安装程序一样，`yaST2` 将安装 MySQL 客户端软件和任何依赖项。

MySQL 已经在运行。当你第一次使用 MySQL 服务器时，它会创建一个服务器环境和一个名为 `test` 的空数据库。

你的 MySQL 数据库数据文件存储在 `/var/lib/mysql/` 目录下。为了方便起见，请参考该目录 `$MYSQL`。

![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_347_0.png)
![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_347_1.png)

# 33 技巧 44：让你的 MySQL 服务器成为你的 SQL 服务器

系统崩溃或正常维护；从库数据库可以接管。

- 它提升了你数据库的整体性能。在另一台计算机上创建一个复制从库，你就将负载分散到了两个系统上。MySQL 的复制架构使其易于配置你需要的任意从库服务器。

首次启动服务器时，为 `root` 用户创建一个 MySQL 密码：

- 打开终端并为自己赋予超级用户权限：

```bash
$ su
Password:
```

- 输入以下命令（将 `password` 替换为你理想的密码）：

```bash
$ mysqladmin -u root password new-password
```

- 当你备份数据时，它能提高可用性。因为从库包含与主库相同的数据，你可以将从库下线，并从那里而不是主服务器恢复数据。

# 配置复制：三种拓扑结构

现在你准备好使用你的 MySQL 服务器了。如果你已经熟悉 MySQL，我们在本章中为你提供的节约时间的技巧会少一些。如果不是，是时候用读读书了。你可以在本地商店（或书店）找到各种关于 MySQL 的书籍，我们恰恰认为 Paul Dubois 写的《MySQL [New Riders/Sams Publishing]》是最好的。

不同的供应商提供复制拓扑结构（复制系统的拓扑结构描述了哪些服务器将数据推送到其他服务器）。MySQL 支持三种基本的拓扑结构：

- 单主/单从
- 单主/多从
- 单主/链从

# 复制 MySQL 数据

MySQL 支持复制。当你配置复制时，MySQL 会自动将数据修改（`SET`、`UPDATE` 和 `DELETE` 操作）从一个 MySQL 服务器转发到另一个。如果你有一个地理位置分布的组织，MySQL 可以自动将数据从你的中心数据库推送到你的分机构。你对主数据库所做的更改几乎会立即出现在每个远程服务器上。

单主/单从拓扑结构最容易理解。一台服务器充当主，当你更改主库中的一个值时，该修改会被推送到另一个服务器，称为复制从库。

复制从库可以将更改（它从主库接收到的更改）推送到另一台，导致单主/链从拓扑结构。

复制提供了三个重要优点：

- 它提高了你数据库的整体可靠性。如果主数据库由于某些原因（硬件问题、系统崩溃或正常维护）无法使用，从数据库可以接管。
- 数据流单向流动：从主库到从库。复制会将所有修改写入二进制（不可读的）日志文件。当从库连接到主库时，它会读取日志文件并将更改应用到自己的数据副本中。

# 复制 MySQL 数据 33

这意味着你不应该在从库上更改数据。如果你在从库上更改了数据，主库和从库就会不同，你可能会丢失数据。MySQL 允许选择要复制哪些表（不需要复制整个数据库）。这意味着一台服务器可以同时作为某些表的主和其他另一些表的从。

# 设置单从/主复制

创建一个单从/主拓扑结构很容易，但你需要在主从两个服务器上都进行一些工作，如下文所示：

1. 登录主库 MySQL 服务器：

```bash
# mysql

Welcome to the MySQL server. Your MySQL connection is 5 to server version 3.2.58

end with ; or \g.

Type '\help' or '\h' for help.

Type '\c' to clear the buffer.
```

2. 在该部分的末尾添加行：

```ini
[mysql]

log-bin

server-id = 1
```

3. 重启主服务器：

```bash
# service mysql stop
```

在复制从库上，按照以下步骤操作：

1. 关闭 MySQL 服务器：

```bash
# service mysql stop
```

2. 创建一个新的 MySQL 用户账户 - 复制从库将使用此登录主库：

```sql
mysql> GRANT FILE ON * TO 'repl_slave'@IDENTIFIED BY 'repl_pass';

Query OK, 0 rows affected (0.13 sec)
```

3. 编辑 `/etc/my.cnf` 文件并找到起始于：

```ini
[mysql]

master-host = master-hostname

master-user = repl_slave

master-password = repl_pass

server-id = 2
```
