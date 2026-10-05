

# 遵循指南操作

覆盖 "VDS."。PowerCLI 的增长为我们提供了一种检查和设置 vSphere 分布式组端口级覆盖的方法，通过 `Set-VDPortGroupOverridePolicy` 和 `Set-VDPortGroupOverridePolicy` 令实现，这两个命令均自 PowerCLI 5.5 Release 1 起可用。PowerCLI 6.0 提供的 `Set-VDPortGroupOverridePolicy` 命令允许你设置九个 `DVPortGroupPolicy` 和 `VMwareDVSPortGroupPolicy` `OverrideAllowed` 属性中的任何一个。PowerCLI 将帮助你如何使用该命令。

为了增加额外价值，我们创建了一个高级函数（见列表 13.9），可以使用它来评估并修复此指南中的所有 vSphere 分布式端口组（VDPortgroup）覆盖配置。

## 13.9 评估和修复 VDPortgroup 覆盖选项

```powershell
function Assert-HardeningGuideVNetworkPortOverride {
# .Description
函数用于评估和修复 VMware 加固指南中 Guideline ID 为
"vnetwork.restrict-port-level-overrides" 的项目（该指南中没有相应的
PowerCLI 评估/修复代码）。此指南旨在“限制 VDS 上的端口级配置覆盖”。此函数将
评估/更新 VDPortgroup 策略的 OverrideAllowed 属性。
.Example
Assert-HardeningGuideVNetworkPortOverride
评估所有 VDPortgroups 的 OverrideAllowed 设置
.Example
Get-VDSwitch myVDSSwitch0 | Get-VDPortgroup |
Assert-HardeningGuideVNetworkPortOverride -Remediate:$true
获取每个 VDSSwitch 的 VDPortgroups，并针对每个加固指南修复每个端口组的 OverrideAllowed 设置。
.Outputs
如果正在修复，则会更新每个 VDPortgroup 的 VMware.VimAutomation.Vds.Impl.V1.VMwareVDPortGroupImpl
对象。如果只是报告，则为每个 VDPortgroup 创建一个 PSCustomObject，
包含有关给定覆盖策略的信息，以及该 VDPortgroup 配置是否符合加固指南的建议。
#>
```

![](img/62596f5acc979040608a4e5111beb7d6_498_0.png)

保护您的 vSphere 环境

第三部分

```powershell
[CmdletBinding(SupportsShouldProcess=$true)]
Param(
## 要评估/修复的虚拟分布式端口组。如果未指定，
## 将作用于当前会话连接的 VIServer 中的所有 VDPortgroups
    [parameter(ValueFromPipeline=$true)] [PSObject[]]$VDPortgroup,
    ## 关：是否修复实体？默认为 $false，导致函数
# 仅报告
    [switch]$Remediate = $false
)
```

```powershell
begin {
## 每个 OverrideAllowed 属性的期望值
$DesiredConfigValue = $false
## 要评估/更新的 "*OverrideAllowed" 属性的名称
$arrOverridePortNames = Write-Output BlockOverrideAllowed,
VendorConfigAllowed,VlanOverrideAllowed,ipfixOverrideAllowed,
trafficFilterOverrideAllowed,NetworkResourcePoolOverrideAllowed,
SecurityPolicyOverrideAllowed,ShapingOverrideAllowed,
uplinkTeamingOverrideAllowed
}
```

```powershell
## 使用 VDPortgroups 的策略值创建一些对象，并注意它们
# 是否都符合建议值
$arrVDPGPolicyInfo = $arrVDPGOInterest | Foreach-Object {
$oVSPGPolicy_thisPG = $_.Extensionondata.Config
New-Object -Type PSObject -Property (ordered)@{
VDPortgroup = $_.Switch
# 此 PG 策略的所有给定属性是否都已设置为
# 期望配置值？
$HasSuggestedValues = $DesiredConfigValue -eq ($arrOverridePropNames |
Foreach-Object {$oVSPGPolicy_thisPG.$_} | Select-Object -Unique)
BlockPorts = $oVSPGPolicy_thisPG.BlockOverrideAllowed
TrafficShaping = $oVSPGPolicy_thisPG.ShapingOverrideAllowed
VendorConfiguration = $oVSPGPolicy_thisPG.VendorOverrideAllowed
VLAN = $oVSPGPolicy_thisPG.VlanOverrideAllowed
UplinkTeaming = $oVSPGPolicy_thisPG.UplinkTeamingOverrideAllowed
ResourceAllocation =
$oVSPGPolicy_thisPG.NetworkPoolOverrideAllowed
SecurityPolicy = $oVSPGPolicy_thisPG.SecurityPolicyOverrideAllowed
NetFlow = $oVSPGPolicy_thisPG.ipfixOverrideAllowed
TrafficFilteringMarking =
$oVSPGPolicy_thisPG.trafficFilterOverrideAllowed
}
```

```powershell
if ($Remediate) {
# 仅获取 OverrideAllowed 值与建议值
# 不相同的 VDPortgroups
$arrVDPGTRemediate = $arrVDPGPolicyInfo | Where-Object {
$_.HasSuggestedValues -eq $false
} |
Select-Object -Unique -ExpandProperty VDPortgroup

if (($arrVDPGTRemediate | Measure-Object).Count -eq 0) {
    Write-Verbose "*所有指定的 VDPortgroups 的其 OverrideAllowed 策略均具有建议值"
}
```

![](img/62596f5acc979040608a4e5111beb7d6_500_0.png)

```powershell
else {
    $ArrVDPGToRemediate | Foreach-Object {
        $ThisVDPG = $_
        if ($PSCmdlet) ShouldProcess($ThisVDPG)
        # 此处逻辑根据原文包含修复逻辑，由于原文代码块不完整，保持结构
    }
}
```
