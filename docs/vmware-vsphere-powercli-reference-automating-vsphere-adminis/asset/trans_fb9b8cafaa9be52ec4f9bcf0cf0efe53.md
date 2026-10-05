

```powershell
-Object "VirtualMachine" -Status "red"
```

# 在 vCenter 根节点创建告警
$dc = Get-Datacenter -Name "DC1"
New-Alarm -Name "Book: guest lost network" -Description \
-"VM network lost" \
-Entity $dc \
-Action $groupactions -Expression $expression -Enabled```

下一个示例（如列表 17.11 所示）创建了一个当有人更改虚拟机（guest）上的自定义属性时，就会触发的告警。该告警将运行一个 PowerShell 脚本。

# 列表 17.11 虚拟机自定义属性告警

```powershell
# 转换状态
$trans = @()
$trans += New-AlarmTransition -Start "green" -Final "yellow"
```

```powershell
$groupactions = @()

# 运行脚本
$cmd = "C:\Windows\System32\cmd.exe /c powershell.exe" + \
-"PSConsole file C:\Scripts\MyConsole.pscl -noninteractive + \
-"-profile -file C:\Scripts\Custom-changed.ps1"
$action = New-AlarmActionScript -Path $cmd
$groupactions += New-AlarmTriggerAction -Action $action \
-Transition $trans
```

```powershell
# 在 cpu.usage.average 指标上触发告警
$expression = @()
$expression += New-AlarmExpressionOr
$expression += New-AlarmExpressionEvent \
-Event "CustomFieldValueChangedEvent" \
-Object "VirtualMachine" -Status "yellow"
```

```powershell
# 在数据中心上创建告警
$dc = Get-Datacenter -Name "DC1"
New-Alarm -Name "Book: CA changed" \
-Description "custom attribute changed" \
-Entity $dc
```

![](img/62596f5acc979040608a4e5111beb7d6_640_0.png)

# 第 17 章 • 告警

-Action $groupactions -Expression $expression -Enabled
通过操作运行的脚本与列表 17.12 中的代码如所示。

# 列表 17.12 Custom-changed.ps1

```powershell
$ErrorActionPreference = "$SilentlyContinue"
$Error.Clear()

$ErrorFile = "C:\error.txt"

$line = "Time:" + (Get-Date).ToShortTimeString()
$line += (",User:" + $env:VMWARE_ALARM_EVENT_USERNAME)
$line += (",On:" + $env:VMWARE_ALARM_TARGET_NAME)
$line += (",Description:" + $env:VMWARE_ALARM_EVENTDESCRIPTION)

$line | Out-File -FilePath "C:\changes.txt" -Append

if($Error) {
  "== Errors" | Out-File -FilePath $errorFile -Append
  $Error | Out-File -FilePath $errorFile -Append
}
```

# 删除告警

Remove-AlarmDefinition 函数（参见列表 17.13）非常直观；它会删除你传递给该函数的一个或多个告警。

# 列表 17.13 删除告警定义

```powershell
function Remove-AlarmDefinition {
  <
  .SYNOPSIS
删除一个或多个告警定义
  .DESCRIPTION
该函数将删除所有名称匹配的告警定义。
  .PARAMETER Name
数据存储名称
  .INPUTS
System.String

.OUTPUTS
None

.EXAMPLE
Remove-AlarmDefinition -Name "Book: My Alarm"

.EXAMPLE
Remove-AlarmDefinition -Name "Book:*"

```

```powershell
#
[CmdletBinding(SupportsShouldProcess,ConfirmImpact="High")]
Param (
    [parameter(Mandatory=$true)]
    [NotNullOrEmpty()]
    [string]$Name
)
```

```powershell
$alarmMgr = Get-View AlarmManager
$alarmMgr.GetAlarm($null) | ForEach-Object {
    $alarm = Get-View $_
    if ($alarm.Info.Name -like $Name){
        if ($PSCmdlet.ShouldProcess($Name)) {
            $alarm.RemoveAlarm()
        }
    }
Remove-AlarmDefinition 函数使用非常简单。`-Name` 参数用于指定要删除的特定告警。`-Name` 参数也可以作为通配符（例如 `Test*`），用于删除多个以 Test 开头的告警。

```powershell
Remove-AlarmDefinition -Name "Book: obsolete alarm"
Remove-AlarmDefinition -Name "Test*"
```

# 修改告警

VMware PowerCLI 模块包含许多用于管理现有告警的 cmdlet，但没有用于创建新告警或删除现有告警的 cmdlet。因此，可以使用这些 cmdlet 对现有告警进行更改。可用的 cmdlet 如下：

```powershell
Get-Command *alarm* -Module VMware.VAutomation.Core
```

| 命令类型 | 名称 | 模块名 |
| --- | --- | --- |
| Cmdlet | Get-AlarmAction | VMware.VimAutomation.Core |
| Cmdlet | Get-AlarmTrigger | VMware.VimAutomation.Core |
| Cmdlet | Get-AlarmDefinition | VMware.VimAutomation.Core |
| Cmdlet | New-AlarmAction | VMware.VimAutomation.Core |
| Cmdlet | New-AlarmTrigger | VMware.VimAutomation.Core |
| Cmdlet | Remove-AlarmAction | VMware.VimAutomation.Core |
| Cmdlet | Remove-AlarmTrigger | VMware.VimAutomation.Core |
| Cmdlet | Set-AlarmDefinition | VMware.VimAutomation.Core |

例如，列表 17.14 展示了如何为现有的 CPU Usage 添加新告警。

```powershell
Get-AlarmDefinition -Name "Host Usage" | New-AlarmAction -ScriptPath 'c:\monitor.bat'
```

可以使用 `Get-AlarmDefinition` 来检查告警操作：

```powershell
(Get-AlarmDefinition "Host Usage").ExtensionData.Info.Action.Script
c:\monitor.bat
```

# 迁移告警

在同一个 vCenter 内迁移告警非常简单，有很多脚本可以使用。你可以在这里找到此类脚本示例：

```
www.vmware.com/2020/02/alarms-them-around/
```

当你需要在无法相互“看到”的 vCenter 之间迁移告警定义时，无法使用从一个 vCenter 读取告警定义并在另一个 vCenter 上重新创建它们的脚本。在这种情况下，脚本需要在目标 vCenter 运行。遗憾的是，PowerShell 对象的序列化和反序列化并不简单。这就是为什么我们使用以下替代方案。`Get-AlarmScript` 函数接收一个由 `Get-Alarm` 函数产生的对象，并将生成创建告警所需的所有 PowerShell 代码。这些 PowerShell 代码可以保存为 PSI 文件并传输到你的目标 vCenter。当你在目标 vCenter 上执行代码时，告警就会创建。`Get-AlarmScript` 和 `Get-Alarm` 函数包含了作者编写并在本书前面提到的 `vCenterAlarms` 模块。

列表 17.15 显示了同时使用这两个函数的示例。

# 列表 17.15 生成在 vCenter 之间迁移告警的 PowerShell 代码

```powershell
Get-Alarm -Name "Book: test alarm" | Get-AlarmScript | Set-Content "C:\myAlarm.ps1"
```

文件 `myAlarm.ps1` 将包含可以在另一个 vCenter 上执行的 PSI 脚本，只要定义告定义的实体存在，脚本就会创建一个与原始告警相同的新告警。生成的脚本类似于列表 17.16。

# 列表 17.16 myAlarm.ps1

```powershell
#Requires -Version 4.0
#Requires -Modules @{ModuleNameName="VMware.VimAutomation.Core";ModuleVersion="6.0.0.0"}

$spec = New-Object VMware.Vim.AlarmSpec
```

![](img/62596f5acc979040608a4e5111beb7d6_644_0.png)

```powershell
$spec.Name = "Book: Change custom field"
$spec.Description = ""
$spec.ActionFrequency = 0
$spec.Enabled = $True
```

```powershell
$action = New-Object VMware.Vim.GroupAlarmAction

$action1 = New-Object VMware.Vim.AlarmTriggeringAction
$action1.Green2yellow = $False
$action1.RedYellow = $False
$action1.Yellow2green = $False
$action1.Yellow2red = $False
$trans1 = New-Object VMware.AlarmTriggeringTransitionSpec
$trans1.StartState = "green"
$trans1.FinalState = "yellow"
$trans1.Repeats = $False

$action1.TransitionSpecs += $trans1

$action.Action += $action1
```

```powershell
$spec.Action = $action

$expression = New-Object VMware.Vim.OrAlarmExpression

$expression1 = New-Object VMware.Vim.EventAlarmExpression
$expression1.EventType = CustomFieldValueEvent
$expression1.EventID = "im.event.CustomFieldValueEvent"
$expression1.ObjectType = VirtualMachine
$expression1.status = yellow

$expression.Expression += $expression1

$spec.Expression = $expression
```

```powershell
$setting = New-Object VMware.Vim.AlarmSetting
$setting.reportingFrequency = 0
```

```powershell
$setting.toleranceRange = 0
```

```powershell
$spec.Setting = $setting
```

```powershell
$entity = Get-Inventory -Name DC1
```

```powershell
$alarmMgr = Get-View AlarmManager
$alarmMgr.CreateAlarm($entity.Extensiondata.MoRef,$spec)
```

> 注意 使用列表 17.16 生成的脚本时，应考虑到，如果跨 vCenter 迁移的告警带有脚本文件，那么源 vCenter 上的这些脚本文件需要复制到目标 vCenter 的相同位置。

# 获取当前活跃告警

现在你已经能够创建新告警、修改现有告警并删除它们，列表最后一项是显示活跃告警。列表 17.17 展示了 `Get-ActiveAlarm` 函数，它将返回给定 vSphere 实体的活跃告警。

# 列表 17.17 获取实体的活跃告警

```powershell
function Get-ActiveAlarm {
  .SYNOPSIS
返回实体上当前的活跃告警
  .DESCRIPTION
返回实体上当前的活跃告警
  .INPUTS
System.Management.Automation.PSCustomObject
  .OUTPUTS
System.Management.Automation.PSCustomObject
  .EXAMPLE
$Folder = Get-Folder "Datacenters"
Get-ActiveAlarm -Entity $Folder
  .EXAMPLE
Get-Cluster Cluster01 | Get-ActiveAlarm
}
```

