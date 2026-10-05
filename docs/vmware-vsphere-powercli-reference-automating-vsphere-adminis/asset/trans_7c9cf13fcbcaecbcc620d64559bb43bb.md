

与保护虚拟机类似，取消虚拟机的保护涉及将虚拟机（VM）托管管理对象引用传递给保护计划的 `UnprotectVms` 方法。列表 22.8 允许你自动移除 SRM 保护。

## 列表 22.8 Remove-SrmProtection 函数

```powershell
function Remove-SrmProtection {
  < .SYNOPSIS
  从 SRM 保护组中移除虚拟机

  < .EXAMPLE
  Get-VM $vmName | Remove-SrmProtection -ProtectionGroup "oldPlan"
  从 SRM 保护组中移除虚拟机

  < .PARAMETER VM
  要取消保护的虚拟机。

  < .PARAMETER ProtectionGroup
  要从中移除虚拟机的保护计划名称。

  < .INPUTS
  [VMware.VimAutomation.ViCore.Impl.Vi.Inventory.VirtualMachineImpl]
#>
[CmdletBinding()]
param(
  [parameter(
    Mandatory=$true,
    ValueFromPipeline=$true
  )]
  [VMware.VimAutomation.ViCore.Impl.Vi.Inventory.VirtualMachineImpl]
  $VM
)

[parameter (Mandatory=$true)]
[String]$ProtectionGroup

process {
  if ($global:DefaultSrmServers.length -lt 1) {
    throw "未连接到 SRM 服务器"
  }
  $srmApi = $global:DefaultSrmServers[0].ExtensionData

  # 获取保护计划对象
  $ProtectionGroup = $srmApi.Protection.ListProtectionGroups() |
  Where-Object {$_.GetInfo().Name -eq $ProtectionGroup}

  # 更新保护组以取消保护 V
  $ProtectionGroup.UnprotectVms($VM.Id)
}
```

想要从 SRM 保护组中移除虚拟机时，可以使用之前的函数更新其状态：

Get-VM $vmName | Remove-SrmProtection -Plan $Name

## 将保护组添加到恢复计划

由于保护组本身包含了组合在一起的虚拟机，你需要确保保护组已添加到恢复计划中。恢复计划是执行操作的地方，恢复顺序、前置脚本和后续操作可以在此处配置。遗憾的是，目前无法通过 API 和 PowerShell 配置这些设置，因此必须依赖 GUI。不过，你至少可以确保保护组受恢复计划保护。在单步中完成此操作的函数位于 22.9。

### 列表 22.9 Add-SrmProtection 函数

```powershell
function Add-SrmProtection {
    .SYNOPSIS
    将保护组添加到恢复计划。

    # .EXAMPLE
    Add-SrmProtection -RecoveryPlan $planName -Group $group
    向计划添加组。

    # .PARAMETER RecoveryPlan
    要修改的恢复计划名称。

    # .PARAMETER ProtectionGroup
    要添加的保护组名称。

    # .OUTPUTS
    VMware.VimAutomation.Srm.Views.SrmRecoveryInfo

[CmdletBinding()]
param(
    [parameter (Mandatory=$true)]
    [String]
    $RecoveryPlan
    ,
    [parameter (Mandatory=$true)]
    [String]
    $ProtectionGroup
)
process {
    if ($global:DefaultSrmServers.length -lt 1) {
        throw "未连接到 SRM 服务器"
    }

    $srmApi = $global:DefaultSrmServers[0].ExtensionData

    # 从 API 获取恢复计划
    $plan = $srmApi.Recovery.ListPlans() | Where-Object {
        _.GetInfo().Name -eq $RecoveryPlan
    }

    # 获取保护组
    $group = $srmApi.Protection.ListProtectionGroups() | Where-Object {
      _.GetInfo().Name -eq $ProtectionGroup
    }

    if ($group.GetInfo().ProtectionGroups.MoRef -contains $group.MoRef) {
      Write-Warning "保护组 $($ProtectionGroup) 已经是 $($RecoveryPlan) 的成员"
    } else {
      $plan.AddProtectionGroup($group.MoRef)
      $plan.GetInfo()
    }
}
```

现在你可以简单快速地将保护组添加到恢复计划：

```powershell
Add-SrmProtection -RecoveryPlan $plan -Group $group
```

这将使用默认设置添加组，因此仍建议使用 GUI 验证恢复计划是否符合业务需求。但这是确保虚拟机有可用保护的方便方法。

## 测试恢复计划

在保护组添加恢复计划是确保在发生恢复时基础设施和组织已做好准备的一大步。然而，有了计划并不等同于有了测试过的计划。许多管理员认为自己的灾难恢复计划是可靠的，结果在执行时失败并需要大量干预。

SRM 提供了点击按钮测试保护计划的能力，并允许你验证虚拟机及其提供的服务能够在目标地有效恢复。测试可以使用 SRM API 执行，并通过 PowerCLI 访问。这意味着你可以随时自动化测试。22.9 提供了添加保护组的函数，结合 22.10 中的函数，你可以根据需要进行测试和清理循环。

### 列表 22.10 Invoke-SrmPlanAction 函数

```powershell
function Invoke-SrmPlanAction {
  # .SYNOPSIS
  在指定的 SRM 计划上执行操作

  # .EXAMPLE
  Invoke-SrmPlanAction -RecoveryPlan $planName -Failover
  开始故障转移

  # .EXAMPLE
  Invoke-SrmPlanAction -RecoveryPlan $planName -Test -WaitMinutes 30
  开始测试，最多等待 30 分钟完成

  # .EXAMPLE
  Invoke-SrmPlanAction -RecoveryPlan $planName -Cleanup
  测试操作后清理

  # .PARAMETER RecoveryPlan
  要执行的计划名称。

  # .PARAMETER Test
  指示测试操作。

  # .PARAMETER Cleanup
  指示清理操作。

  # .PARAMETER WaitMinutes
  等待完成的最大分钟数。

  [CmdletBinding()]
  param(
    [parameter (Mandatory=$true)]
    [String]
    $RecoveryPlan
    ,
    [parameter (Mandatory=$false)]
    [switch]$Test
    ,
    [parameter (Mandatory=$false)]
    [switch]$Cleanup
    ,
    [parameter (Mandatory=$false)]
    [int]$WaitMinutes = 5
  )
  process {
    if ($global:DefaultSrmServers.length -lt 1) {
        throw "未连接到 SRM 服务器"
    }

    $srmApi = $global:DefaultSrmServers[0].ExtensionData

    $plan = $srmApi.Recovery.ListPlans() | Where-Object {
        _.GetInfo().Name -eq $RecoveryPlan
    }

    $expectedState = ""
    $mode = 0
    if ($Test) {
        $expectedState = "Protecting"
        $mode = 1
    } elseif ($Cleanup) {
        $expectedState = "NeedsCleanup"
        $mode = 2
    } elseif ($Failover) {
        $expectedState = "Protecting"
        $mode = 0
    } elseif ($Reprotect) {
        $expectedState = "FailedOver"
        $mode = 3
    }

    if ($plan.GetInfo().State -eq $expectedState) {
        Write-Host "正在操作..." -NoNewline
        $plan.Start($mode);

        $start = Get-Date
        while ((New-TimeSpan $start).TotalMinutes -le $WaitMinutes) {
            if ($plan.GetInfo().State -ne "Running") {
                break
            }
            Write-Host "." -NoNewline
            Start-Sleep -Seconds 5
        }
        Write-Host "DONE!"

        $planHistory = $srmApi.Recovery.GetHistory($plan.MoRef)
        $planHistory.GetRecoveryResult(1)
    } else {
        Write-Warning "SRM 计划不处于预期状态。"
    }
  }
)
```

