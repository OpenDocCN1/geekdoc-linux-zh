
### 3.1 托管网络信息

| ID | PNIC | Speed | MAC | DeviceID | Observed | IP Range | VLAN |
|---|---|---|---|---|---|---|---|
| 1 | vmx2 | 1000 | 00:52:56:8a:c2 | Cisco | GuestEthernet/7 | 192.168.0.1-192.168.0.254 | 101 |
| 2 | vmx2 | 1000 | 00:52:56:8a:c7 | Cisco | GuestEthernet/10 | 192.168.10.0-192.168.10.254 | 100 |
| 3 | vmx2 | 1000 | 00:52:56:8a:c7 | Cisco | GuestEthernet/2 | 192.168.2.0-192.168.2.254 | 110 |
| 4 | vmx2 | 1000 | 00:54:77:fb:65 | Cisco | GuestEthernet/9 | 192.168.15.0-192.168.15.254 | 210 |
| 5 | vmx2 | 1000 | 00:54:77:fb:67 | Cisco | GuestEthernet/10 | 192.168.20.0-192.168.20.254 | 220 |
| 6 | vmx2 | 1000 | 00:54:77:fb:68 | Cisco | GuestEthernet/15 | 192.168.25.0-192.168.25.254 | 220 |

现在你知道哪些 NIC 应该分配给虚拟交换机，是时候开始交换机了。默认情况下，ESXi 的安装会在与管理 NIC 相同的虚拟交换机上创建一个虚拟端口组。由于你有用于虚拟流量的 NIC，让我们使用它。使用 `Get-VirtualSwitch` 命令检索默认虚拟交换机，使用 `Get-VirtualPortGroup` 命令识别默认虚拟机网络端口组，并使用 `Remove-VirtualPortGroup` 将其删除（列表 3.3）。

### 3.3 移除默认虚拟机网络端口组

```powershell
Get-VirtualSwitch -VMHost vesxi105* -Name vSwitch0 |
Get-VirtualPortGroup -Name "VM Network" |
Remove-VirtualPortGroup -Confirm:$false
```

现在让我们创建一个新的虚拟机虚拟交换机。在列表 3.4 中，我们将交换机分配给 `vmnic4` 和 `vmnic5`，之前之前之前分配给此虚拟交换机的。

### 列表 3.4 创建新的虚拟交换机

```powershell
$vSwitch = New-VirtualSwitch -VMHost vesxi05* -Name "vSwitch" -Nic vmnic4,vmnic5
```

> 提示：我们在上一个示例中使用的技术（存储交互式命令的结果）是在命令行外壳工作时节省时间的好方法。与其反复输入命令来处理同一个对象，你可以返回该对象并存储在易于访问的变量中。

### 列表 3.5 创建新的端口组

```powershell
New-VirtualPortGroup -VirtualSwitch vSwitch -Name VM220 -VlanID 220
```

除了用于虚拟机的虚拟交换机和端口组外，你可能还需要创建 VMkernel 端口组以用于 vMotion 或容错等技术。如之前所述，VMkernel 端口组也是 iSCSI 或 NFS 存储的要求。

让我们为 vMotion 创建一个 VMkernel 端口组；我们将将其创建为 `vSwitch0` 的额外端口组（在下一节查看交换机和端口组时将看到这一点）。

### 列表 3.6 创建 VMkernel 端口组

```powershell
$vSwitch0 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch0"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "vMotion" \
-VirtualSwitch $vSwitch0 \
-IP 192.168.1.10 \
-SubnetMask 255.255.255.0 \
-VMotionEnabled=$true
```

希望在你的环境中，将使用独立的 VLAN 用于 vMotion 网络流量。要为你已创建的 vMotion 端口组配置 VLAN，请使用 `Set-VirtualPortGroup` 命令（列表 3.7）。

### 列表 3.7 为 vMotion 端口组配置 VLAN

```powershell
$vMotionPG = Get-VirtualPortgroup -VMHost vesxi05* -Name vMotion
Set-VirtualPortGroup -VirtualPortGroup $vMotionPG -VlanId 101
```

为基于 IP 的存储创建 VMkernel 端口组的过程几乎相同。只需从用于创建 vMotion 端口组的命令中删除 `-VMotionEnabled` 参数（列表 3.8）。

### 列表 3.8 为基于 IP 的存储创建 VMkernel 端口组

```powershell
$vSwitch1 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch1"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "iSCSI" \
-VirtualSwitch $vSwitch1 \
-IP 192.168.20.50 \
-SubnetMask 255.255.255.0

$iSCIPG = Get-VirtualPortgroup -VMHost vesxi05* -Name iSCSI
Set-VirtualPortGroup -VirtualPortGroup $iSCIPG -VlanId 200
```

> 注意：ESXI 默认有一个 VMkernel 端口组；安装期间创建的管理网络就是一个 VMkernel 端口组。虽然这可以用于测试或低使用率目的连接 iSCSI 或 NFS 存储，但我们建议在生产环境中使用此配置。通常，良好的设计应具有用于网络存储的专用网卡。

![](img/62596f5acc979040608a4e5111beb7d6_113_0.png)

### 使你的交换机和端口组具有韧性

在上一节课程中，你创建了一个 vMotion 端口组。你将其添加到现有的 `vSwitch0` 中，该交换机已经托管管理网络端口组并分配了一个网卡 `vmnic`。显然，作为一名优秀的 IT 专业人员，你需要一个应对出现问题情况的计划。对于这种情况，更好的做法是为交换机添加额外的网卡以增强韧性。更好的办法是将 `vmnic` 配置为管理网络的活动适配器和 vMotion 网络的备用适配器，反之亦然。

`Set-ManagementAndMotionResilient` 函数接收主机、管理网络和 vMotion 网络名称以及使用的网卡作为输入，然后将第一个网卡设置为管理网络的活动适配器和 vMotion 网络的备用适配器，第二个网卡反之亦然（列表 3.9）。

### 列表 3.9 为管理和 vMotion 端口组添加韧性

```powershell
function Set-ManagementAndMotionResilient {

<SYNOPSIS
    为管理和 vMotion 端口组添加韧性。

  .DESCRIPTION
    为管理和 vMotion 端口组添加韧性。

  .PARAMETER VMHost
    要配置的主机名称

  .PARAMETER Management
    管理网络端口组名称

  .PARAMETER vMotion
    vMotion 端口组名称

  .PARAMETER NIC0
    使用的第一个网卡名称

  .PARAMETER NIC1
    使用的第二个网卡名称

  .EXAMPLE
    Set-ManagementAndMotionResilient -VMHost Server01 -Management 'Management Network' -vMotion vMotion -NIC0 vmnic -NIC1 vmnic

  .EXAMPLE
    Get-VMHost Server01,Server02 | Set-ManagementAndMotionResilient -Management 'Management Network' -vMotion vMotion -NIC0 vnic0 -NIC1 vmnic
```
