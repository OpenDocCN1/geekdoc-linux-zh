

## 第 12 章 组织你的灾难恢复

注意，你只能对非简单恢复模式（Simple recovery mode）的数据库执行日志备份。要对数据库的事务日志文件进行备份，请在 Log 中使用 `-BackupAction` 参数：

```powershell
-Backup-SqlDatabase -ServerInstance "MGMT-DB" -vCenter6
```

```powershell
-BackupFile C:\Temp\Mybackup.bak -BackupAction Log -Credential (Get-Credential)
```

## 恢复你的 vCenter Server

在恢复 vCenter Server 环境时，根据你的原始设置，有几种可能性。如果你使用了外部数据库，请先恢复你的数据库。遵循你数据库供应商的指南。数据库上线后，请按照下一节中概述的步骤安装并恢复你的 vCenter 环境。

> 提示 在 vSphere 6 中，不再支持 Microsoft SQL Server Express。如果你使用内部的 vFabric Postgres 数据库，你将无法恢复 SQL 备份。你只能对使用 SQL 的 vCenter Server 部署恢复 SQL 备份。

## 恢复你的 vCenter Server 数据库

在恢复数据库之前，你需要使用 `Stop-Service` get 停止 vCenter Server 服务。因为 vCenter Server 有依赖服务，你必须提供 `-Force` 参数：

```powershell
Stop-Service vpxd -Force
```

要恢复数据库，请使用 SQL Server cmdlet。恢复与备份类似，但现在我们使用 `Restore-SqlDatabase` cmdlet。就像备份 cmdlet 一样，恢复 cmdlet 有一些你需要定义的属性。首先，提供你想要执行的恢复类型。在这里，如果你想恢复数据库并在数据库已存在时覆盖它：

```powershell
Restore-SqlDatabase -ServerInstance MGMT-DB -Database VCENTER6 -BackupFile "C:\Temp\MyBackup.bak" -ReplaceDatabase -Credential (Get-Credential)
```

如果你在 PowerShell 控制台中收到错误消息“由于数据库正在使用，无法获取独占访问权限”，你可能还需要停止 `vmware-cis-config` 服务并重试：

```powershell
Stop-Service vmware-cis-config -Force
```

恢复完成后，你可以使用 `Start-Service` cmdlet 启动 vCenter Server：

```powershell
Start-Service vpxd
```

如果你为了恢复数据库而停止了 `vmware-cis-config` 服务，你将需要确保也启动该服务。

## 重新连接 ESXI 主机

当你在没有原始 SSL 证书备份的情况下恢复 vCenter Server 时，vCenter Server 将无法加密 ESXi 主机。所有 ESXi 主机将显示为已断开。在这种情况下，你必须通过重新连接它们对每个主机重新进行身份验证。在替换 vCenter Server 证书时，你必须重新连接所有 ESXi 主机以更新 ESXi 主机密码。

你可以使用 `Set-VMHost` cmdlet 重新连接 ESXi 主机，该 cmdlet用于更改主机配置。将 `-State` 参数设置为 `Connected` 以重新连接已断开的主。要断开主机，将 `-State` 参数设置为 `Disconnected`。

```powershell
Set-VMHost esx01 -State Connected
```

你应该理解，如果 SSL 证书是有效的，`Set-VMHost` cmdlet 将不允许你重新连接服务器，此时错误为：“由于用户名或密码错误无法完成登录。”

当你必须处理无效的 SSL 证书且仅使用 PowerCLI cmdlets 时，你唯一的选择是使用 `Remove-VMHost` 和 `Add-VMHost` cmdlet 移除并重新添加主机。

```powershell
Remove-VMHost -Name esx01 -Confirm:$false
Add-VMHost -Name esx01 -User root -Password VMware! -Location MainDC -Force
```

然而，这种方法有一个缺点。移除 ESXi 主机将移除该主机的所有配置，包括资源池、虚拟机等。这绝对是你不希望在生产环境或恢复操作期间发生的。

![](img/62596f5acc979040608a4e5111beb7d6_434_0.png)

好消息是还有另一种选择。它依赖使用 `Get-View` cmdlet 获取的 vSphere API 对象

```powershell
$vmHostView = Get-View -ViewType HostSystem -Filter @{"Name" = "esx01"}
```

`VMware.Vim.HostSpec` 对象包含一个 `ReconnectHost()` 方法。如果你查看方法的定义，你会发现 `ReconnectHost()` 方法接受一个 `VMware.Vim.HostSpec` 对象作为输入。该对象允许你指定用于身份验证 ESXI 主机的用户名和密码，如下：

```powershell
$objHostConnectSpec = New-Object VMware.Vim.HostSpec
$objHostConnectSpec.userName = $user
$objHostConnectSpec.password = $password
```

要重新连接 ESXI 主机，你需要调用 `ReconnectHost()` 方法并使用你定义的 `$objHostConnectSpec` 变量：

```powershell
$vmHost.Reconnect_Task($objHostConnectSpec, $null)
```

