

# 第 9 章 • 高级虚拟机功能

驱动器：Z:
制造商：(标准 CD-ROM 驱动器)
卷名：VM001

这是一个特别有趣的例子，因为 `Get-WmiObject` 命令令实现了对 WMI 的封装。然而，通过用 `Invoke-Command` 命令令封装 `Get-WmiObject`，PowerShell 使用 PowerShell 远程管理（PowerShell Remoting）在远程执行 `Get-WmiObject`，而该命令反过来又远程机器上本地执行 WMI 查询。

你可以使用 `Enter-PSession` 命令令启动交互式会话：

```
PS C:\> Enter-PSession VM001
[VM001]: PS C:\>
```

注意命令提示符已变为 `[VM001]: PS C:\`，表示 PowerShell 会话现在正在远程计算机 VM001 上运行。完成后，通过发布 `Exit-PSession` 命令令退出交互式会话。

让我们进一步，在脚本中使用 PowerShell 远程管理技术。在列表 9.2 中，你会发现一个使用 PowerShell 远程报告服务状态的脚本。可选开关允许启动或重启服务。

# 列表 9.2 使用 PowerShell 远程管理报告服务状态

```powershell
<# SYNOPSIS
  使用 PowerShell 远程管理检查服务的状态
.DESCRIPTION
  此函数使用 PowerShell 
  远程管理检查服务的状态。
  如果服务已停止，可以使用可选的重启开关
  来重启服务。
.PARAMETER Computer
  要检查服务状态的一个或多个计算机名称
.PARAMETER Service
  要检查的一个或多个服务名称
.PARAMETER Start
  启动已停止服务的可选参数
.PARAMETER Restart
  重启服务的可选参数
.EXAMPLE
  PS> Check-Service -Computer VM001 -Service wuauserv
#>
```

# 与客机交互

```powershell
function Check-Service {
  Param(
    [parameter (Mandatory = $true)]
    [string]$Computer,

    [parameter (Mandatory = $true)]
    [string]$Service,

    [switch]$Start,

    [switch]$Restart
  )
  #建立持久连接
  $session = New-PSSession $Computer
  $remoteService = Invoke-Command -Session $session \
    -ScriptBlock {
      param($ServiceName)
      $localService = Get-Service $ServiceName
      $localService
    }-ArgumentList $Service
  if ($Start -and $remoteService.Status -eq "Stopped") {
    Invoke-Command -Session $session -ScriptBlock {
      $localService.Start()
    }
    $remoteService | Add-Member -MemberType NoteProperty \
    -Name Restart -Value $true
  }
  if ($Restart) {
    Invoke-Command -Session $session -ScriptBlock {
      $localService.Stop()
      $localService.WaitForStatus("Stopped")
      $localService.Start()
    }
    $remoteService | Add-Member -MemberType NoteProperty \
    -Name Started -Value $true
  }
  #关闭持久连接
  Remove-PSSession $session
  Write-Output $remoteService
}
```

![](img/62596f5acc979040608a4e5111beb7d6_334_0.png)

第二部分

# 第 9 章 • 高级虚拟机功能

每次运行远程命令时都设置会话会降低性能。可以通过 `New-Session` 命令令创建持久会话来缓解此问题。可以使用 `-Session` 参数对持久会话进行安全保护。要关闭持久会话，请使用 `Remove-PSSession` 命令令。

例如，让我们通过报告 `wuauserv` 服务的状态，验证远程服务器 VM001 是否仍在接收 Windows 更新，如列表 9.2 所示：

```powershell
Check-Service VM001 wuauserv
```

| 状态 | 名称 | 显示名称 | 计算机 |
|---|---|---|---|
| 运行 | wuauserv | Automatic Updates | VM001 |

> 提示 如果你想了解更多关于 PowerShell 远程信息，`about_remote` 是一个很好的起点。原生方法的缺点是总是需要网络连接。但对于位于防火墙后或完全隔离的虚拟机怎么办？幸运的是，可以使用 PowerCLI。PowerCLI 允许通过 `Invoke-VMscript` 命令令在虚拟机内部执行脚本。唯一的要求是虚拟机必须安装了 VMware Tools。使用此强大的工具，无论如何都可以与客机进行交互，只要安装了 VMware Tools 即可。

由于支持批处理和 Bash 脚本，任何可以通过批处理或 Bash 脚本启动的内容（例如旧的 VBScript 脚本或 Linux 中的 Perl 脚本）都可以远程执行。为了运行 PowerShell 脚本，必须确保客机上安装了 PowerShell。

```powershell
Get-Help about_remote
```

当你被迫处理文本时，可能需要额外的处理。在本例中，使用了 `.Trim()` 方法来删掉 `wmic` 在输出开头返回的空行；如果没有它，CSV 将是无效。CSV 表头必须位于 CSV 文件的第一行。现在，`cdrom` 变量以良好的 PowerShell 对象格式包含了所需信息：

```powershell
# 将文本转换为对象
$cdrom = $Output.ScriptOutput.Trim() | Convert-Csv
```

