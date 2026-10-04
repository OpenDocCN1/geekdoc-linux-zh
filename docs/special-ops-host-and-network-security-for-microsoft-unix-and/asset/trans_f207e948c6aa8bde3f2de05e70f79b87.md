

# Microsoft SQL Server 攻击与防御 • 第 12 章

```
USE msdb
REVOKE update on mswetasks to public
REVOKE insert on mswetasks to public
GO
```

- 10. 收紧数据转换服务 (DTS) 程序包连接的权限，防止恶意用户影响 DTS 程序包。

USE msdb
REVOKE select on RTblDBMProps to public
REVOKE update on RTblDBMProps to public
REVOKE insert on RTblDBMProps to public
REVOKE delete on RTblDBMProps to public
GO

- 11. 收紧需要频繁使用但不应允许公开访问的扩展存储过程权限。

USE master
REVOKE execute on sp_runwebtask to public
REVOKE execute on sp_readwebtask to public
REVOKE execute on sp_MSServerProperties to public
REVOKE execute on sp_MScopyscriptfile to public
REVOKE execute on sp_MSsetalertinfo to public
REVOKE execute on xp_xpread to public
REVOKE execute on xp_instance_regard to public
GO

- 12. 取消对 MSDB 的访客访问，以防止非系统管理员在没有显式权限的情况下访问数据库。

USE msdb
EXECUTE sp_revokedbaccess guest
GO

- 13. 关闭远程访问，防止其他 SQL Server 通过 RPC 连接到此服务器。

EXECUTE sp_configure 'remote access', '0'
GO
RECONFIGURE WITH OVERRIDE
GO

- 14. 验证允许访问系统表的能力已禁用。

```
EXECUTE sp_configure 'allow updates', '0'
GO
RECONFIGURE WITH OVERRIDE
GO
```

- 15. 增加 SQL Server 日志历史阈值，以便保留日志日志。

```
EXECUTE master.dbo.xp_regwrite N'HKEY_LOCAL_MACHINE',
'Software\Microsoft\MSSQLServer\MSSQLServer',
'NumErrorLogs',N'REG_DWORD',365
```

- 16. 移除文件系统中可能残留的任何文件（sqldir\setup.iss - winnt\setup.iss - \ winnt\sqstp.log）。这些命令可能需要根据操作系统和 SQL Server 安装路径进行微调。

```
EXECUTE master.dbo.xp_cmdshell 'del c:\windows\setup.iss'
GO
EXECUTE master.dbo.xp_cmdshell 'del c:\windows\sqstp.log'
GO
EXECUTE master.dbo.xp_cmdshell 'del c:\program files\microsoft sql server\mssql\install\setup.iss'
GO
```

- 17. 移除任何未使用的网络库。这是一个加固后的服务器，在确定外部连接需求之前，可以移除所有网络库。仍然可以使用共享内存（Shared Memory）网络库连接到本地服务器，通过指定 (local) 或句号 () 作为服务器名称即可始终生效。可以使用 SQL 网络实用程序轻松恢复其他网络库。（必须停止并重启 SQL Server 才能生效。）

```
EXECUTE master.dbo.xp_regwrite N'HKEY_LOCAL_MACHINE',N'SOFTWARE\nMicrosoft\MSSQLServer\MSSQLServer\SuperSocketNetLib',
'ProtocolList',N'REG_SZ',','
GO
```

- 18. 删危险的扩展存储过程。以后可以通过系统管理员使用 `sp_addextendedproc` 来恢复它们。此步骤是可选的，仅用于防止在执行前未尝试添加此类功能的非驻留病毒。虽然可能还有许多可以删除的扩展存储过程，但我们在这里删除的被认为是高度危险的。其他的应根据您的决定删除，因为删除它们可能会影响 Enterprise Manager 等应用程序正常运行。

```
USE MASTER
EXECUTE sp_droxtendedproc 'xp_cmdshell'
EXECUTE sp_droxtendedproc 'sp_OACreate'
EXECUTE sp_droxtendedproc 'sp_OADestroy'
EXECUTE sp_droxtendedproc 'sp_OAGetErrorInfo'
EXECUTE sp_droxtendedproc 'sp_OAGetProperty'
EXECUTE sp_droxtendedproc 'sp_OAMethod'
EXECUTE sp_droxtendedproc 'sp_OASetProperty'
EXECUTE sp_droxtendedproc 'sp_OAStop'
```

- 19. 创建一个低权限本地账户，并使用 Enterprise Manager 将其分配给 SQL Server 和 SQL Agent 服务。这是清单中唯一无法脚本化的项目，因为要求通过 EM 更改账户。这是为了确保为账户分配了正确的权限。可能可以通过脚本实现，但这会大大增加过程的复杂性，且充其量是权宜，因此假设此步骤是手动执行的。务必花时间按照本章前面“减少过度慷泛的权限”部分提到的移除该用户的过度权限。

# 总结

SQL Server 的历史决定了其某些安全组件继承自 Sybase；旧的 SQL Server 身份验证主要为了向下兼容和跨平台环境。SQL 的不同版本（企业版、标准版、个人版和开发版）根据其功能强弱具有不同的安全影响。微软数据引擎 (MSDE) 由于其低调的特性默认高权限安装，对安全性至关重要——用户通常完全不知道应用程序安装了 MSDE。本章回顾了 SQL Server 术语和安全概念，包括实例、网络库、登录名、角色和用户。

攻击者识别并渗透 SQL Server 所采取的步骤包括使用端口扫描器和数据包嗅探器等工具，以及查询 SQL 解析服务。技术包括使用发现机制以及如 SQLBF、SQLPoke 和 SQLPing 等暴力破解账户渗透工具。通过在 SQL Server 内部提升权限，可以实现操作系统和 SQL Server 内部特权数据的访问。

在本章中，我们研究了保护 SQL Server的方法，包括攻击者使用的某些发现技术，如端口扫描、查询服务控制器、查询 SQL 解析服务以及使用 sqlexe 等工具。此外，我们查看了重要的安全概念，包括尽量减少可能会使系统暴露在攻击风险的功能和权限。SQL Server 本身以及任何运行时身份登录和用户都应以最小权限运行。您应该通过 SQL Agent 服务、抓取日志和定期审计来监控、维护并检测您的 SQL Server 安装变化。

SQL Server 还可以通过其他应用程序使用 SQL 注入等技术受到直接攻击。SQL Server 安全并非在数据库管理员处结束这一观点至关重要。良好的安全性涉及分层方法，确保计算机系统的每一层都不会无意中暴露相邻的层。相反，良好的 SQL Server 安全可以帮助保护其他层，防止配置错误变成对您关键系统的全面渗透。

# 网站链接

- http://community.whitehatsec.com 这是一个关于 Web 应用安全的优秀网站，每个 SQL Server 安全专家都应该深入熟悉。

- http://online.securityfocus.com 该网站拥有互联网上最全漏洞数据库，并结合了顶级安全邮件列表。它是根据补丁级别查找 SQL Server 漏洞的好地方。

- www.owasp.org 在这里可以找到关于安全 Web 开发的良好信息。这里的重点是应用程序而非必然是数据库，但您需要对这两个层进行加密。

- www.microsoft.com/security 微软网站是 NT 和 SQL Server 安全的事实来源。通常情况下，人们应该先向微软提交新问题，以便其在全世界发现之前修复问题。

# 邮件列表

- Bugtraq (http://online.securityfocus.com) 这是一个涵盖所有平台漏洞披露、漏洞和补丁的优秀列表。它的审核较松，倾向于完全披露。如果您不介意看到许多与您可能的情况无关的问题，这是一个非常好的列表。它比大多数列表需要更多耐心，但通过这个列表的人并不多。

- NTBugtraq (www.ntbugraq.com) NTBugtraq 关注与微软操作系统相关的问题。它的审核非常严格，倾向于有限披露。对于那些只对微软相关的漏洞感兴趣，并且不介意漏掉几个可能进入 Bugtraq 的“不负责任”披露的人来说，这是一个很好的列表。

- VulnWatch (www.vulnwatch.org) 这是一个专注于漏洞而非讨论或补丁发布的完全披露列表。这是一个

![](img/729efc56f204a2ebffb8295c3a2dfdfb_699_0.png)

