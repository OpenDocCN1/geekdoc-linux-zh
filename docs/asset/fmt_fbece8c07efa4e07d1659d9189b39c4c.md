
![](img/f4a88d4bf9ae965be31d8ef5c6d98f93_336_0.png)

图 5-81 Domino Designer - `LASTNAME` 数据选择

对于“数据连接资源”选择 `DB2`；对于“表”选择 `ADMINATOR.EMPLOYEE`；对于“列”选择 `LASTNAME`；然后点击 `OK`。回到属性对话框，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

对于 `EmployeeForm` 中的所有剩余字段，重复上述步骤：启用“外部数据源”（External data source），在“数据源选项”（Data Source Options）旁边选择“浏览”（Browse）。在属性对话框中，启用“本地存储数据”（Store data locally）。这允许你在视图中查看数据。

## 5.4.1 环境说明

推荐的 Domino 服务器配置是使用专用的服务器来运行 Domino 服务器。然而，在我们的实验室环境中，我们在同一台机器上实现了带有 Domino 和 MySQL 的系统。

## Linux

在我们的示例中，我们使用了内核为 `2.4-7-6` 的 `RedHat 7.2`。MySQL 强烈建议使用 `2.4` 内核，因为其稳定性和性能远优于 `2.2` 内核。

### Domino

与 `DB2` 示例一样，假设你已经安装了 `Domino 6`，并在安装过程中选择将 `DECS` 作为额外服务安装。

## MySQL

有关 MySQL 的最新信息以及最新版本的下载，请参阅 MySQL 官网：

```
http://www.mysql.com
```

在开始使用 MySQL 之前，你需要做出以下几个选择：

1. 你想使用哪个版本的 MySQL？MySQL AB 公司建议使用最新的稳定发行版，因为它在功能和稳定性之间取得了最好的平衡。在编写本文时，`3.23` 是当前的推荐版本，而 `4.0` 已以 Beta 版本发布。本文讨论基于 `3.23` 版本，这也是我们在实验室中安装的版本。
2. 你需要解决的选择是哪个 MySQL 产品最适合你的需求。MySQL 3.23 提供了 2 种“口味”：
    - a. MySQL，基础发行版
    - b. MySQL-Max，它为 MySQL 添加了高级功能，特别是事务支持。
  我们选择了基础 MySQL 发行版以保持示例简单。
  MySQL 目前有一个 4.0 Beta 版本可用。如果我们选择使用 4.0 版本，将会有 4 种选项：
    - a. MySQL 4，基础发行版
    - b. MySQL Classic，针对原始速度进行了优化，但不支持事务
    - c. MySQL Pro，本质上是带有事务支持的 MySQL Classic
    - d. MySQL-Max，它提供了两个表处理器（InnoDB & BDB），为 MySQL 提供事务支持
3. 接下来，选择你的 Domino 系统的架构。在某些情况下，将 MySQL 服务器放置在不同的机器上是很有用的。为了简单起见，我们实验室中的 Domino 服务器和 MySQL 服务器都放置在同一台机器上，因此我们的讨论也基于此。
4. 最后一个选择是你希望如何安装 MySQL。对于 Linux 有三种选项：
    - a. 源码安装，这需要在你的机器上编译代码。这提供了最大的灵活性，但也具有最高的复杂性。
    - b. 二进制安装，将所有必要文件编译并组织在一个 tar 文件中。
    - c. rpm 文件，这是最简单的安装方式，甚至可以自动为你启动守护进程。这恰好也是 MySQL 推荐的 Linux 安装方法。

由于我们的演示目标是简单化，因此我们选择了 `rpm` 安装方法。这种安装方法为每个逻辑文件包都提供了一个 rpm 包。以下是 MySQL 手册中的列表：

- `MySQL-VERSION.i386.rpm`

  MySQL 服务器。

- `MySQL-client-VERSION.i386.rpm`

  标准 MySQL 客户端程序。

- `MySQL-bench-VERSION.i386.rpm`

  测试和基准测试。需要 Perl 和 msql-mysql-module rpm。

- `MySQL-devel-VERSION.i386.rpm`

  如果你想编译其他 MySQL 客户端（如 Perl 模块），所需的库和头文件。

- `MySQL-VERSION.src.rpm`

  上述所有包的源代码。

我们想要安装服务器和客户端。

## MyODBC/unixODBC

Domino 不直接支持 MySQL，但它支持 ODBC。你可以使用 MyODBC 来提供驱动程序。MyODBC 的当前稳定版本是 `2.50`；可以从此处下载：

```
http://www.mysql.com
```

MyODBC 需要客户端共享库，因此你需要在安装 MyODBC 之前安装它。这通过 `MySQL-shared-VERSION.i386.rpm` 或 `MySQL-devel-VERSION.i386.rpm` 包提供。

最后，你需要一个 ODBC 来管理 Linux 上的数据源访问。unixODBC 包遵循 `unixODBC-VERSION.i386.rpm` 命名方案（在大多数 Linux 发行版中包含），或者可以从此处下载：

```
http://www.unixodbc.org
```

总结一下，本节的内容：

- `MySQL-VERSION.i386.rpm` 可从 http://www.MySQL.com 获取
- `MySQL-client-VERSION.i386.rpm` 可从 http://www.MySQL.com 获取
- `MySQL-shared-VERSION.i386.rpm` 可从 http://www.MySQL.com 获取
- `MyMySQL-VERSION.i386.rpm` 可从你的 Linux 发行版获取，或从 `unixODBC-VERSION.i386` 可从 http://www.unixodbc.org 获取

## 5.4.2 安装 MySQL

就像安装 Domino 一样，所有安装必须以 `root` 用户身份进行。Linux 不允许 `root` 用户从其他机器登录。要正确安装，你必须以另一个用户登录并使用 `su -` 命令切换到 `root` 用户。

## 服务器和客户端

安装方法是在服务器包和客户端包上运行 `rpm -i`。

```
[root@dnyp-243-89-153 notes]# rpm -iv mysql-client
[root@dnyp-243-89-153 notes]# rpm -iv mysql-shared
[root@dnyp-243-89-153 notes]# rpm -iv mysql-devel
[root@dnyp-243-89-153 notes]# rpm -iv mysql-server
```

```mysql
mysqld = max_connections=256
safe-variable mysqld
open-files-limit = 8192
```

如果你想使用默认配置，可以进入 `/usr/share/mysql` 目录并选择那里的一个配置。

这些示例的命名方案为 `my-SIZE.cnf`（例如，`my-small.cnf`）。

简单地使用以下命令将它们复制到 `/etc` 目录：

```bash
cp /usr/share/mysql/my-SIZE.cnf /etc/my.cnf
```

如果你希望所有表在 `$DATADIR` 自动进行检查和修复，请添加以下行：

```bash
echo "Checking tables in $DATADIR" --silent --force --fast --medium-check -O key
# $MY_BINDIR_VERSION/bin/mysisamck --auto-repair $DATADIR/*.MYI
# $MY_BINDIR_VERSION/bin/mysisamck --silent --force --sort-buffer=64M $DATADIR/*.MYM

echo "Starting $MYSQL daemon with databases from $DATADIR"
renice -20 $$
echo Does this work on all systems?
if type limit | grep 'shell builtin' > /dev/null
then
ulimit -256 > /dev/null 2>&1 # Fix for BSD and FreeBSD system
fi
```

```bash
echo "date '+%Y-%m-%d %H:%M:%S' mysqld started" >>err_log
while true
do
  rm -f $MYSQL_UNIT_PORT $pid_file # Some extra safety
if test -f "$1"
```
