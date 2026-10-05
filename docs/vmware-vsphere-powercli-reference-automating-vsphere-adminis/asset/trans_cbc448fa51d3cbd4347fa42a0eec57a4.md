

```powershell
[parameter(
    Mandatory=$true,
    ParameterSetName="EnableDpm"
))
[Switch]
$Enable
,
[parameter(
    Mandatory=$true,
    ParameterSetName="DisableDpm"
))
[Switch]
$Disable
,
[parameter(
    Mandatory=$false,
    ParameterSetName="EnableDpm"
))
[ValidateRange(1, 5)]
[Int]
$Threshold
,
[parameter(
    Mandatory=$false,
    ParameterSetName="EnableDpm"
))
[ValidateSet("Automated", "Manual")]
[String]
$Behavior
)
process {
    # 用于存储消息的数组
```

# 使用分布式电源管理 201

$whatIf = @()

# 获取相关的配置数据
$clusterObj = Get-Cluster $Cluster
$clusterView = $clusterObj | Get-View -Property Name

$dpmConfig = New-Object VMware.Vim.ClusterDpmConfig

```powershell
# 根据 Enable/Disable 属性设置操作
# 同时，也设置 WhatIf 操作
if ($Disable) {
    $dpmConfig.Enabled = $false
    $whatIf += "Disabling DPM"
}
```

```powershell
if ($Enabled) {
    $dpmConfig.Enabled = $true
    $whatIf += "Enabling DPM"
}
```

```powershell
# 如果提供了则设置剩余属性
if ($Behavior) {
    $dpmConfig.DefaultDpmBehavior = \
VMware.Vim.DpmBehavior::$Behavior
    $whatIf += "Setting behavior to: $($Behavior)"
}
```

```powershell
if ($Threshold) {
    $dpmConfig.HostPowerActionRate = $Threshold
    $whatIf += "Setting Threshold to: $($Threshold)"
}
```

```powershell
# 创建配置规范并设置我们的信息
$clusterConfig = New-Object \
VMware.Vim.ClusterConfigSpecEx
$clusterConfig.DpmConfig = $dpmConfig
```

```powershell
if ($PSCmdlet.ShouldProcess(
$clusterView.Name,
```

使用 vSphere 环境进行安装、配置和管理 第一部分

# 第 5 章 • 使用高级 vSphere 特性

```powershell
$whatIf -join ""
)
# 执行更新
$taskId = $clusterView.
ReconfigureComputeResource_Task(
  $clusterConfig,
  $true
)
$task = Get-View $taskId

# 等待更新完成
while (
  "running", "queued" -contains $task.Info.State
){
  $task.UpdateViewData("Info")
  Start-Sleep -Seconds 1
}
```

```powershell
# 返回错误或当前状态
if ($task.Info.State -eq "error") {
  Write-Error $task.Info.Error.LocalizedMessage
} else {
  $clusterObj | Get-DPM
}
```

将所有内容整合在一起，要在任何当前禁用 DPM 的集群上启用 DPM，你需要运行以下命令：

```powershell
Get-Cluster |
  Get-DPM |
  Where-Object { $_.Status -eq "Disabled" } |
  Set-DPM -Enable
```

# 配置主机配置文件

你也可以执行基础管理。例如，你只需一行 DPMCLI 即可将主机电源操作速率设置为 4，并将默认 DPM 行为设置为自动：

![](img/62596f5acc979040608a4e5111beb7d6_234_0.png)

# 主机电源操作级别

在 Set-DPM 函数中显示为阈值的操作级别定义了建议执行电源操作的级别。vCenter 建议开启或关闭主机的操作级别发生在资源不平衡时。例如，1 级操作非常激进，会关闭主机；5 级非常保守，很少关闭主机。这些设置影响许多操作。

现在你可以自动化 DPM 了，对关闭 vSphere 主机感到担心是可以理解的。随着你建立信心并开始意识到节省电力，你自然会提高自动化水平。如果你目前没有使用 DPM，没有任何理由不尝试。数据中心相关的电力成本是持续开支之一。谁知道呢？节省电费，也许你就能说服老板去 VMWorld 旅行了！

# 配置主机配置文件

主机配置文件用于确保 vCenter 内系列主机的一致性。这是通过识别参考主机并创建主机配置文件来实现。主机配置文件捕获该主机的配置并将其保存到 vCenter 数据库中。之后任何时候，你都可以根据配置文件测试给定的 vSphere 主机并报告合规性。如果主机偏离了合，你只需重新应用配置文件。对于 vSphere 6，主机配置文件目前涵盖以下配置设置：

- 高级选项
- 身份验证
- 日期/时间
- 防火墙
- 组
- 内存预留
- 网络
- 安全
- 存储
- 用户

# 20 创建主机配置文件

```powershell
New-HostProfile -Name Prod01 `
  -ReferenceHost (Get-Host prod01) `
  -Description "集群配置文件"
```

# 21 关联主机配置文件并检查合规性

```powershell
Apply-HostProfile -Entity (Get-Host prod01) `
  -Profile (Get-HostProfile prod01) `
  -AssociateOnly
```

# 22 将主机配置文件应用于任何不合规的主机

```powershell
Get-Cluster Prod01 |
Get-VMHost |
Test-VMProfileCompliance |
ForEach-Object {
  $profile = Get-HostProfile $_.VMHost |
  Set-VMHost -State 'Maintenance' -VMHost $_.VMHost |
  Apply-HostProfile -Profile $profile |
  Set-VMHost -State 'Connected' |
  Test-HostProfileCompliance
}
```

# 23 使用主机配置文件对集群进行更改

```powershell
$cluster = Get-Cluster prod01

# 添加数据存储
$cluster | Get-VMHost |
```

