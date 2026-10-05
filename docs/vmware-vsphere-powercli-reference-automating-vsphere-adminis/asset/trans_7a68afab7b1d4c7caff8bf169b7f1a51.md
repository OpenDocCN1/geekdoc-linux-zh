
因此，为了启用此强大功能，你必须启用 IP 分配并指定将使用哪些协议。在 vSphere Web Client 中，这被分为两个步骤：Set-vAppIPAsignment 函数（见列表 10.24）允许在一行 PowerCLI 代码中配置 IP 分配（前提是在会话中已了该函数，当然）。

# 列表 10.24 Set-vAppIPAsignment 函数

```
<#  .SYNOPSIS
    为指定的 vapp 设置 IP 分配。
  .DESCRIPTION
    为指定的 vapp 设置 IP 分配。这些
    设置控制客机软件如何配置
    IP 地址，包括协议类型
    （IPv4 或 IPv6）以及这些 IP 地址的生存周期。
  .PARAMETER vapp
    要修改 IP 分配设置的 vapp。
  .PARAMETER IpProtocol
    指定此部署选择的 IP 协议。
    这必须是 SupportedIpAllocation
    中的值之一。
  .PARAMETER IpAllocationPolicy
    指定 VI 平台如何管理 IP 分配。
    这通常由部署者指定。
    有效选项为 'dhcpPolicy'、'transientPolicy' 和
    'fixedPolicy'
  .PARAMETER SupportedIpAllocation
    指定客机软件支持的 IP 分配方案。
    更新此字段时，格式为 "" 的数组
    将清除所有设置。
    否则，提供的值将覆盖
    当前设置。
  .PARAMETER SupportedIpProtocol
    指定客机软件支持的 IP 协议。
    更新此字段时，格式为 "" 的数组
    将清除所有设置。

    否则，提供的值将覆盖
    当前设置。
```

![](img/62596f5acc979040608a4e5111beb7d6_394_0.png)

# 第 10 章 使用 VAPPS

```
#>
function Set-vAppIPAddressAssignment {
    [CmdletBinding(SupportsShouldProcess=$true)]
    Param (
        [parameter(ValueFromPipeline=$true)]
        [VMware.VmAutomation.V1Core.Impl.V1.VAppImpl]
        $vApp
        [parameter(ValueFromPipelinePropertyName=$true)]
        [ValidateSet('IPv4', 'IPv6')]
        [string]
        $IpProtocol
        [parameter(ValueFromPipelinePropertyName=$true)]
        [ValidateSet('dhcpPolicy',
            'transientPolicy',
            'fixedPolicy')]
        [string]
        $IpAllocationPolicy
        [parameter(ValueFromPipelinePropertyName=$true)]
        [ValidateSet('ovfenv', 'dhcp')]
        [string[]]
        $SupportedIpAllocation
        [parameter(ValueFromPipelinePropertyName=$true)]
        [ValidateSet('IPv4', 'IPv6')]
        [string]
        $SupportedIpProtocol
    )
    Process {
        $spec = New-Object VMware.Vm.VAppConfigSpec
        $spec.IpAssignment = $vApp.ExtensionData.VAppConfig.
        IpAssignment
        $msg = "Modifying ${($vApp.Name)}"
        Switch ($PSCMdlet.MyInvocation.BoundParameters.Keys) {
            'IpProtocol' {
                $msg = "{0} IP protocol:{1}" -f $msg, $IpProtocol
                $spec.IpAssignment.IpProtocol = $IpProtocol
            }
        }
    }
}
```

# 'IpAllocationPolicy'

```
{
  $msg = "{0} IP allocation policy:{1}" -f $msg;
  $IpAllocationPolicy
  $spec.IpAssignment.IpAllocationPolicy = \
  $IpAllocationPolicy
}
```

```
'SupportedIpAllocation'
{
  $msg = "{0} supported allocation policy:{1}" -f \
  $msg, $($SupportedIpAllocation -join ',');
  $spec.IpAssignment.SupportedAllocationScheme = \
  $SupportedIpAllocation
}
```

```
'SupportedIpProtocol'
{
  $msg = "{0} supported IP protocol:{1}" -f $msg;
  $($SupportedIpProtocol -join ',\');
  $spec.IpAssignment.SupportedIpProtocol = \
  $SupportedIpProtocol
}
```

```
if ($PSCmdlet.ShouldProcess ($vApp.Name, $msg))
{
  $vApp.ExtensionData.UpdateVAppConfig($spec)
  if ($?)
  {
    Get-vAppIPAssignment -vApp $vApp
  }
  Else
    Write-Warning "Failed to set vApp IP Assignment check vCenter"
}
```

10.25 使用 Set-vAppIPAssignment 函数同时为 IPv4 和 IPv6 协议启用 DHCP 和 IP 池，并设置 vApp 使用临时 IPv4 地址从池中获取 IP。

# 10.25 为 App01 配置 IP 分配

```
Get-VApp App01 | Set-vAppIPAssignment \
-SupportedIpAllocation ovfenv, DHCP
-SupportedIpProtocol IPv4, IPv6
-IpProtocol IPv4
-IpAllocationPolicy transientPolicy
```

```
IpProtocol : IPv4
IpAllocationPolicy : transientPolicy
SupportedIpAllocation : {ovfenv, DHCP}
SupportedIpProtocol : {IPv4, IPv6}
vApp : App01
```

# 修改 vApp 产品信息

深入研究 vApps 可以发现以产品信息形式存在的额外元数据。要获取现有 vApp 的信息，提供了 Get-vAppProductInfo 函数（见 10.26）。

# 10.26 Get-vAppProductInfo 函数

```
<#  .SYNOPSIS
    获取指定的 vapp 的产品信息。
  .DESCRIPTION
    获取指定的 vapp 的产品信息。
  .PARAMETER vapp
    要获取产品信息的 vapp。
```

# 10.27 Set-vAppProductInfo 函数

```
<#  .SYNOPSIS
    设置指定的 vapp 的产品信息。
  .DESCRIPTION
    设置指定的 vapp 的产品信息。
  .PARAMETER vapp
    要设置产品信息的 vapp。
```

