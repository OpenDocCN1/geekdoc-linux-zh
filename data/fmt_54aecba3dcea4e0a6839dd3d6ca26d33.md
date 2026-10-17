
表 9-2 默认 MS SQL Server 变量

# 第 8 章：攻击 Web 数据存储

简短、直击要点的过程可以返回有用信息。表 9-3 包含了常用于枚举用户、表和自定义存储过程的存储过程列表。这些存储过程最大的优势是它们可以在不引用 Master 数据库的情况下调用。

| 存储过程 | 枚举用户 | 枚举对象 | 描述 |
| --- | --- | --- | --- |
| `sp_columns <<table>>` | | | 最重要的是，返回表的列名。 |
| `sp_configure [name]` | | | 内部数据库设置。指定特定设置以检索该值——例如 `sp_configure 'remote query timeout()' `。 |
| `sp_dboption` | | | 查看（或设置）用户可配置的数据库选项。 |
| `sp_depends <object>` | | X | 列出与存储过程相关的表。 |
| `sp_helptext <object>` | | X | 描述对象。这对于识别可以执行存储过程的区域更有用。它很少执行成功。 |
| `sp_helpextendedproc` | | X | 列出所有扩展存储过程。 |
| `sp_used [object]` | | X | 不带参数时，返回数据库名、大小和未分配空间。如果指定了对象，它将相应地描述行和其他信息。 |
| `sp_who2 [username]` (以及 `sp_who`) | X | | 远优于它的数值表兄弟。它显示用户名、连接它们的主机、用于连接数据库的应用程序、在数据库中执行的当前命令以及其他几条信息。这两个过程都接受一个可选的用户名。这是枚举 SQL 数据库用户（而非应用程序用户）的极佳方法。 |

表 9-3 用于枚举数据库的存储过程

# 黑客攻防 Web 应用程序

## 扩展存储过程

以 `xp_` 前缀签名的扩展存储过程提供了完全在 SQL 舒适环境中强大的系统管理功能。我们将在本章末尾介绍防御措施，但我们提示其中一种防御措施涉及完全删除这些命令。表 9-4 列出了一些不需要参数的过程。表 9-5 包含了需要参数的过程列表。

这些命令涵盖了系统级访问的几乎任何方面。此外，在您尝试使用 `xp_regread` 获取 SAM 文件之前，您应该知道该技术仅适用于未启用 Syskey 的系统。Windows 2000 默认启用此功能。

## 默认本地表（实用的）

也被称为系统表对象，这些表包含有关数据库和操作系统的信息。表 9-6 列出了具有最用信息的表。

从这些表检索信息的的最简单方法是使用 `SELECT *` 示例：

```
SELECT * FROM sysfiles
```

然而，如果你熟悉数据库，那么你可以解析请求以获取特定字段——例如，查看所有存储过程：

```
SELECT name FROM sysobjects WHERE type = 'P'
```

## 默认 Master 表（实用的）

表 9-7 列出了从 Master 数据库中选定的表。这些表提供了有关操作系统和数据库配置的详细信息。从这些表进行 `SELECT` 通常需要 `master..` 标识：

```
SELECT * FROM master..sysdevices
```

| 扩展存储过程 | 描述 |
|---|---|
| `xp_loginconfig` | 显示登录信息，特别是登录模式（混合等）和默认登录。 |
| `xp_logininfo` | 显示当前登录的账户。仅适用于 NTLM 账户。 |
| `xp_msver` | 列出 SQL 版本和平台信息。 |
| `xp_enumdn` | 枚举 ODBC 数据源。 |
| `xp_enumgroups` | 枚举 Windows 组。 |
| `xp_ntsec_enumdomains` | 枚举网络上存在的域。 |

表 9-4 不需要参数的扩展过程

| 扩展存储过程 | 描述 |
|---|---|
| `xp_cmdshell <command>` | 等同于 `cmd.exe`——换句话说，对数据库服务器的完全命令行访问。假设存在 `cmd.exe`，因此你只需要输入 `'dir'` 来获取目录列表。默认当前目录是 `%SYSTEMROOT%\System32`。从配置单元程序中读取注册表。 |
| `xp_regread <rootkey>, <key>, <value>` | 还有其他与注册表相关的过程。读取值是最用的。 |
| `xp_servicecontrol <action>, <service>` | 启动或停止 Windows 服务。 |
| `xp_terminate_process <PID>` | 根据进程 ID 杀死进程。 |

表 9-5 参数化存储过程

| 系统表对象 | 描述 |
|---|---|
| `syscolumns` | 当前数据库的所有列名和存储过程，而不仅仅是 master。 |
| `syssobjects` | 数据库中的每个对象（以存储过程的形式）。 |
| `sysusers` | 可以操作数据库的所有用户。 |
| `sysfiles` | 当前数据库及其日志文件的文件名和路径。 |
| `systypes` | SQL 定义的数据类型或用户定义的新类型。 |

表 9-6 系统表对象

| Master 数据库表 | 描述 |
|--- | --- |
| `sysconfigs` | 当前配置设置。 |
| `sysdevices` | 用于数据库、日志和临时文件的设备。 |
| `syslogins` | 每个允许访问数据库的用户信息。 |
| `sysremotelogins` | 每个允许远程访问数据库或其存储过程的用户信息。 |
| `sysversers` | 列出服务器作为 OLE 数据库服务器可以访问的所有节点。 |

表 9-7 Master 数据库表

# 通用 SQL 技术

上一节对 Microsoft SQL Server 的关注不应阻止你对其他数据库尝试 SQL 注入技术。MS SQL Server 仅仅内置了极其的功能，使得 SQL 注入更具破坏性。许多技术适用于基于 SQL 的数据库。

SQL 运算符有一组预定义的关键字，这些留具有特殊含义。当你从表中选择数据时，使用 `SELECT` 语句。应用程序从 `SELECT`、`FROM` 和 `WHERE` 中受益——这些构成了基础查询。

> TIP 这些代表了数据操作技术。它们的注入方式从单引号、双连字符到多个单引号和括号不等。

# 第8 章：攻击 Web 数据存储库

## OR 1=1

这个显而易见的陈述创建了一个真值条件。这在检查用户名和密码的身份验证查询中非常有用：

```sql
sqlAuth = "SELECT userid FROM logins WHERE name='" & Username & "' AND password='" & Password & ""
```

如果用户用用户名 `"Wayne"` 和密码 `"Pirate"` 登录，查询将如下：

```sql
SELECT userid FROM logins WHERE name='Wayne' AND password='Pirate'
```

因此，除非 `"Pirate"` 与数据库中的记录匹配，否则 Wayne 无法登录。然而，

```sql
SELECT userid FROM logins WHERE name='Wayne' AND password='Pirate' OR 1=1
```

## UNION

`UNION` 语句组合了 `SELECT` 语句。它用于从表中检索所有行。基本语法是：

```sql
UNION ALL SELECT FROM TABLE WHERE condition
```

你可以根据应用程序中的变量名、`.inc` 文件或 SQL 错误轻松推断出字段和表名。条件通常始终为真，例如 `1=1` 或 `"="`（空都不等于空）。

## INSERT

`INSERT` 指令仅仅是向表中插入值。这看起来可能没什么用；毕竟，我们想知道数据库里有什么。它对于绕过身份验证非常有用。如果我们使用 SQL 注入向 `users` 表插入一个名为 `"neo"` 密码为 `"trinity"` 的用户：

```sql
INSERT INTO VALUES('neo', 'trinity')
```

### 数据库身份验证凭据

Web 服务器需要用户名和密码来连接数据库。服务器会自动建立此连接。因此，应用程序会将身份验证凭据存储在页面内部。不幸的是，大多数应用程序将这些连接字符串存储在文档根目录的文件中——Web浏览器可以访问。

有时开发者依赖服务器来保护敏感文件，例如 IIS 禁止请求 `global.asa` 文件。然而，如果应用程序存在文件泄露漏洞（这在 Web 应用程序中很常见），用户名和密码可能会暴露。其他时候，开发者会将他们不希望用户发现或查看的连接字符串放在某些文件中，如 `xmlserver.js`、`database.inc` 或 `server.js`。

SQL Server 连接字符串很容易发现，特别是当它有一个空密码时：

```sql
```
