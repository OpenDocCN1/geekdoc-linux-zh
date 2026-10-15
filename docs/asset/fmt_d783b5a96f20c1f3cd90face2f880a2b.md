
在另一个场景中，如图 21.5 所示，用户通过 SSH 登录到远程主机并在其上启动一个程序来访问数据库，但数据库实际上运行在

## Web Access to a Database

在本节中，我们来看两个基本的数据库服务器 Web 访问示例。在第一个示例中，用户通过位于 World Wide Web 上的表单访问数据库。乍一看，似乎客户端运行在用户的 workstation 上。当然，实际上并非如此；客户端实际上运行在 Web 服务器上。用户 workstation 上的 Web 浏览器只是为用户提供了一种输入他想要发送到数据库的数据的方式，以及一种将从数据库发送的结果显示给用户的方式。实际处理向数据库发送请求的软件以 CGI 脚本的形式运行在 Web 服务器上；Java servlet；或嵌入式脚本，如 PHP 或 Sun Microsystems, Inc. 的 JavaServer Pages (JSP)。

通常，在谈论数据库结构时，术语 client 和 front end 会被互换使用。然而，图 21.7 显示了一个访问形式的示例，其中客户端和前端根本不是同一回事。在此示例中，前端是用户 Web 浏览器中显示的表单。在这种情况下，客户端被称为 middleware。

![](img/7aaa8e4f2209bf9f2fb443905096e94c_535_0.png)

FIGURE 21.7 The user accesses the database through the World Wide Web. The front end is the user's web browser, the client is running on leopard, and the server is running on simba.

在另一种可能的 Web 访问场景中，可以说客户端是一个两部分组成的应用程序，其中一部分运行在用户的 workstation 上，另一部分运行在 Web 服务器上。例如，数据库程序员可以在 Web 表单中使用 JavaScript 来确保用户输入了有效的查询。在这种情况下，用户查询部分在她自己的 workstation 上处理，部分在 Web 服务器上处理。错误检查在用户自己的 workstation 上完成，这有助于减轻服务器负载，也有助于减少网络流量，因为查询在通过网络发送到服务器之前已进行了错误检查。

## The MySQL Command-Line Client

MySQL 命令行客户端是 `mysql`，其语法如下：

```
mysql [options] [database]
```

`mysql` 的一些可用选项在表 21.1 中讨论。`database` 是可选的，如果给出，应为要连接到的数据库的名称。

**TABLE 21.1 — Command-Line Options to Use When Invoking `mysql`**

| Option | Action |
|---|---|
| `-h hostname` | 连接到远程主机 `hostname`（如果数据库服务器不在本地系统上）。 |
| `-u username` | 以用户 `username` 的身份连接到数据库。 |
| `-p` | 提示输入密码。如果您以身份连接的用户需要密码才能访问数据库，则此选项是必需的。请注意，这是一个小写 `p`。 |
| `-P n` | 指定 `n` 为客户端应连接到的端口号。请注意，这是一个大写 `P`。 |
| `-?` | 显示帮助信息。 |

可用的选项比表 21.1 中列出的要多，但这些是最常用的选项。有关可用选项的更多信息，请参阅 `mysql` 的 man 手册。

> **CAUTION**
>
> 尽管 `mysql` 允许您在 `-p` 选项后在命令行上指定密码，从而避免在提示时输入密码，但您绝不应以这种方式调用客户端。这样做会导致您的密码显示在进程列表中，而进程列表可以被系统上的任何用户访问。这是严重的安全漏洞，因此您绝不应在 `mysql` 命令行上提供您的密码。

您可以在不指定要使用的数据库的情况下访问 MySQL 服务器。登录后，您使用 `help` 命令获取可用命令的列表，如下所示：

```
mysql> help

MySQL commands:
Note that all text commands must be first on line and end with ';'
help (\h) Display this help.
? (\?) Synonym for 'help'.
clear (\c) Clear command.
connect (\r) Reconnect to the server. Optional arguments are db and host.
edit (\e) Edit command with $EDITOR.
ego (\G) Send command to mysql server, display result vertically.
exit (\q) 退出 mysql。与 quit 相同。
go (\g) 将命令发送到 mysql 服务器。
nopager (\n) 禁用分页器，打印到 stdout。
notee (\t) 不写入 outfile。
pager (\P) 设置 PAGER [to_pager]。通过 PAGER 打印查询结果。
print (\p) 打印当前命令。
quit (\q) 退出 mysql。
rehash (\#) 重建补全哈希。
source (\.) 执行 SQL 脚本文件。需要提供文件名作为参数。
status (\s) 从服务器获取状态信息。
tee (\T) 设置 outfile [to_outfile]。将所有内容追加到指定 outfile。
use (\u) 使用另一个数据库。需要提供数据库名称作为参数。
```

然后你可以通过使用 `use` 命令和已创建的数据库名称（例如 `animals`）以及你有权连接的数据库来访问数据库，如下所示：

```
mysql> use animals
Database changed
mysql>
```

## The PostgreSQL Command-Line Client

你通过命令 `psql` 调用 PostgreSQL 命令行客户端。与 `mysql` 类似，`psql` 可以使用你想要连接的数据库名称进行调用。同样与 `mysql` 一样，`psql` 可以接受多个选项。这些选项列在表 21.2 中。

**TABLE 21.2 Command-Line Options to Use When Invoking `psql`**

| Option | Action |
|---|---|
| `-h hostname` | 连接到远程主机 `hostname`（如果数据库服务器不在本地系统上）。 |
| `-p n` | 指定 `n` 为客户端应连接到的端口号。请注意，这是一个小写的 `p`。 |
| `-U username` | 以用户 `username` 的身份连接到数据库。 |
| `-W` | 在连接到数据库后提示输入密码。在 PostgreSQL 7 及更高版本中，如果服务器在建立连接后请求密码，则密码提示是自动的。 |
| `-?` | 显示帮助信息。 |

除了表 21.2 中列出的选项外，还有更多选项可用。有关所有可用选项的详细信息，请参阅 `psql` 的 man 手册。

- [http://www.postgresql.org/idocs/index.php?tutorial-start.html](http://www.postgresql.org/idocs/index.php?tutorial-start.html)—这个交互式 HTML 文档树是开始学习如何使用 PostgreSQL 的绝佳起点。
- [http://www.pgsql.com](http://www.pgsql.com)—这是一家提供 PostgreSQL 数据库付费支持合同的商业公司。

# CHAPTER 22

## LDAP

### IN THIS CHAPTER

- ► Configuring the Server
- ► Configuring Clients
- ► Administration
- ► Reference

轻量级目录访问协议（LDAP，发音为 ell-dap）是那些技术之一，虽然隐藏，但构成了企业计算核心基础设施的一部分。它的工作很简单：存储有关用户的信息。然而，它的强大之处在于它可以链接到数十种其他服务。LDAP 可以为登录认证、公钥分发、电子邮件路由和地址验证提供支持，并且最近已成为推动单点登录技术发展的核心。

### TIP

大多数人发现将 LDAP 视为一种高度专业化的数据库服务器形式时更容易理解其概念。在幕后，Ubuntu 使用数据库来存储所有 LDAP 信息；然而，LDAP 并没有提供像 SQL 那样简单直接的数据操作方式！

OpenLDAP 使用 Sleepycat Software 的 Berkeley DB（BDB），并且强烈建议坚持使用该默认设置。话虽如此，如果你有特定需求，也有替代方案。
