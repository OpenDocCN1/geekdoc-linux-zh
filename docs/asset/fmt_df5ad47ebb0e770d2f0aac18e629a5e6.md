
请确保放入公共选项组中的任何选项都被你运行的所有服务器理解。例如，如果你的任何服务器早于 5.1.6 版本，你就不能使用 `event_manager=1` 来启用事件调度器，因为事件功能是在 5.1.6 版本中引入的。如果在公共选项组中存在该选项，会导致较旧服务器启动失败。

如果你的所有服务器都是 MySQL 4.0.2 或更新版本，可以使用 `loose-opt_name` 语法来指定不被所有服务器理解的选项。如果服务器以这种方式收到其不理解的选项，它将忽略该选项，在记录警告后继续执行。有关“loose”选项的更多信息，请参阅第 F.1 节“指定程序选项”。

- 使用 `mysqld_multi` 脚本来管理多个服务器的启动。此脚本允许你在单个文件中列出所有服务器的选项，但将每个服务器与该文件中其特定的选项组相关联。
- 在 Windows 下，你可以运行多个服务，使用这种服务器配置方式特有的特殊选项文件组命名约定。请参阅第 12.2.2.2 节“将服务器作为 Windows 服务运行”。

以下各节通过演示如何使用 `mysqld_multi` 以及在 Windows 下如何运行多个服务器，展示了应用这些策略的一些方法。

### 12.10.4 使用 mysqld_multi 进行服务器管理

在 Unix 上，通常用于启动服务器的 `mysqld_safe` 和 `mysqld.server` 脚本在单服务器环境下效果最佳。为了更方便地处理多个服务器，可以使用 `mysqld_multi` 脚本来替代。

`mysqld_multi` 基于以下原理工作：你为想要创建的每个服务器配置分配一个特定的数字，然后在该数字对应的选项组（`[mysqldn]` 组，其中 n 是该数字）中列出该服务器的选项。选项文件还可以包含一个 `[mysqld_multi]` 组，其中列出了专门用于 `mysqld_multi` 本身的选项。例如，如果我安装了 MySQL 5.0.56、5.1.24 和 6.0.5 的服务器，我可能会将它们的选项组指定为 `[mysqld50056]`、`[mysqld50124]` 和 `[mysqld60005]`，并在 `/etc/my.cnf` 文件中如下设置选项：

```ini
[mysqld50056]
basedir=/var/mysql/50056
datadir=/var/mysql/50056/data
mysqld=/var/mysql/50056/bin/safe_mysqld
socket=/var/mysql/50056/mysql.sock
port=50056
user=mysql
log=1og
log-bin=binlog
innodb_data_file_path = ibdata1:100M
```

### 12.10.5 在 Windows 上运行多个服务器

在 Windows 上运行多个服务器有几种方法。一种方法基于手动启动服务器，另一种方法是使用多个 Windows 服务。如果你愿意，可以混合使用这两种方法。

若要手动启动多个服务器，请为每个服务器创建一个选项文件，其中列出其参数。例如，若要运行两个使用相同程序二进制文件但数据目录不同的服务器，你可能需要创建两个如下所示的选项文件：

`C:\my.ini1` 文件：

```
[mysqld]
basedir=C:/mysql
datadir=C:/mysql/data
port=3306
```

`C:\my.ini2` 文件：

```
[mysqld]
basedir=C:/mysql
datadir=C:/mysql/data2
port=3307
```

在启动服务器之前，数据目录必须存在，因为 Windows 没有 `mysql_install_db` 的等效命令。如果将 MySQL 安装到 `C:\mysql`，那么 `C:\mysql\data` 应该已经为你创建好了。设置 `C:\mysql\data2` 最简单的方法是将其创建为 `C:\mysql\data` 的副本。使用以下命令（在没有任何服务器运行时）：

```
C:\> xcopy C:\mysql\data C:\mysql\data2 /E
```

然后从命令行启动服务器，使用 `--defaults-file` 告诉每个服务器读取特定的选项文件：

```
C:\> mysql --defaults-file=C:\my.ini1
C:\> mysql --defaults-file=C:\my.ini2
```

客户端连接时，应指定与其想要访问的服务器相对应的端口号。这包括使用 `mysqladmin` 关闭服务器。以下命令中，第一条使用默认端口（3306），第二条明确指定端口 3307：

```
C:\> mysqladmin -p -u root shutdown
C:\> mysqladmin -p -u root -P 3307 shutdown
```

要将 MySQL 服务器安装为 Windows 服务，请使用 `--install` 选项。例如，要将 `mysqld` 安装为服务，你可能需要使用以下命令之一：

```
C:\> C:\mysql\bin\mysqld --install
C:\> C:\mysql\bin\mysqld --install service_name
```

`--install` 命令使用服务器的完整路径名。如果没有提供 `service_name` 参数，或者名称为 MySQL，则使用默认服务名称（MySQL）；否则，使用给定的名称。（关于在两种情况下读取哪些选项组的规则，见第 12.2.2.2 节“将服务器作为 Windows 服务运行”。）

假设你要运行两个 `mysqld` 实例，使用服务名称 MySQL 和 `mysqldsvcc2`，共享内存名称 MySQL 和 `mysqldsvcc2`，并使用前面示例中所示的相同数据目录。按照以下方式在每个服务器的标准选项文件（如 `C:\my.ini`）中设置选项：

```ini
# 默认 (*MySQL*) 服务的组
[mysqld]
basedir=C:/mysql
datadir=C:/mysql/data
port=3306
shared-memory
shared-memory-base-name=MYSQL

# *mysqldsvcc2* 服务的组
[mysqldsvcc2]
basedir=C:/mysql
datadir=C:/mysql/data2
port=3307
shared-memory
shared-memory-base-name=mysqldsvcc2
```

组的顺序很重要。安装在默认服务名称 MySQL 下的服务器仅读取 `[mysqld]` 选项组。然而，安装在非默认服务名称 `mysqldsvcc2` 下的服务器会读取 `[mysqld]` 和 `[mysqldsvcc2]` 这两个组。通过将 `[mysqldsvcc2]` 组放在选项文件的第二位，可以使用它来覆盖 `[mysqld]` 组中所有不适合作为 `mysqldsvcc2` 服务运行的服务器的选项值。

要安装并启动服务，请使用这些命令：

```
C:\> C:\mysql\bin\mysqld --install
C:\> net start MySQL
C:\> C:\mysql\bin\mysqld --install mysqlsvc2
C:\> net start mysqlsvc2
```

如果你提供了一个服务名称，在安装服务器时，也可以在命令行中指定 `--defaults-file` 选项作为最后的选项：

```
C:\> C:\mysql\bin\mysqld --install service_name --defaults-file=file_name
```

这为你提供了提供特定服务器选项的另一种方式。该文件的名称会被记住，并在服务器每次启动时由服务器使用，它仅从该文件的 `[mysqld]` 组中读取选项。

当有多个服务器正在运行时，客户端可以使用默认的 TCP/IP 端口或共享内存名称连接到默认服务器。要连接到第二个服务器，请明确指定其 TCP/IP 或共享内存参数：

```
C:\> mysql --protocol=tcp --port=3307
C:\> mysql --protocol=memory --shared-memory-base-name=mysqlsvc2
```

要关闭服务器，请使用 `mysqladmin shutdown`、`net stop` 或服务管理器。要卸载服务，请先关闭正在运行的服务器，然后指定 `--remove` 以及在服务器安装时使用的相同服务名称来删除每个服务。如果服务名称是默认名称（MySQL），则可以省略服务名称：

```
C:\> mysql --remove
C:\> mysql --remove mysqlsvc2
```

## 12.11 更新 MySQL

由于 MySQL 正在积极开发中，更新会定期出现。这给管理员带来了这样一个问题：当出现新版本时，是否应该升级 MySQL 安装。以下准则应有助于你做出这一决定。
