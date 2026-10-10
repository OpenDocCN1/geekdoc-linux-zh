
## SetEnvIfNoCase

`SetEnvIfNoCase` 指令与 `SetEnvIf` 相同，除了它提供非区分大小写的正则表达式匹配。

- **语法：** `SetEnvIfNoCase attribute regex variable=value [...]`
- **上下文：** 服务器配置

## mod_unique_id

`mod_unique_id` 模块为每个请求提供一个魔术令牌，在非常特定的条件下保证该令牌在所有请求中是唯一的。该唯一标识符即使在正确配置的主机集群中的多台机器之间也是唯一的。每个请求的环境变量 `UNIQUE_ID` 被设置为该标识符。此模块没有指令。

## 认证和访问控制模块

Apache 有许多模块用于执行认证和授权任务。在大多数情况下，认证模块使用基本 HTTP 认证，它使用明文密码。授权模块允许您通过用户名或 IP 地址控制对您网站目录的访问。表 5-2 中显示的模块允许您执行认证和访问控制任务。

### 表 5-2 认证和访问控制模块

| **模块** | **用途** |
| --- | --- |
| `mod_auth` | 这是标准认证模块，实现了基本 HTTP 认证。详情见第 7 章。 |
| `mod_auth_anon` | 允许匿名用户访问认证区域。 |
| `mod_auth_dbm` | 提供使用 DBM 文件进行用户认证。 |
| `mod_auth_db` | 提供使用 Berkeley DB 文件进行用户认证。 |
| `mod_auth_digest` | 此模块使用消息摘要 5 (MD5) 实现 Digest 认证。 |
| `mod_access` | 此模块允许您通过主机名或 IP 地址授权访问。详情见第 7 章。 |

## mod_auth_anon

`mod_auth_anon` 模块允许匿名访问认证区域。如果您熟悉匿名 FTP 服务器，这与该设置非常相似。所有用户都可以使用名为 "anonymous" 的用户 ID 及其电子邮件地址作为密码来获得访问权限。输入的电子邮件地址存储在日志文件中，可用于执行用户跟踪或创建潜在客户邮件列表。

您必须使用源代码发行版中 `configure` 脚本的 `-enable-auth-anon` 选项启用此模块，并编译和安装 Apache。

## Anonymous

使用 `Anonymous` 指令，您可以指定一个或多个可用于访问该区域的用户名。将用户名 "anonymous" 保留在您选择的列表中是个好主意，因为它与匿名访问密切相关。如果您选择的用户名中包含空格字符，请确保用户名用引号括起来。

- **语法：** `Anonymous user user ...`
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

例如，下面的指令允许用户输入 Unregistered User 或 anonymous 作为用户名进入匿名区域。

```
Anonymous "Unregistered User" anonymous
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_140_0.png)

> 用户名字符串不区分大小写。

## Anonymous_Authoritative

当设置为 `On` 时，匿名认证成为目录的权威认证方案。换句话说，如果您对目录有多个认证要求并且也设置了此指令，则其他方法将被忽略。

- **语法：** `Anonymous_Authoritative On | Off`
- **默认设置：** `Anonymous_Authoritative Off`
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

## Anonymous_LogEmail

当 `Anonymous_LogEmail` 指令设置为 `On` 时，在浏览器弹出认证窗口的密码字段中输入的任何内容都会记录在 Apache 访问日志文件中。

- **语法：** `Anonymous_LogEmail On | Off`
- **默认设置：** `Anonymous_LogEmail On`
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

## Anonymous_MustGiveEmail

当设置为 `On` 时，`Anonymous_MustGiveEmail` 指令使模块拒绝未提供电子邮件地址格式密码的访问请求。

- **语法：** `Anonymous_MustGiveEmail On | Off`
- **默认设置：** `Anonymous_MustGiveEmail On`
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

![](img/e11fcbd2818a3495ac70085e5d8d1c26_141_0.png)

当此指令设置为 `On` 时，您不应该信任人们输入的电子邮件地址，因为没有办法检查是谁输入了谁的电子邮件地址。

## Anonymous_NoUserID

如果您希望用户将弹出窗口中的用户名字段留空，请将 `Anonymous_NoUserID` 指令设置为 `On`；否则，需要与 `Anonymous` 指令中提供的值匹配的用户名。

- **语法：** `Anonymous_NoUserID On | Off`
- **默认设置：** `Anonymous_NoUserID Off`
- **上下文：** 目录，每目录访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

## Anonymous_VerifyEmail

当 `Anonymous_VerifyEmail` 指令设置为 `On` 时，它要求密码是一个有效的电子邮件地址。然而，有效性检查是有限的。模块仅检查密码字段中的 `@` 符号和点 `.`。如果输入的密码包含这两个符号，则接受。

- **语法：** `Anonymous_VerifyEmail On | Off`
- **默认设置：** `Anonymous_VerifyEmail Off`

### 上下文：目录，按目录的访问控制文件（`.htaccess`）

#### 覆盖：AuthConfig

以下配置展示了如何使用前文所述的指令为目录提供匿名访问权限。

```
Anonymous_NoUserId off

Anonymous_MustGiveEmail on

Anonymous_VerifyEmail on

Anonymous_LogEmail on

Anonymous_anonymous guest "I do not know"

AuthName Use 'anonymous' & Email address for guest entry

AuthType basic

require valid-user
```

## mod_auth_dbm

基于文本文件的认证（使用 `mod_auth`）在处理速度上效率较低，当大量用户（超过 2000 人）需要认证访问受限的 Web 部分时，可能会负面影响 Web 服务器的性能。在这种情况下，`mod_auth_dbm` 模块是更好的选择。`mod_auth_dbm` 模块使用 DBM 文件而不是文本文件来存储数据。DBM 文件是一种特殊类型的数据文件，允许对存储的数据进行更快的随机访问。

> **注意** 实际上，如果你拥有大量用户，请考虑在第 7 章中讨论的基于 `mod_auth_mysql` 或 `Apache::AuthDBI` 的认证。只有在无法使用数据库时，才建议使用基于 DBM 的认证。

DBM 文件以键=值对的形式存储数据记录，并为文件中的键保持一个计算过的索引表。通过使用 DBM 文件中的索引表，检索与键关联的记录的速度比解析拥有数万条记录的大文本文件所需的时间更快。有许多 DBM 可用，最常见的包括 GDBM、NDBM、SDBM 和 Berkeley DB (BSD-DB)。表 5-3 列出了这些 DBM 的功能列表。

**表 5-3**
**DBM 功能**

| 功能 | NDBM | SDBM | GDBM | BSD-DB |
| :--- | :--- | :--- | :--- | :--- |
| 许可限制 | 未知 | 无 | 有 | 无 |
| 字节序无关 | 否 | 否 | 否 | 是 |
| 默认大小限制 | 4K | 1K | 无 | 无 |
| 创建 FTP 安全文件 | 否 | 是 | 是 | 是 |
| 速度 | 未知 | 慢 | 中 | 快 |
| 数据库大小 | 未知 | 小 | 大 | 中 |
| 代码大小 | 未知 | 小 | 大 | 大 |
| 源码包含在 Perl 中 | 否 | 是 | 否 | 否 |

此表格基于 Perl 5 文档中的信息。在使用任何 DBM 与 Apache 之前，请执行以下操作，以确保你选择的 DBM 已安装在你的系统中。通过确认 DBM 库文件位于你系统的默认库目录中来完成此操作。你需要带有 DBM 支持的 Perl。确保你拥有编译了所选 DBM 支持的最新版本 Perl。

> 你可以从 `www.perl.com` 下载 Perl。为 DBM 支持配置 Perl 非常容易。只需运行配置脚本，它会提示你关于 DBM 支持的信息。例如，如果你选择 `NDBM` 或 `GDBM` 作为你所需的 DBM，并且如果你的系统中安装了它们，Perl 配置脚本会询问你是否希望使用 `-ln dbm`、`-lgdbm` 和库标志来编译 Perl。

在你已在系统中安装了适当的 DBM 库之后，你需要配置 Apache 以支持 DBM 文件，因为标准的 Apache 发行版并未启用 DBM 支持。使用 `configure` 脚本配合 `--enable-auth-dbm` 选项配置 Apache 源代码，并按照常规编译和安装 Apache。

> 如果你在编译 Apache 时遇到困难，请尝试在 `configuration` 文件中的 `EXTRA_LIBS` 中添加 `-lyour_dbmaname`。例如，如果你正在使用 GDBM，你可以添加 `-lgdbm` 使 `EXTRA_LIBS=-lgdbm`。确保你重新运行 `configure` 脚本并在之后再次运行 `make`。如果有问题，最好尝试 GNU GDBM，因为它被许多不同的系统大量使用，并且你很可能在 USENET 新闻组中获得帮助。

在 Apache 正确编译以支持 DBM 文件后，你可以使用 `dbmmanage` 创建 DBM 用户文件。首先使用标准 Apache 发行版（或源代码发行版）支持目录中找到的 `dbmmanage` Perl 脚本，用于创建基于 DBM 的用户文件。`dbmmanage` Perl 脚本可以创建许多流行的 DBM 文件，如 NDBM、GDBM 和 Berkeley DB 文件。此脚本可用于创建新的 DBM 文件、添加用户和密码、更改密码、删除用户或查看用户信息。在使用脚本之前，你应该修改脚本中的以下行，以便你想使用的 DBM 列为 ISA 数组中的第一项：

```
BEGIN { @AnyDBM_File::ISA = qw(DB_File, NDBM_File, GDBM_File) }
```

例如，如果你计划使用 GDBM 文件，将该行更改为：

```
BEGIN ( $AnyDBM_File::ISA = qw( GDBM_File , DB_File, NDBM_File) )
```

要查看脚本提供的选项，请如下运行它：

```
./dbmanage
```

这会显示一条包含所有可能选项的语法行。要创建一个名为 `/www/secrets/myuserdbm` 的新 DBM 文件，并添加一个名为 `reader` 的用户，请输入以下命令：

```
./dbmanage /www/secrets/myuserdbm adduser reader
```

脚本将要求你输入（并重新输入）用户 `reader` 的密码。完成后，它将把用户名和加密后的密码添加到 `myuserdbm` DBM 文件中。不要使用 `add` 选项来添加用户，因为它不会加密密码。要查看 DBM 文件中所有用户的列表，请使用以下脚本：

```
./dbmanage /path/to/your/dbmfile view
```

在重新编译支持 DBM 的 Apache 后，你可以使用 `mod_auth_dbm` 模块来提供基于 DBM 的 Basic HTTP 认证。请注意，对于 Berkeley DB，你必须使用 `mod_auth_db` 而不是 `mod_auth_dbm`。

`mod_auth_dbm` 模块提供了指令 `AuthDBMUserFile`、`AuthDBMGroupFile` 和 `AuthDBMAuthoritative`。让我们来看看这些指令以及使用 `mod_auth_dbm` 模块的一些示例。

### AuthDBMUserFile

`AuthDBMUserFile` 指令设置用于 DBM 认证的用户文件的完全限定路径名。该文件每条记录包含一个键值对，其中用户名是键，而经过 `crypt()` 加密的密码是值。请注意，记录中的每个字段由冒号分隔，并且可以在初始的用户名和密码字段之后追加任意数据。

- **语法：** `AuthDBMUserFile filename`
- **上下文：** 目录，按目录的访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

![](img/e11fcbd2818a3495ac70085e5d8d1c26_144_0.png)

> 切勿将用户数据库文件存储在你的 Web 文档树中，因为某人可能会下载整个用户数据库并滥用它。

### AuthDBMGroupFile

`AuthDBMGroupFile` 指令设置包含用户组列表的组文件的完全限定路径名。文件中的每条记录都是一个键值对，其中键是用户名，值是该用户所属的组名的逗号分隔列表。

- **语法：** `AuthDBMGroupFile filename`
- **上下文：** 目录，按目录的访问控制文件 (`.htaccess`)
- **覆盖：** `AuthConfig`

如果你不想使用单独的组文件，可以使用单个 DBM 文件来提供密码和组信息。该文件的格式如下：

```
DBM_Record_Key(username) - encrypted_password; comma_separated_group_list
```
