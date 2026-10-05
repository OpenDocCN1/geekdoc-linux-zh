
（列表 5.10）、一个 VM 组（列表 5.11），最后是这两个组的亲和性规则（列表 5.12）。

# 列表 5.10 New-DrsHostGroup 函数

```
function New-DrsHostGroup {
  < .SYNOPSIS
  创建一个 DRS 主机组。

  .DESCRIPTION
  在指定的集群中创建一个 DRS 主机组，使用
  一个或多个 VM 主机作为成员。

  .EXAMPLE
  使用特定主机创建一个组
  New-DrsHostGroup -Cluster clusterName -VMhost1,host2 `
  -GroupName MyGroup

  .EXAMPLE
  使用管道为新的 DRS 组指定集群
  Get-Cluster clusterName | New-DrsHostGroup -VMhost1,host2 `
  -GroupName MyGroup

  .PARAMETER Cluster
  [System.String]
  要创建组的集群名称。

  .PARAMETER VMHost
  [System.String[]]
  要放入新创建组中的主机数组。

  .PARAMETER GroupName
  [System.String]
  新组的名称。

  .INPUTS
  [VMware.VimAutomation.ViCore.Impl.V1.Inventory.Cluster]
```

#>
[CmdletBinding()]
param(
    [parameter(
        Mandatory=$true
```

```
[parameter (Mandatory=$true)]
[String[]]
$VMHost,
```

```
[parameter (Mandatory=$true)]
[String]
$GroupName
```

```
$clusterObj = Get-Cluster -Name $Cluster
$clusterSpec = New-Object VMware.Vim.ClusterConfigSpecEx
$hostGroup = New-Object VMware.Vim.ClusterGroup
```

```
# 添加、编辑或删除 DRS 组
$hostGroup.operation = "add"
```

```
# 指定这是一个主机组
$hostGroup.Info = New-Object VMware.Vim.ClusterHostGroup
```

```
# 给它命名
$hostGroup.Info.Name = $groupName
```

# 添加主机的 MoRefs

```
$VMHost | Foreach-Object {

    $hostGroup.Info.Host += (Get-VMHost $_).Id
}
```

# 将组添加到集群设置规范中
$clusterSpec.GroupSpec += $hostGroup

# 执行重新配置方法
$clusterObj.ExtensionData.ReconfigureComputeResource(

```
# 提供上面创建的规范
$clusterSpec,
```

```
# 设置为 true 以更新集群，设置为 false
# 则取消集群的配置，除了作为此规范
# 部分设置的内容以外的所有设置
$true
```

此函数用于创建 DRS 组。然而，它可以通过修改第 31 行，将 `$hostGroup.operation- "add"` 改为 `$hostGroup.operation = "edit"` 或 `$hostGroup.operation = "remove"`，来轻松地编辑或删除现有的组。这种指定需要执行的操作类型的简单能力，在 VMware SDK 使用的许多规范任务中都是通用的。

请注意，ReconfigureComputeResource 方法调用的第二个参数（除配置规范之外的布尔选项）非常重要。它指定了我们正在更新集群的配置。如果没有它，我们规范中未提供的任何设置都将被取消，这可能会导致非常糟糕的后果！

# 列表 5.11 New-DrsVmGroup 函数

```
function New-DrsVmGroup {
    .SYNOPSIS
    <#
创建一个 DRS 虚拟机组。

    .DESCRIPTION
```

在指定的集群中创建一个 DRS 虚拟机组，使用
一个或多个 VM 作为成员。

```
.EXAMPLE
使用特定 VM 创建一个组
New-DrsVmGroup -Cluster clusterName -VM vm1,vm2 \
-GroupName MyVMGroup
```

```
.EXAMPLE
使用管道为新的 DRS 组指定集群
Get-Cluster clusterName | New-DrsVmGroup -VM vm1,vm2 `
-GroupName MyVMGroup
```

```
.PARAMETER Cluster
[System.String]
要创建组的集群名称。
```

```
.PARAMETER VM
[System.String[]]
要放入新创建组中的 VM 数组。
```

```
.PARAMETER GroupName
[System.String]
新组的名称。
```

```
.INPUTS
[Vmware.VimAutomation.ViCore.Impl.V1.Inventory.ClusterImpl]
```

```
#>
[CmdletBinding()]
param(
    [parameter(
        Mandatory=$true,
        ValueFromPipelinePropertyName=$true
    )]
    [Alias('Name')]
    [String]
    $Cluster
)
```

```
[parameter (Mandatory=$true)]
[String []]
$VM
```

```
[parameter (Mandatory=$true)]
[String]
$GroupName
```

```
$clusterObj = Get-Cluster -Name $Cluster
```

```
$clusterSpec = New-Object VMware.Vim.ClusterConfigSpecEx
```

```
$vmGroup = New-Object VMware.Vim.ClusterGroupSpec
```

```
# 添加、编辑或删除 VM 组
$vmGroup.operation = "add"
```

```
# 指定这是一个 VM 组
$vmGroup.Info = New-Object VMware.Vim.ClusterVmGroup
```

```
# 给它命名
$vmGroup.Info.Name = $GroupName
```

```
# 将 VM 添加到组
$VM | Foreach-Object {
vmGroup.Info.VM += (Get-VM $_).id
}
```

```
# 将 VM 组添加到集群规范中
$clusterSpec.GroupSpec += $vmGroup
```

```
# 执行集群重新配置
$clusterObj.ExtensionData.ReconfigureComputeResource(
# 提供规范
$clusterSpec,
```

```
# 更新集群配置
$true

```

此函数与创建主机组的函数几乎相同，并且具有相同的修改能力，可以编辑或删除 VM 组。下一个函数位于列表 5.12 中，用于通过将使用先函数创建的虚拟机组和主机组与创建规则集的逻辑相结合，来设置组亲和性。

# 列表 5.12 New-DrsGroupAffinity 函数

```
function New-DrsGroupAffinity {
  <# SYNOPSIS
  为 VM 和主机组创建 DRS 亲和性规则。

  .DESCRIPTION
在指定的集群中使用主机组和 VM 组作为成员创建一个 DRS 亲和组。如果 mandatory 为 false，则该规则是“应该”规则，否则它是“必须”规则。

  .EXAMPLE
  创建一个强制性组
  Get-Cluster clusterName | New-DrsGroupAffinity -HostGroup MyGroup -VmGroup MyGroup -RuleName MyRule

  .PARAMETER Cluster
[System.String]
要创建组的集群名称。

.PARAMETER HostGroup
[String[]]
要添加到规则的主机组名称。

  .PARAMETER VmGroup
[System.String]
要添加到规则的 VM 组名称。

  .PARAMETER RuleName
[System.String]
规则的名称。

  .PARAMETER Mandatory
[Boolean]
如果为 true，规则为“必须”，否则为“应该”

  .INPUTS
[Vmware.VimAutomation.ViCore.Impl.V1.Inventory.Cluster]
```

#>
[CmdletBinding()]
param(
    [parameter(
        Mandatory=$true,
        ValueFromPipelinePropertyName=$true
    )]
    [Alias('Name')]
    [String]
    $Cluster
,
    [parameter (Mandatory=$true)]
    [String []]
    $HostGroup,
,
    [parameter (Mandatory=$true)]
    [String]
    $VmGroup,
,
    [parameter (Mandatory=$true)]
    [String]
    $RuleName,
,
    [parameter (Mandatory=$false)]
    [Boolean]
    $Mandatory = $false
)

$clusterObj = Get-Cluster -Name $Cluster
$clusterSpec = New-Object VMware.Vim.ClusterConfigSpecEx
$rule = New-Object VMware.Vim.ClusterRuleSpec

# 添加、编辑、删除规则
$rule.operation = "add"

# 此对象的类型决定了创建的规则类型：
# ClusterHostRuleInfo = VM(s) 对主机的（反）亲和
# ClusterAffinityRuleSpec = VM 聚合
# ClusterAntiAffinityRuleSpec = VM 分离

$rule.Info = New-Object VMware.Vim.ClusterRuleInfo

# 启用或禁用规则
$rule.Info.enabled = $true

# 名称
$rule.Info.name = $RuleName

# 根据规则类型具有不同的含义
# 对于 ClusterHostRuleInfo：
# 将强制 设置为 false 等于“应该”
# 将强制 设置为 true 等于“必须”
# 对于 VM 亲和性和反亲和性规则：
# 如果规则被违反，设置为 true 将阻止 VM 启动
# 如果设置为 false，将允许 VM 启动且 DRS 将尝试保持规则生效
$rule.Info.mandatory = $Mandatory

# VM 组的名称
$rule.Info.vmGroupName = $VmGroup

# 如果我们想让 VM 留在指定的主机上，使用亲和组
$rule.Info.affineHostGroupName = $HostGroup

# 或者，为了让 VM 离开指定的主机，使用反亲和性组
$rule.Info.antiAffineHostGroupName = $HostGroup

# 将我们的规则添加到集群规范中
$clusterSpec.RulesSpec += $rule

# 执行集群重新配置
$clusterObj.ExtensionData.ReconfigureComputeResource(
# 提供规范
$clusterSpec,

# 更新集群配置
$true
```

# 列表 5.13 使用 DRS 组强制亲和性

```
Get-Cluster $clustername | \
New-DrsHostGroup -GroupName $hostGroup \
-VMHost $host1,$host2
```

