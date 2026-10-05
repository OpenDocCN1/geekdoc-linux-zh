

```powershell
elseif ($ESXIHost -isnot [VMware.VimAutomation.VCore.Impl.V1.Inventory.VMHostImpl]){
    Write-Warning "您传递的不是字符串或 VMHost 对象"
    continue
}

# --- 创建主机维护规格
try {
```powershell
$VSANHostDecommissionModeObjectAction = `
New-Object VMware.Vim.VsanHostDecommissionModeObjectAction `
-Property @value = $VSANModeValue
```

```powershell
$VSANHostDecommissionMode = `
New-Object VMware.Vim.VsanHostDecommissionMode `
-Property "ObjectAction" = $VSANHostDecommissionModeObjectAction
```

```powershell
$HostMaintenanceSpec = `
New-Object VMware.Vim.HostMaintenanceSpec `
-Property "VSANMode" = $VSANHostDecommissionMode
```
}
catch [Exception] {
    $ErrorText = "无法为 $ESXIHost 创建主机维护规格"
    throw
}

# ---  {带有 VSAN 选项的维护模式
try {
    if ($PSCmdlet.ShouldProcess($ESXIHost)) {
```powershell
$MaintenanceModeTask = $ESXIHost.ExtensionData.EnterMaintenanceMode_Task(0,$true,$HostMaintenanceSpec)
$Task = Get-Task -Id $MaintenanceModeTask
```
![](img/62596f5acc979040608a4e5111beb7d6_192_0.png)

# 162 第 4 章 • 存储自动化

```powershell
while ((($Task.State -ne 'Success') -and ($Task.State -ne 'Error'))) {
```

```powershell
Write-Verbose "正在等待 VSAN 维护模式任务完成（已完成：$($Task.PercentComplete)%）"
Start-Sleep -Seconds $PollSeconds
```

```powershell
$Task = Get-Task -Id $MaintenanceModeTask
}
if ($Task.State -eq 'Success') {
```powershell (注：此处原文代码块标记重复，已修正)
Write-Verbose "ESXiHost 的 VSAN 维护模式任务成功！操作耗时：$(New-TimeSpan -Start $Task.StartTime -End $Task.FinishTime)'"
Get-VMHost $ESXiHost | Select-Object Name,ConnectionState
```

```powershell
if ($Task.State -eq 'Error') {
Write-Warning "$ESXIHost 的 VSAN 维护模式任务失败"
}
}
catch [Exception] {
```powershell
$ErrorText = "$ESXIHost 的 VSAN 维护模式任务失败"
throw
}
catch [Exception] {
    if ($ErrorText) {
        throw "无法将 VMHost $($ESXIHost) 设置为 VSAN 维护模式。错误为：($ErrorText)"
    }
    else {
        throw "无法将 VMHost $ESXIHost 设置为 VSAN 维护模式"
    }
}
}
end {

典型的用法类似于以下示例：

```hell
PS C:\ Get-VMHost vsanesxi101* | Set-VMHostMaintenanceMode -VSANMode Evacuate
```

## 存储策略

在本章前面的部分，我们展示了如何创建存储策略。通过 VSAN，你可以利用它的某些功能创建存储策略。（在之前的示例中创建了 vCenter 标签）。列表 4.33 展示了如何使用 VSAN 功能 `VSAN.hostFailuresToTerate` 和 `VSAN.cacheReservation` 创建存储策略，并将其分配给带有通配符 `Server*` 的虚拟机。

## 列表 4.33 创建 VSAN 存储策略并分配给虚拟机

```powershell
$Rule1 = New-SpbmRule -Capability (Get-SpbmCapability) -Name 'VSAN.hostFailuresToTerate' -Value 1
$Rule2 = New-SpbmRule -Capability (Get-SpbmCapability) -Name 'VSAN.cacheReservation' -Value 10
$VSANRuleSet = New-SpbmRuleSet -AllOfRules $Rule1,$Rule2
$VSANStoragePolicy = New-SpbmStoragePolicy -Name 'VSAN Storage Policy 01' -Description 'VSAN Storage Policy' -AnyOfRuleSets $VSANRuleSet | Get-VMServer* | Set-SpbmEntityConfiguration -StoragePolicy $VSANStoragePolicy
```

## 使用高级 vSphere 特性

在本章中，你将学习：

- 配置 EVC 166
- VFLASH 读缓存 171
- 管理 DRS 组 184
- 使用故障容错 (Fault Tolerance) 194
- 使用分布式电源管理 196
- 配置主机配置文件 (Host Profiles) 204
- 配置活动目录集成 207

到目前，我们已经表明由于众多原因，vSphere 是首选的虚拟化平台。本章重点介绍 vSphere 提供的一些最先进的功能。请注意，这些功能许多需要企业级许可才能使用。

## 配置 EVC

你是否尝试过在与新购买的服务器相同的集群中使用硬件？你是否遇到过虚拟机无法在不同代处理器之间进行 vMotion的情况？新旧代 CPU 之间的特性往往是不兼容的。VMware 使用增强型虚拟机兼容性（EVC）来掩盖新一代 CPU 的功能，使其看起来与旧代具有相同的能力。这有助于在相同制造商的 CPU 之间进行 vMotion，即使它们差异巨大。但需要注意的是，EVC 不允许在不同制造商的 CPU 之间迁移。在较新的版本中，EVC 允许在不同代之间进行迁移。

在较新的版本中，通过 PowerCLI 允许在集群（Cluster）级别设置 EVC 模式，如列表 5.1 所示。

```powershell
## 5.1 设置 EVC 模式

.SYNOPSIS
获取集群的 EVC 模式。

.DESCRIPTION
该函数获取集群所支持的 EVC 模式。

.EXAMPLE
Get-MaxMode -Cluster (Get-Cluster)

.PARAMETER Cluster
要获取 EVC 模式的集群。

.INPUTS
VMware.VimAutomation.VCore.Impl.V1.Inventory.ClusterImpl

.OUTPUTS
PSCustomObject

```powershell
[CmdletBinding()]
param(
    Mandatory=$true,
    ValueFromPipeline=$true
)
    [VMware.VimAutomation.VCore.Impl.V1.Inventory.ClusterImpl]
    $Cluster
)
process {
    $hosts = $Cluster | Get-VMHost

    # 获取每个主机的最大模式
    $nodeMaxMode = @{}

    $hosts | Foreach-Object {
        $nodeMaxMode.Add(
            $_.Name,
            $_.ExtensionData.Summary.MaxEVC
        )
    }

    # 检查是否存在不同的 CPU  {
    $lastManufacturer = ""

    $incompatible = $false

    $nodeMaxMode.GetEnumerator() | Foreach-Object {
        $currentManufacturer = ($_.Value -split "-") [0]
        if ($lastManufacturer -eq "") {
            $lastManufacturer = $currentManufacturer
        }

        if ($lastManufacturer -ne $currentManufacturer) {
            Write-Warning "存在 Intel 和 AMD CPU"
            $incompatible = $true
        }
    }

    # 检查所有模式是否相同
    [Array]$evcGroups = $nodeMaxMode.GetEnumerator() |
    Group-Object -Property Value

    if ($evcGroups.Count -eq 1) {
        # 如果相同，输出第一个
        $obj = $ | Select-Object MaxEcMode
        $obj.MaxEcMode = $evcGroups[0].Name
        $obj
    }
    elseif ($incompatible -eq $false) {
        # 如果不相同，我们需要找出最小公约数
        # 收集所有可用的 EVC 模式
        $evcModes = @{
            'intel' = @();
            'amd' = @();
        }

        $serviceInstance = Get-View ServiceInstance

        $serviceInstance.Capability.SupportedEVCMode | Foreach-Object {
            $procManufacturer = ($_.key -split "-") [0]
            $evcModes[$procManufacturer] += $_.key
        }

        # (此处逻辑未完成，遵循原文结束)
    }
}
```

