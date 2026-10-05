

# 按照指南操作

| VirtualPortGroup（虚拟端口组） | AllowPromiscuous | ForgedTransmits | MacChanges |
|---|---|---|---|
| MgmtNetwork | False | False | False |
| dNet0 | False | False | False |
| vESXiNet0 | False | False | False |

注意我们为虚拟交换机设置了显式安全策略，然后更新了这些虚拟交换机上虚拟端口组的安全策略，以继承虚拟交换机配置的设置。你可以在列表 13.7 中看到相同的技巧，但它使用了 VMware.VimAutomation.Vds PowerCLI 模块来处理分布式网络组件。

# 列表 13.7 报告和更新分布式交换机/端口组安全策略

```powershell
Import-Module VMware.VimAutomation.Vds
## 比加固指南更直接的方式进行评估：
Get-VDSwitch | Get-VDSecurityPolicy
```

| VDSwitch（分布式交换机） | AllowPromiscuous | MacChanges | ForgedTransmits |
|---|---|---|---|
| vDSw-Dev0 | True | True | False |
| vDSw-Prod1 | False | True | True |

```powershell
Get-VDSwitch | Get-VDPortgroup | Get-VDSecurityPolicy
```

| VDPortgroup（分布式端口组） | AllowPromiscuous | MacChanges | ForgedTransmits |
|---|---|---|---|
| dvPG01 | True | False | False |
| vMotion | True | False | True |

```powershell
## 修复
Get-VDSwitch | Get-VDSecurityPolicy | Set-VDSecurityPolicy \
-AllowPromiscuous:$false -MacChanges:$false -ForgedTransmits:$false
```

![](img/62596f5acc979040608a4e5111beb7d6_492_0.png)

# 加固 vSphere 环境

VDSwitch AllowPromiscuous MacChanges ForgedTransits 

| | | | |
|---|---|---|---|
| vDSw-Dev0 | False | False | False |
| vDSw-Prod1 | False | False | False |

Get-VDSwitch | Get-VDPortgroup | Get-VDSecurityPolicy | Set-VDSecurityPolicy -AllowPromiscuousInherited:$true -ForgedTransitsInherited:$true -MacChangesInherited:true

VPortgroup AllowPromiscuous MacChanges ForgedTransits

| | | | |
|---|---|---|---|
| dvPG01 | False | False | False |
| vMotion | False | False | False |

下一个 vNetwork 指南需要 PowerCLI 来帮助处理 `vNet-work.limit-network-healthcheck`。加固指南建议：“如果只需要它，请启用 VDS 网络健康检查”。由于没有用于直接检查和管理这些健康检查选项的 cmdlet，我们在列表 13.8 中创建了该函数。

# 列表 13.8 评估和修复网络健康检查选项

```powershell
function Assert-HardeningGuideVNetworkHealthChk {
<#Description
用于评估和/或修复 VMware 加固指南中指南为
"vNetwork.limit-network-healthcheck" 的项目（该指南中没有
PowerCLI 评估/修复代码）。该指南建议禁用这些健康检查项，因为正如指南所述，
“一旦启用，健康检查包将包含主机、vds# 端口# 等信息，攻击者会发现这些信息有用”
.Example
Assert-HardeningGuideVNetworkHealthChk
报告所有虚拟分布式交换机健康检查配置项的当前值
.Example
Get-VDSwitch myVDSwitch0, myVDSwitch1 |
Assert-HardeningGuideVNetworkHealthChk -Remediate:$true

按照加固指南建议禁用 vDSitches 上任何启用的健康检查设置

.Outputs
如果进行修复，将更新每个 VDSwitch 的 VMware.VimAutomation.Vds.Impl.V1.VmwareVDSwitchImpl
对象。如果只是报告，则返回涉及的每个 VDSwitch 的 Selected.Vmware.Vim.VmwareVDSwitchV1MinutHealthCheckConfig 和 Selected.Vmware.Vim.VmwareDVSteamingHealthCheckConfig 对象

```powershell
#
[CmdletBinding(SupportsShouldProcess=$true)]
Param(
    ## 要评估/修复的分布式交换机。如果没有指定，将
    # 报告
    # 对当前会话连接的 VIServer 中的所有 VDSitches 执行操作
    [parameter(ValueFromPipeline=$true)] [PSObject[]]$VDSwitch,
    ## 交换机：修复该实体？默认为 $false，会导致更改
    [switch]$Remediate = $false
)
begin {
    ## HealthCheckConfig 属性的期望值
    $DesiredConfigValue = $false
}

process {
    $ArrVDSwitchOfInterest = if ($PsBoundParameters.ContainsKey("VDSwitch")) {
        if ($VDSwitch.GetType().Name -eq "VmwareVDSwitchImpl") {$VDSwitch}
        else {Get-VDSwitch -Name $VDSwitch}
    } else {Get-VDSwitch}
}
```
```

![](img/62596f5acc979040608a4e5111beb7d6_494_0.png)

# 第三部分

# 第 13 章 加固 vSphere 环境

```powershell
## 获取 VDSwitch 的 HealthCheckConfig 信息
$arrHealthCheckConfigInfo = $VDSwitch | Foreach-Object {
  $ThisVDSwitch = $_
  $ThisVDSwitch.ExtensionData.HealthCheckConfig |
    Select-Object @(n="VDSwitch"; e=$ThisVDSwitch),
    @(n="HealthCheckType"; e={$GetType().Name}),
    @(n="Enabled"; e={$Enable}),
    @(n="SuggestedValue"; e={$DesiredConfigValue -eq $_})
}

if ($Remediate) {
  # 获取健康检查值与建议值不符的 VDSwitch
  $arrVDSwitchToRemediate = $arrHealthCheckInfo |
    Where-Object {$_.SuggestedValue -eq $false}
    Select-Object -Unique -ExpandProperty VDSwitch
  # 用于更新 DVSHealthConfig 的健康检查项
  $arrVDSHealthCheckItems = @(
    "VMware.Vim.VmDVSTamingHealthCheckConfig",
    "VMware.Vim.VmVSlanMtuHealthCheckConfig"
  )
  $arrVDSwitchToRemediate | ForEach-Object {
    $ThisVDSwitch = $_
    if ($ShouldProcess($ThisVDSwitch, "禁用 $($ThisVDSwitch.Name) 上的健康检查)")) {
      try {
        $Task = $ThisVDSwitch.ExtensionData.UpdateHealthCheckConfig($arrVDSHealthCheckItems | ForEach-Object {
            @{ Name = $_; Enabled = $DesiredConfigValue }
        })
        Wait-Task -Id $Task.Id | Out-Null
        $TaskFinal = Get-Task -Id $Task.Id
        if ($TaskFinal.State -eq "Success") {
            Get-VDSwitch -Name $ThisVDSwitch
        } else {
            Write-Error "设置 $($ThisVDSwitch.Name) 的健康配置失败。任务结果：($TaskFinal.Result)。以及任务错误：($TaskFinal.ExtensionData.Info.Error)"
        }
      } catch {
        Write-Error "启动 $($ThisVDSwitch.Name) 配置任务失败""
      }
    }
  }
} else {
  # 否则仅返回健康检查信息
  $arrHealthCheckConfigInfo
}
```

![](img/62596f5acc979040608a4e5111beb7d6_496_0.png)

