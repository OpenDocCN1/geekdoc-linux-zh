
| :--- | :--- |

| -h hostname | 连接到远程主机 `hostname`（如果数据库服务器不位于本地系统上）。 |

| -u username | 以用户 `username` 的身份连接到数据库。 |

| -p | 提示输入密码。如果您要连接的用户需要密码才能访问数据库，则此选项是必需的。注意，这是一个小写 p。 |

| -P n | 指定 `n` 作为客户端应连接的端口号。注意，这是一个大写 P。 |

| -? | 显示帮助信息。 |

除了表 18.1 中列出的选项外，还有更多可用选项，但这些是最常用的选项。有关可用选项的更多信息，请参阅 `mysql` 的 man 页。

> **注意**
>
> 虽然 `mysql` 允许您在 `-p` 选项后的命令行上指定密码，从而避免在提示符下输入密码，但您绝不应以此方式调用客户端。这样做会导致您的密码显示在进程列表中，而进程列表可以被系统上的任何用户访问。这是一个重大的安全漏洞，因此您永远不要在 `mysql` 命令行上提供您的密码。

您可以访问 MySQL 服务器而不指定要使用的数据库。登录之后，您可以使用 `help` 命令获取可用命令列表，如下所示：

```
mysql> help

MySQL commands:
Note that all text commands must be first on line and end with `;`:
help (\h) Display this help.
? (\?) Synonym for 'help'.
clear (\c) Clear command.
connect (\r) Reconnect to the server. Optional arguments are db and host.
edit (\e) Edit command with $EDITOR.
ego (\G) Send command to mysql server, display result vertically.
exit (\q) Exit mysql. Same as quit.
go (\g) Send command to mysql server.
nopager (\n) Disable pager, print to stdout.
note (\T) Don't write into outfile.
pager (\P) Set PAGER [to_pager]. Print the query results via PAGER.
print (\p) Print current command.
quit (\q) Quit mysql.
rehash (\#) Rebuild completion hash.
source (\.\s) Execute a SQL script file. Takes a file name as an argument.
status (\s) Get status information from the server.
tee (\T) Set outfile [to_outfile]. Append everything into given outfile.
use (\u) Use another database. Takes database name as argument.
```

然后，您可以使用 `use` 命令和一个已创建的数据库名称（例如 animals）来访问该数据库，并且您被授权连接该数据库，如下所示：

```
mysql> use animals
Database changed
mysql>
```

### PostgreSQL 命令行客户端

您使用 `psql` 命令调用 PostgreSQL 命令行客户端。与 `mysql` 类似，`psql` 可以用您想要连接的数据库名称来调用。与 `mysql` 类似，`psql` 可以接受多个选项。这些选项列在表 18.2 中。

**表 18.2 调用 psql 时使用的命令行选项**

| 选项 | 操作 |

| :--- | :--- |

| -h *hostname* | 连接到远程主机 *hostname*（如果数据库服务器不位于本地系统上）。 |

| -p *n* | 指定 *n* 作为客户端应连接的端口号。注意，这是一个小写 p。 |

| -U *username* | 以用户 *username* 的身份连接到数据库。 |

| -W | 在连接到数据库后提示输入密码。在 PostgreSQL 7 或更高版本中，如果服务器在连接建立后请求密码，则密码提示是自动的。 |

| -? | 显示帮助信息。 |

除了表 18.2 中列出的选项外，还有更多可用选项。有关所有可用选项的详细信息，请参阅 `psql` 的 man 页。

## 图形客户端

如果您更喜欢使用图形数据库客户端而不是上一节中讨论的命令行客户端来与数据库交互，那么您走运了：有一些可用的选项。

MySQL 有一个官方的图形客户端，称为 MySQLGUI。MySQLGUI 可以从 MySQL 网站 http://www.mysql.com/ 以源码和二进制格式获取。

MySQL 和 PostgreSQL 也有基于 Web 的管理界面。phpMyAdmin 和 phpPgAdmin 是两个此类产品。这两个产品都基于 PHP 嵌入式脚本语言，因此您需要安装 PHP。当然，您还需要安装 Web 服务器。

### 相关的 Fedora 和数据库命令

以下命令对于在 Fedora 中创建和操作数据库非常有用：

- `createdb` — 创建一个新的 PostgreSQL 数据库

- `createuser` — 创建一个新的 PostgreSQL 用户账户

- `dropdb` — 删除一个 PostgreSQL 数据库

- `dropuser` — 删除一个 PostgreSQL 用户账户

- `mysql` — 交互式查询 `mysqld` 服务器

- `mysqladmin` — 管理 `mysqld` 服务器

## 参考资料

- `mysqldump`——转储或备份 MySQL 数据或表

- `pgaccess`——访问 PostgreSQL 数据库服务器

- `pg_ctl`——控制 PostgreSQL 服务器或查询其状态

- `psql`——通过交互式终端访问 PostgreSQL

- `http://www.mysql.com/`——这是 MySQL 数据库服务器的官方网站。你可以在这里找到最新版本以及 MySQL 的最新信息和在线文档。你还可以在此购买支持合同。如果你打算在企业环境中使用 MySQL，这可能值得关注。（许多企业对使用没有支持合同保障的软件持犹豫态度。）

- `http://www.postgresql.org/`——这是 PostgreSQL 数据库服务器的官方网站。到达此网站时，系统会要求你选择一个镜像站点。选择镜像站点后，你会被重定向到主网站。在那里，你可以找到 PostgreSQL 最新版本的信息并阅读在线文档。

- `http://www.postgresql.org/docs/8.1/interactive/tutorial-start.html`——这个交互式 HTML 文档树是开始学习使用 PostgreSQL 的好地方。

- `http://www.psql.com/`——这是一家为 PostgreSQL 数据库提供付费支持合同服务的商业公司。

## 第 19 章

# 文件和打印

在计算发展的早期，由于缺乏良好的网络标准和互操作性，文件和打印机共享几乎是不可行的。如果你想使用连接到另一台计算机的打印机，你必须将文件保存到软盘上，然后走过去使用它。

如今，在一个一个人拥有多台计算机变得司空见惯的世界里，文件共享和打印机共享已经成为第二天性。无论是在不同计算机之间共享照片，还是为协作提供中央存储库，文件共享都是我们信息时代的重要组成部分。与此同时，共享打印机的需求也随之产生；毕竟，没有人希望为了打印一封简短的信函而不得不反复将计算机连接到打印机又断开。

无论你需要在网络上共享文件和打印机的原因是什么，你都会在本章中学习如何实现这两点。本章介绍了如何使用流行的 UNIX 网络文件系统（NFS）协议共享文件，以及更友好的 Windows Samba 系统。你还将了解如何配置具有 JetDirect 等接口的网络附加打印机。本章涵盖了图形界面和命令行工具，因此你应该能找到适合你工作方式的工具。

### 使用网络文件系统

NFS 是由 Sun Microsystems 开发的一种协议，它允许计算机将远程文件系统当作本地机器的一部分来使用。NFS 的一个常见用途是让用户的主目录出现在他们使用的每一台本地机器上，从而消除对物理主目录的需求。这使得“热插工位”和其他灵活的工作安排成为可能，尤其因为无论用户在哪里，他的主目录都会跟随他。

NFS 的另一个流行用途是在类似计算机之间共享二进制文件。如果你有一个新版本的软件包希望所有机器都拥有，你只需在 NFS 服务器上进行升级，所有运行相同版本 Fedora 的主机都将拥有相同的升级后软件包。

## 本章内容

- 使用网络文件系统
