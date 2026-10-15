
要使用本章包含的 PowerShell 函数，你需要为 vCenter Server 安装 Microsoft SQL Server Management Objects 程序包。这些包是作为 vCenter Server 上 SQL 安装程序的一部分安装的。如果你想从另一个系统运行脚本，你需要三个文件：适用于 SQL Server 的 Microsoft SystemCLR Types、Microsoft SQL Shared Management Objects 以及 Microsoft SQL Server 的 Microsoft Windows PowerShell Extensions。如果你运行的是 SQL 2014，可以在 Microsoft SQL Server 2014 Feature Pack 中找到它们。否则，你可以从 Microsoft 下载网站单独下载它们：

```
www.microsoft.com/downloads/
```

尽管本章侧重于 SQL 2014，但此处概述的步骤和函数适用于任何 SQL Server 2012 或更高版本。我们建议使用 SQL Server Management Studio 来调度维护任务（包括备份）。然而，由于本书的性质，我们将向你展示如何使用 PowerShell 完成此操作。

> 警告 请确保你不要干扰数据库上正在运行的备份计划！如果不确定数据库上是否有激活的备份计划，在继续使用本章中的 PowerShell 备份和恢复函数之前，请咨询你的数据库管理员。

# 创建完整数据库备份

过去几年里，微软在通过 PowerShell 简化 SQL 备份方面取得了巨大进展。最初，用户必须完全与 SQL Server 对象（类似于 PowerShell 对象）交互，这不像目前的方法那样直观。

此后微软引入了 `Backup-SqlDatabase` cmdlet 来简化备份过程。

要使用此 cmdlet，你首先需要将 `SQLPS` 模块导入你的 PowerShell 会话中：

```
Import-Module "SQLPS"
```

`SQLPS` 模块中有几个 cmdlet 不符合标准的 cmdlet 命名规范，在导入模块时会产生警告信息。如果你不想看到此警告，可以使用 `-DisableNameChecking` 参数来抑制警告。导入模块后，你就可以使用 `Backup-SqlDatabase` cmdlet 了。

`Backup-SqlDatabase` cmdlet 针对各种用例具有大量参数。我们将只关注其中一小部分；请注意，你可以像我们在这里这样，利用该 cmdlet 备份更多的 SQL 数据库。

要创建完整数据库备份，你需要以下信息：

- **服务器实例 (Server Instance)**：托管数据库的服务器名称。
- **数据库 (Database)**：你计划备份的数据库名称。
- **备份文件位置 (Backup File Location)**：备份文件的目标位置。
- **备份操作 (Backup Action)**：定义你是在备份数据库、文件还是日志的规范。
- **凭据 (Credentials)**：连接数据库所需的用户名和密码。

在第 1 章的示例“自动化 vCenter Server 部署和配置”中，我们使用了带有 SQL 身份验证的远程 SQL 数据库，而不是 Windows 身份验证。因为使用了 SQL 身份验证，我们必须在命令中指定凭据。如果我们使用 Windows 身份验证，并从具有 vCenter Server 数据库权限的 Windows 账户执行这些命令，就不需要指定凭据了。

```
Backup-SqlDatabase -ServerInstance "MGMT-DB" -Database vCenter6 \
-BackupFile C:\Temp\Mybackup.bak -BackupAction Database \
-Credential (Get-Credential)
```

如果未指定备份操作的值，则将默认执行完整备份。

备份完成后，你可以查看文件并验证其是否成功。命令中指定的备份文件位于 SQL 服务器。如果指定了无效位置，将返回错误，如图 12.1 所示。

## 12.1 无效位置错误

```
Administrator: Windows PowerShell
PS C:\> Backup-SqlDatabase -ServerInstance SQLClient -Database Sales -BackupFile "C:\Backups\Sales.bak"
PS C:\> Backup-SqlDatabase -ServerInstance SQLClient -Database Sales -BackupFile "D:\InvalidPath\Sales.bak"
CategoryInfo: InvalidOperation: () (Backup-SqlDatabase)
SqlError: The operation 'Backup database' failed because Microsoft SQL Management could not open the path specified.
:Backup-SqlDatabaseCommand
PS C:\ _
```

如果备份成功，你将在命令指定的位置看到该文件。

# 创建差异备份

你还可以创建差异备份。对于变化较少的大型数据库，差异备份特别有用。差异备份仅存储自上次备份以来的的更改。这种方法缩短了备份窗口，但是有代价的。如果你使用差异备份并需要恢复数据库，必须先恢复最后的完整备份，然后是最后的差异备份。差异备份只能在非简单恢复模式的数据库上执行。默认情况下，vCenter 安装将数据库设置为简单恢复模式。

要创建差异备份，你必须将 `-BackupAction` 参数设置为 `Database`。一旦设置好，在命令中添加 `-Incremental` 参数：

```
Backup-SqlDatabase -ServerInstance "MGMT-DB" -Database vCenter6
-BackupFile C:\Temp\Mybackup.bak -BackupAction Database \
-Incremental -Credential (Get-Credential)
```

# 创建日志备份

你可以制作的第三种备份类型是日志备份。通过日志备份，你可以将数据库恢复到特定的时间点。日志备份通常比数据库备份消耗的资源，因此你可以更频繁地创建它们。

## 第 12 章 组织你的灾难恢复

注意，你只能对非简单恢复模式（Simple recovery mode）的数据库执行日志备份。要对数据库的事务日志文件进行备份，请在 Log 中使用 `-BackupAction` 参数：

```powershell
-Backup-SqlDatabase -ServerInstance "MGMT-DB" -vCenter6
```

```powershell
-BackupFile C:\Temp\Mybackup.bak -BackupAction Log -Credential (Get-Credential)
```

# 恢复你的 vCenter Server

在恢复 vCenter Server 环境时，根据你的原始设置，有几种可能性。如果你使用了外部数据库，请先恢复你的数据库。遵循你数据库供应商的指南。数据库上线后，请按照下一节中概述的步骤安装并恢复你的 vCenter 环境。

> 提示 在 vSphere 6 中，不再支持 Microsoft SQL Server Express。如果你使用内部的 vFabric Postgres 数据库，你将无法恢复 SQL 备份。你只能对使用 SQL 的 vCenter Server 部署恢复 SQL 备份。

## 恢复你的 vCenter Server 数据库

在恢复数据库之前，你需要使用 `Stop-Service` cmdlet 停止 vCenter Server 服务。因为 vCenter Server 有依赖服务，你必须提供 `-Force` 参数：

```powershell
Stop-Service vpxd -Force
```

要恢复数据库，请使用 SQL Server cmdlet。恢复与备份类似，但现在我们使用 `Restore-SqlDatabase` cmdlet。就像备份 cmdlet 一样，恢复 cmdlet 有一些你需要定义的属性。首先，提供你想要执行的恢复类型。在这里，如果你想恢复数据库并在数据库已存在时覆盖它：

```powershell
Restore-SqlDatabase -ServerInstance MGMT-DB -Database VCENTER6 -BackupFile "C:\Temp\MyBackup.bak" -ReplaceDatabase -Credential (Get-Credential)
```
