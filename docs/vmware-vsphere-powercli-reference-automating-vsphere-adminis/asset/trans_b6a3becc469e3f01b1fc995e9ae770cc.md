

## 设置网络

Select-Object -ExpandProperty MoRef

```powershell
try {
    Get-VIObjectByVIView `
    $dvSwitchManager.QueryCompatibleHostForExistingDvs($MoRef,
    $r, $Vds.MoRef)
} catch {
    Write-Warning "在 ($VIObject.name) 中未找到兼容的主机"
}
```

在下一个练习中，我们感兴趣识别 Prod01 数据中心中任何可以添加到我们新 VDS 的 VMHost（列表 3.15）。

## 列表 3.15 查找 VDS VMHost 候选主机

```powershell
Get-Datacenter PROD01 | Get-DistributedSwitchCandidate -DistributedSwitch 'PROD01-VDS02' -Recurse
```

| 名称 | 连接状态 | 运行电状态 |
|---|---|---|
| vesxi05.sunndyle... | 已连接 | 已开启 |
| vesxi06.sunndyle... | 已连接 | 已开启 |

列表 3.15 中的代码专门定位了两个可以添加到我们新 VDS 的 vSphere 主机。接下来，识别将绑定到 VDS 上行程序的 pNIC。记住，你可以使用列表 3.2 中的 `Get-VMHostDetailedNetworkInfo` 函数帮助识别分配到正确位置的正确 pNIC。

现在你准备好添加你的主机了。为了完成此任务，请使用列表 3.6 所示的代码添加以下内容：

- VMHost: vesxi06
- pNIC: vmnic2, vmnic3, vmnic4, vmnic5
- vDS: PROD01-VDS02

## 列表 3.16 将 VMHost 添加到 vDS

```powershell
$VMHost = Get-VMHost 'vesxi06*'
$NetworkAdapters = $VMHost | \
Get-VMHostNetworkAdapter \
-Name vmnic2,vmnic3,vmnic4,vmnic5 -Physical
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
Add-VDSSwitchVMHost -VDS $VDSSwitch02 -VMHost $VMHost
Add-VDSSwitchPhysicalNetworkAdapter -DistributedSwitch $VDSSwitch02 -NIC $NetworkAdapters -Confirm:$false
```

大功告成了——从无到有一个准备好托管 VM 的 VDS。现在，如果你在想：“我打赌这一切可以合并成一个步骤”，你是正确的！将你从 VDS 列表中学到的知识结合并将这些步骤合并为一个单一步骤。

如果你在事后修改 pNIC 映射，你需要使用 `Remove-VDSSwitchPhysicalNetworkAdapter` 命令，如列表 3.17 所示。

## 列表 3.17 修改现有的 VDS-to-VMHost pNIC 映射

```powershell
# 移除适配器 vmnic4 和 vmnic5
$VMHost | Get-VMHostNetworkAdapter -Name vmnic4,vmnic5 -Physical | \
Remove-VDSSwitchPhysicalNetworkAdapter -Confirm:$false
```

如果你需要完全移除主机，可以使用 `Remove-VDSSwitchVMHost` 命令（列表 3.18）。你可以从分布式交换机 (PROD01-VDS02) 移除主机（在我们的示例中为 vesxi06）。如果你是从 vCenter 移除主机，此命令可以很容易地处理。

## 列表 3.18 从 VDS 移除 VMHost

```powershell
$VMHost = Get-VMHost 'vesxi06*'
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
$VDSSwitch02 | Remove-VDSSwitchVMHost -VMHost $VMHost -Confirm:$false
```

那么，DVPG 中的 VMkernel 网络适配器呢？虽然比它们的 VDS 兄弟复杂一点，但它们不仅可以使用，还可以使用 PowerCLI 进行自动化。在列表 3.19 中，我们正在创建一个符合以下规格的新 VDS 网络适配器：

- VDS: PROD01-VDS02
- DVPG: vMotion
- vSphere 主机: vesxi06
- IP: 192.168.2.40
- 启用 v

注意：如果你按照示例操作，在运行列表 3.19 之前，确保已通过列表 3.16 将主机添加到 VDS。

![](img/62596f5acc979040608a4e511beb7d6_128_0.png)

## 列表 3.19 在 DVPG 上创建网络适配器

```powershell
$VMHost = Get-VMHost 'vesxi06'
$VDSwitch2 = Get-VDSwitch -Name 'PROD01-VDS02'
$vMotionDVPG = $VDSwitch2 | New-DVPortgroup -Name 'vMotion' -VlanId 853
$vmk = New-VMHostNetworkAdapter -VMHost $VMHost \
-PortGroup $vMotionDVPG -VirtualSwitch $VDSwitch2 \
-IP 192.168.2.40 -SubnetMask 255.255.255.0
$vmk | Set-VMHostNetworkAdapter -vMotionEnabled:$true -Confirm:$false
```

后续管理使用 `Set-VMHostNetworkAdapter` 更新更新移除适配器是直接的。当你需要在整个集群上启用容错 (FT) 等操作时，你会很快发现这些功能的强大。如列表 3.20 所示，即使是这项也可以在 PowerCLI 中完成。

## 列表 3.20 跨集群启用 FT 日

```powershell
[System.Collections.Array]$IPAddresses = '192.168.5.10', '192.168.5.11'
$VDSwitch2 = Get-VDSwitch -Name 'PROD01-VDS02'
$FTDVPG = $VDSwitch2 | New-DVPortgroup -Name 'FT' -VlanId 700
foreach ($VMHost in (Get-Cluster Cluster01 | Get-VMHost)) {
    $vmkFT = New-VMHostNetworkAdapter -VMHost $VMHost \
    -PortGroup $FTDVPG -VirtualSwitch $VDSwitch2 \
    -IP $IPAddresses[0] -SubnetMask 255.255.255.0
    $vmkFT | Set-VMHostNetworkAdapter \
      -FaultToleranceLoggingEnabled:$true -Confirm:$false
    $IPAddresses.RemoveAt(0)
}
```

## 创建分布式交换机的副本

如果需要部署新的分布式交换机，可能需要与 vCenter 中已有的项目一致的配置，例如发现协议和管理员联系详情。VDS 模块包含通过 `New-VSwitch` 命令执行此操作的方法。列表 3.21 展示了如何从 PROD01-VDS02 VDS 复制配置，如果不需要复制端口组，可以使用 `-WithoutPortGroups`。

## 列表 3.21 创建 VDS 副本

```powershell
$Datacenter = Get-Datacenter -Name 'PROD01'
$VDSwitch02 = Get-VDSwitch -Name 'PROD01-VDS02'
$VDSwitch02 | New-VSwitch -Name 'PROD01-VDS02-Copy' -Location $Datacenter -WithoutPortGroups
```

## 备份和恢复分布式交换机

VDS 模块包含的更多功能包括备份 DVS 配置并在后将文件恢复到 vCenter。

## 列表 3.22 备份交换机

```powershell
Get-VDSwitch -Name 'PROD01-VDS02' | Export-VDSwitch -Path "C:\Scripts\PROD01-VDS02.zip"
```

## 列表 3.23 恢复分布式交换机

```powershell
Import-VDSwitch -Name 'PROD01-VDS02' -Path "C:\Scripts\PROD01-VDS02.zip"
```

## 将 VM 移动到新端口组

常见的管理任务是将 VM 从一个端口组移动到另一个。可能存在背后的网络更改，涉及网络重新设计、VLAN 更改或可能的从标准交换机的迁移。`Move-VMToNewGroup` 函数接收源和目标端口组作为输入、源端口组中的每个 VM 并将其移动到新端口组（列表 3.24）。

## 列表 3.24 将 VM 从一个端口组移动到另一个

```powershell
function Move-VMToNewGroup {
    .SYNOPSIS
    将 VM 从一个端口组移动到另一个端口组。
    .DESCRIPTION
    将 VM 从一个端口组移动到另一个端口组。
    .PARAMETER Source
    要移动的端口组名称
    .PARAMETER Target
    要移动到的端口组名称
    .PARAMETER Cluster
    包含 VM 的集群名称
    .EXAMPLE
    Move-VMToNewGroup -Source PortGroup1 -Target PortGroup2 -Cluster Cluster01

    [CmdletBinding(SupportsProcess=$true)]
    Param(
        [parameter(Mandatory=$true, HelpMessage='要移动的端口组名称')]
        [ValidateNotNullOrEmpty()]
        [string]$Source,

        [parameter(Mandatory=$true, HelpMessage='要移动到的端口组名称')]
        [ValidateNotNullOrEmpty()]
        [string]$Target,

        [parameter(Mandatory=$false)]
        [ValidateNotNullOrEmpty()]
        [string]$Cluster
    )
    process {
        try {
            if ($Cluster) {
                Get-Cluster $Cluster | Get-VM | Get-NetworkAdapter |
                Where-Object {$_.NetworkName -eq $Source } |
                Set-NetworkAdapter -portgroup $Target -Confirm:$false
            } else {
                Get-VM | Get-NetworkAdapter |
                Where-Object {$_.NetworkName -eq $Source } |
                Set-NetworkAdapter -portgroup $Target -Confirm:$false
            }
        } catch [Exception] {
            throw "无法将 VM 移动到目标端口组"
        }
    }
}
```

