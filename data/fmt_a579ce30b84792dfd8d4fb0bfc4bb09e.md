
$VSANRuleSet = New-SpbmRuleSet -AllOfRules $Rule1,$Rule2

$VSANStoragePolicy = New-SpbmStoragePolicy -Name 'VSAN Storage Policy 01' -Description 'VSAN Storage Policy' -AnyOfRuleSets $VSANRuleSet | Get-VMServer* | Set-SpbmEntityConfiguration -StoragePolicy $VSANStoragePolicy

# 第5章 使用高级 vSphere 特性

## 使用高级 vSphere 特性

在本章中，你将学习：

- 配置 EVC 166
- VFLASH 读缓存 171
- 管理 DRS 组 184
- 使用故障容错 (Fault Tolerance) 194
- 使用分布式电源管理 196
- 配置主机配置文件 (Host Profiles) 204
- 配置活动目录集成 207

到目前，我们已经表明由于众多原因，`vSphere` 是首选的虚拟化平台。本章重点介绍 `vSphere` 提供的一些最先进的功能。请注意，这些功能许多需要企业级许可才能使用。

### 配置 EVC

你是否尝试过在与新购买的服务器相同的集群中使用硬件？你是否遇到过虚拟机无法在不同代处理器之间进行 `vMotion` 的情况？新旧代 CPU 之间的特性往往是不兼容的。`VMware` 使用增强型虚拟机兼容性（EVC）来掩盖新一代 CPU 的功能，使其看起来与旧代具有相同的能力。这有助于在相同制造商的 CPU 之间进行 `vMotion`，即使它们差异巨大。但需要注意的是，EVC 不允许在不同制造商的 CPU 之间迁移。在较新的版本中，EVC 允许在不同代之间进行迁移。

在较新的版本中，通过 `PowerCLI` 允许在集群（`Cluster`）级别设置 EVC 模式，如列表 5.1 所示。

#### 5.1 设置 EVC 模式

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
```

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

```powershell
$procArchitecture = $.key
$evcModes.$procManufacturer += $procArchitecture
```

# 将映射到具有最大支持值的数组索引。

# 初始值设置得足够高以便在检查期间

# 被实际的主机值覆盖。

$maxSupported = `

$serviceInstance.Capability.SupportedEVCMode.length
```

```powershell
# 检查支持的最小值是多少
$nodeMaxEvcMode.GetEnumerator() | Foreach-Object {
$cpuManufacturer = ($_.Value -split "-") [0]
```
```powershell
# 获取此元素的索引值
$nodeEvcIndex = [Array]::IndexOf(
$evcModes.$cpuManufacturer,
$_.Value
```
```powershell
# 检查此 EVC 值是否小于
# 当前报告的最小值
if ($nodeEvcIndex -lt $maxSupported) {
$maxSupported = $nodeEvcIndex
}
```
```powershell
# 将值作为匿名对象返回
$obj = "" | Select-Object MaxEvcMode
$obj.MaxEvcMode = `
$evcModes.$cpuManufacturer {$maxSupported}
$obj
}
```

你可以结合列表 5.2 中创建的函数和标准的 `Set-Cluster` 命令行，快速方便地为任何服务器设置 EVC 模式。列表 5.3 显示了如何操作。

#### 列表 5.3 为集群设置 EVC 模式

```powershell
Get-Cluster $clustername | Set-Cluster $EVCMode (Get-Cluster $clustername) | 
Get-MaxEvcMode
```

同样，你可以通过将 EVC 模式设置为 `$null` 来禁用集群的 EVC，正如我们在列表 5.4 中做的那样。

#### 列表 5.4 禁用集群的 EVC

```powershell
Get-Cluster $clustername | Set-Cluster -EVCMode $null
```

EVC 是一个实用的功能，可以在包含多代服务器的集群中启用 `vMotion`，但它也有一些细微之处。例如，你可以在不关闭集群中所有虚拟机（VM）的情况下提高 EVC 级别，但无法在不先关闭虚拟机的情况下降低级别。同样，如果你从具有较高 EVC 设置的集群 `vMotion` 到较低设置的集群，你将需要关闭虚拟机。

考虑到此工作流，你可以无缝地替换整个集群的服务器，而无需跨集群进行 `vMotion`：
