
配置时注意这一点非常重要，因为 `prefix=/usr/local/mysql` 是数据库安装的目录，可以更改以将数据库位于我们希望的任何目录。

## 2.2. 安装后验证

一旦安装（无论是通过二进制文件还是源代码），我们必须验证服务器是否正常工作。在 Debian 中可以直接完成这一点：

| `/etc/init.d/mysql start` | 启动服务器 |
| `mysqladmin version` | 生成版本信息 |
| `mysqladmin variables` | 显示变量的值 |
| `mysqladmin -u root shutdown` | 关闭服务器 |
| `mysqlshow` | 将显示预定义的数据库 |
| `mysqlshow mysql` | 将显示 MySQL 数据库的表 |

如果是从源代码安装的，在进行这些检查之前，我们必须执行以下命令来创建数据库（从发行版目录）：

```
./scripts/mysql_install_db
cd InstallationDirectoryMys
.bin/mysqld_safe --user mysql &
```

如果我们安装的是二进制文件（RPM, Pkg,...），我们将执行以下操作：

```
cd InstallationDirectoryMys
./scripts/mysql_install_db
./bin/mysqld_safe user = mysql &
```

`install_db_script` 脚本创建 mysql 数据库，`mysqld_safe` 启动 mysql 服务器。接下来，我们可以检查上述所有适用于 Debian 命令，第一个是启动服务器的。此外，如果安装了测试程序，可以使用 `run-all-tests` 目录下的 `sql-bench` 运行。结果将出现在 `sql-bench/results` 目录，以便与其他数据库进行比较。

## 2.3. MySQL 监控程序（客户端）

MySQL 客户端可以创建和使用简单的数据库，它是交互式的，可以连接到服务器、运行查询并可视化结果。它也可以在批处理模式（作为脚本）下工作，通过文件将命令传递给它。要查看所有命令选项，可以运行 `mysql --help`。我们将能够使用 `mysql` 命令建立连接（本地或远程），例如通过同一台机器的 Web 界面进行连接：

```
mysql -h localhost -u mysql -p DBName
```

如果我们不输入最后一个参数，则不选择数据库。

进入后，`mysql` 将显示提示符（`mysql>`）并等待我们输入命令（或 SQL 语句），例如。接下来，我们将顺序给出一系列命令来测试服务器（记住始终输入 `;` 来结束命令）：

```
mysql> SELECT VERSION(), CURRENT_DATE;
```

我们可以使用大写字母或小写字母。

```
mysql> SELECT SIN(PI/4), (4+1);
```

```
mysql> SELECT SIN(PI/4), (4+1)
-> VERSION();
```

```行输入。

```
mysql> SELECT CURRENT_DATE;
```

或者多行输入。

```
mysql> SHOW DATABASES;
```

| 注意 |
| MySQL 客户端 (root) |
| 网站 |
| 更多信息请参阅[文档](https://dev.mysql.com/doc/mysql/8.0/en/) |
| 选择数据库 |

```
mysql> USE test;
```

创建一个名为 test 的数据库。

```
mysql> CREATE TABLE pet (
```

在 MySQL 内部创建一个表。

```
mysql> SHOW TABLES;
```

显示表。

```
mysql> DESCRIBE pet;
```

显示表结构。

```
mysql> LOAD DATA INFILE "pet.txt" INTO TABLE pet;
```

从 pet.txt 加载数据。pet.txt 文件必须每行一个记录（格式为 YYYY-MM-DD）。

```
mysql> INSERT INTO pet
```

# `mysqlhotcopy DBName /DestinationDirectory`

同样，我们可以在服务器停止状态下复制 `*.frm`、`*.MYD` 和 `*.MYI` 文件。要进行恢复，执行：

```
REPAIR TABLE myisamchk -r
```

这在 99% 的情况下有效。否则，我们可以复制保存的文件并启动服务器。取决于我们想要恢复的内容，还有其他替代方法，并可能保存/恢复部分数据库（参见文档的第 4.4 节）。[Mys]

## 2.5. 图形界面

MySQL 有许多图形界面，其中我们应该提到 MySQL Administrator（可以从 http://www.mysql.com/products/tools/administrator/ 获取）。此外，作为工具我们还可以 MySQL-Navigator (http://sourceforge.net/projects/mysqlnavigator/)，或者带有 MySQL 工作模块的 Webmin（webmin-mysql 软件包），尽管后者不再包含在某些发行版中。与 PostgreSQL 类似，Webmin 也允许进行 MySQL 操作（我们需要安装 webmin-mysql，它会警告主用户将是操作系统的 root）。要建立连接，我们可以在例如 https://localhost:10000 的 URL 上输入相同的密码，导航器会请求接受（或拒绝）使用 SSL 连接证书，然后它将显示所有可以管理的的服务，其中包含 MySQL 服务器。

MySQL Administrator 是一个用于 MySQL 管理和控制数据库的强大应用程序。该应用程序以简单的方式在同一个环境中将数据库管理、控制和维护集成在一起。它的主要特点是：大型数据库的高级管理、通过“视觉化管理”减少错误、提高生产力以及安全的环境。底图显示了 MySQL Administrator 的视图（可以在 http://dev.mysql.com/doc/administrator/en/index.html 找到关于安装和启动它的所有文档）。

## 23 数据管理

- 文件 编辑 帮助
- 服务器信息
- 通用状态
- 某些操作
- 用户
- 健康状况
- 备份/恢复
- 复制状态
- 统计数据
- 用户账户
- users
- 事件
- 审计
- name
- localhost
- 127.0.0.1
- all

| 用户信息 | 全局权限 | 表格/列权限 | 资源 |
| --- | --- | --- | --- |
| Jack, Black Folat | 此用户有权连接到 MySQL 服务器 | | |

登录信息

MySQL 用户: Jack

密码: 填写您分配的密码

确认密码: 再次输入，确保密码已确认

| 附加信息 | | |
| --- | --- | --- |
| 描述: 具有 root 权限的管理员 | 用户的额外描述 |
| 邮箱: jack@example.com | 此用户的账户描述 |
| 联系信息: | 可选描述 |

![](img/7eff7e7ab4e6603f02d06e026ff29408_382_0.png)

图 2. MySQL Administrator

## 3. 源代码管理系统

并发版本系统 (CVS) 是一种版本控制系统，允许维护旧版本的文件（通常是源代码），并保存谁在何时以及为了什么做了什么更改的日志。与其他系统不同，CVS 并不是针对每次文件/目录工作，而是对它控制的目录分级组进行操作。

CVS 的目的是帮助管理软件版本，并控制多个作者对源文件的并发编辑。CVS 内部使用另一个名为 RCS（修订控制系统）的工具作为底层。虽然 RCS 可以独立使用，但不建议这样做，因为它除了其功能外，还具备 RCS 的所有能力，但在稳定性、功能和维护方面有显著改进。其中我们重点强调的是：去中心化操作（每个用户都可以拥有自己的代码树）、并发编辑、通过 shell 脚本实现自适应行为。[Ced, Vasa, Kiev]

正如引言中所解释的那样，Subversion (http://subversion.org/) 是一种专门设计用于取代 CVS 并扩展其能力的版本控制软件。它是 Apache/BSD 类型许可协议下的免费软件，在命令行中的名称也简称为 `svn`。Subversion 的一个重要特性是，与 CVS 不同，版本化文件没有独立的修订号，而是整个仓库有一个单一的版本号，该版本号标识了在“版本化”时仓库中所有文件的共同状态。我们提到的主要功能包括：

- 可以通过备份和重命名跟踪文件和目录的历史。
- 原子化且安全的修改（包括对多个版本的更改）。
- 高效且简单地创建分支
- 分支中仅发送差异（在 CVS 中，完整文件始终发送到服务器）。
