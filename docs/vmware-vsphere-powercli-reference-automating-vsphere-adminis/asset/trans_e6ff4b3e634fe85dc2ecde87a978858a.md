

# 为企业备份应用程序提供 PowerShell 支持

Veeam 也是最早为其应用程序添加 PowerShell 支持的供应商之一。在 8.0 版本中，他们拥有 272 个可用于管理此应用程序的 cmdlet。

# 要求

确保您在安装过程中选择了 Veeam Backup & Replication PowerShell SDK，因为它在 8.0 版本中不是默认选项。

# 启动

由于 VBR cmdlets 是 PowerShell Snap-in 的一部分，我们可以使用 `Add-PSSnapin` cmdlet 将其添加到 PowerShell 会话中（列表 11.13）。

+ 列表 11.13 将 Veeam Snap-in 添加到 PowerShell 会话

```bash
Add-PSSnapin VeeamPSSnapIn
```

> 提示：确保在具有管理员权限的 PowerShell 会话中运行 Veeam Snap-in；Snap-in 中的某些 cmdlet 需要此权限。

在开始创建任何备份作业之前，您需要将 VBR 连接到服务器源。该产品能够备份来自 VMware vCenter、VMware vCloud Director 和 Microsoft Hyper-V 的虚拟机，并包含了连接到这些这些源类型的 cmdlet。我们将重点关注 VMware vCenter 源。

# 将 Veeam Backup & Replication 连接到 vCenter

作为将 VBR 连接到 vCenter的一部分，您需要一组凭据来建立连接并获得备份虚拟机的权限。最好为此目的使用专用的服务账户，并在 vCenter 中授予该账户所需的权限。然后使用 `Add-VirtualCredential` 创建连接（列表 11.14）。

+ 列表 11.14 将 VBR 连接到 vCenter

```bash
$vCenterCredentials = Get-Credential
Add-VBRvCenter -Name vcenter01.sunnydale.local -User $vCenterCredentials.UserName -Password ($vCenterCredentials.GetNetworkCredential()).Password
```

# 创建存储库

您需要一个存储库作为备份作业备份数据存储的目标。VBR 8.0 支持以下目标类型：Microsoft Windows Server、Linux Server、CIFS/SMB 文件共享、EMC Data Domain、ExGrid 和 HP StoreOnce。使用 `Add-VBRBackup` cmdlet 创建存储库。在列表 11.15 中，我们创建了一个 SMB 存储库作为备份作业的目标。

# 列表 11.15 创建 SMB 存储库

```bash
$SMBCredentials = Get-Credential
Add-VBRBackupRepository -Name 'SynologySMB' -Folder \\\synology.sundayle.local\vbr' -CifsShare -Username $SMBCredentials.Username -Password ($SMBCredentials.GetNetworkCredential()).Password
```

# 从源清单中检索实体

备份作业的另一个要求是识别您想要包含在备份中的虚拟机。VBR 允许您以 vCenter 对象列表的形式提供这些对象：vCenter 服务器、数据中心、文件夹、资源池、虚拟中心、ESXi 主机或特定的虚拟机列表。使用 vCenter 对象（如集群或文件夹）而不是特定的虚拟机列表的优势在于，当这些对象中包含的虚拟机发生变化时，无需修改备份作业。

您可以使用 `Find-VBREntity` cmdlet 来列出所有可能项。可以使用 `-Name` 参数进行过滤。当该创建备份作业时，请使用 `Find-VBREntity` 提供要包含的虚拟机或 vCenter 对象。

# 列表 11.16 从源清单中作为实体检索虚拟机和集群

```bash
Find-VBREntity -Name Server01 -VmsAndTemplates
Find-VBREntity -Name Cluster01 -ResourcePool
```

# 计划

对于每个备份作业，您还需要一个该作业运行的计划。VBR Snap-in 提供了 `Set-VBRJobSchedule` cmdlet，用于在创建作业后设置计划。

# 为企业备份应用程序提供 PowerShell 支持

# 备份作业模板

现在您已有了创建备份作业模板所需的所有元素。列表 11.17 为名为 Cluster01 的集群中的所有虚拟机创建一个备份作业，将数据存储在 SynologySMB 存储库中，并设置了每天上午 8 点开始的周中计划。查看创建备份作业模板的帮助是非常值得的，例如 `Add-VBRViBackupJob`、`Set-VBRViJobRepository` 和 `Set-VBRViJobSchedule` 以了解可用功能。

# 11.17 创建备份作业模板

```bash
$ClusterEntity = Find-VBRViEntity -Name Cluster01 -ResourcePool
$Repository = Get-VBRBackupRepository -Name SynologySMB
Add-VBRViBackupJob -Name Cluster01 -Entity $ClusterEntity -Repository $Repository

$Job = Get-VBRJob -Name Cluster01
$Job | Set-VBRJobSchedule -DailyKind Weekly
$JobOptions = Get-VBRJobOptions -Job $Job
$JobOptions.RunManually = $false
Set-VBRJobOptions -Job $Job -Options $JobOptions
```

# 多个备份作业模板

在 PowerShell 中创建单个备份作业模板并不一定比在 VBR GUI 中创建能节省大量时间。然而，当你转而创建多个备份作业模板时，这种节省就能体现出来。列表 11.18 展示了如何为集群 01–05 创建备份作业模板，并让每个集群的启动时间错开一小时。注意，这与创建单个备份作业模板相比，代码量并没有显著增加。

# 11.18 创建多个备份作业模板

```bash
$Clusters = 1..5 | ForEach-Object "Cluster0$_"
$Repository = Get-VBRBackupRepository -Name SynologySMB
$InitialStartTime = [DateTime]"20:00"
$i = 0

foreach ($Cluster in $Clusters){
$ClusterEntity = Find-VBRViEntity -Name $Cluster -ResourcePool
```

![](img/62596f5acc979040608a4e5111beb7d6_426_0.png)

第三部分

# 第11章 • 备份和恢复您的虚拟机

```bash
Add-VBRBackupJob -Name $Cluster -Entity $Entity -BackupRepository $Repository
```

```bash
$BackupTime = $InitialStartTime.AddHours($i)
```

```bash
$Job = Get-VBRJob -Name $Cluster
$Job | Set-VBRJobSchedule -DailyKind Weekly
$JobOptions = Get-VBRJobOptions -Job $Job
$JobOptions.RunManually = $false
Set-VBRJobOptions -Job $Job -Options $JobOptions
```

```bash
}
```

# 恢复作业

要从备份作业恢复虚拟机，您需要使用 `Get-VBRServer`。列表 11.19 使用最新的还原点为 Server01 启动恢复作业。它不会覆盖现有的 Server01，而是创建一个新名称。

# 11.19 恢复虚拟机

```bash
$Restorespoint = Get-VBRRestorePoint -Name Server01 | Sort-Object CreationTime | Select-Object -Last 1
$Server = Get-VBRServer -Name pesxi01.sunnydale.local
Start-VBRRestoreVM -RestorePoint $Restorespoint -VMName Server01_Restore -Server $Server -RunAsync
```

# 第12章 组织您的灾难恢复

在本章中，您将学习：

- 备份您的 VCENTER 数据库 398
  备份您的 vCenter 数据库 ............................................ 398

- 恢复您的 VCENTER 402
  恢复您的 vCenter 数据库 ............................................ 402
  重新连接 ESXI 主机 ................................................................ 403

- 导出 VCENTER 清单项 407
  文件夹 ...................................................................................... 407
  数据中心 ................................................................................ 410
  集群 ..................................................................................... 412
  角色 ........................................................................................ 413
  权限 ................................................................................ 414
  虚拟机位置 ............................................................................... 414
  主机 ........................................................................................ 415
  标签 ........................................................................................ 416
  网络 ................................................................................................ 418

- 导入 VCENTER 清单项 421
  文件夹和数据中心 ............................................................ 421
  数据中心文件夹 ................................................................................. 422
  集群 ..................................................................................... 423
  主机 ........................................................................................ 424
  虚拟机位置 ............................................................................... 426
  角色 ........................................................................................ 426
  权限 ................................................................................ 427
  网络 ................................................................................................ 428

- 恢复虚拟机 434

