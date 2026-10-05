

# 附录 . 报告

```powershell
Where {$_.PowerState -eq "PoweredOn" |
Measure-Object -Property MemoryMB -Sum).Sum / 1024
$ObjCluster.MemUsagePct = "{0:p2}" -f
($Cluster.AssignedMemGB / $Cluster.TotalMemGB)
$ObjCluster
```

现在你已经检查了 Get-ClusterSummary 函数，让我们来试一下，看一眼生成的报告：

```
Get-Cluster CL02 | Get-ClusterSummary
```

ClusterName : CL02
NumHost : 3
NumVM : 48
NumDatastore : 13
NumNetwork : 15
AssignedCpu : 63
NumCores : 24
CpuPerCore : 2.63
TotalCPU : 64.08
TotalMemGB : 135.67
AssignedMemGB : 90.95
MemUsagePct : 67.04 %
```

为单个集群生成此报告很棒，但你的其他集群呢？将 Get-ClusterSummary 代码编写成函数的用处在于，你可以将其应用于任何喜欢的集群对象。要为所有集群生成报告，你只需从 Get-Cluster 命令行中删除集群名称，将它们全部放入管道即可：

```powershell
Get-Cluster | Get-ClusterSummary | Format-Table
```

| ClusterName | Host | NumVM | DatDat | NumNe | Assig | NumCo | vCPU | Total | CPUGB | MemGB |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| CL01 | 5 | 102 | 14 | 62 | 138 | 64 | 2.16 | 101.07 | 33.99 |
| CL02 | 3 | 48 | 13 | 15 | 63 | 24 | 2.63 | 64.08 | 135.67 |
| CL03 | 1 | 16 | 4 | 5 | 16 | 8 | 2.00 | 22.50 | 40.00 |
| CL04 | 2 | 24 | 3 | 14 | 28 | 16 | 1.75 | 44.99 | 111.99 |

注意，这里使用了 Format-Table 命令行以表格格式显示输出。所显示的输出也经过了编辑，以适应页面宽度的。

# 不一致的端口组 (Port Groups)

如果你正在使用标准交换机，那么确保集群中所有主机上的端口组定义是一致的至关重要。如果你没有做到这一点，可能会遇到虚拟机错误。A.7 中的函数将帮助你检测到命名不一致的端口组。

```powershell
LISTING A.7 Get-MissingPortGroup
```

```powershell
function Get-MissingPortgroup {
    SYNOPSIS
    获取集群中不一致的虚拟端口组
    .DESCRIPTION
    此函数会创建一个关于集群中不一致端口组的报告。它会报告在哪些主机上缺少了哪些端口组。
    .NOTES
    来源：Automating vSphere Administration
    作者：Luc Dekens, Brian Graf, Arnim van Lieshout, Jonathan Medd, Alan Renouf, Glenn Sizemore, Andrew Sullivan
    .PARAMETER Cluster
    要检查的集群对象
    .EXAMPLE
    Get-MissingPortGroup -Cluster (Get-Cluster CL01)
    .EXAMPLE
    Get-Cluster | Get-MissingPortGroup
}
```

```powershell
[parameter(ValueFromPipeline = $true, Mandatory = $true,
HelpMessage = "输入一个集群实体")]
[VMware.VimAutomation.Core.Impl.V1.Inventory.ClusterImpl]
$Cluster)
process{
```

```powershell
# 创建包含集群中所有可用端口组的数组
$clusterHosts = @($cluster | Get-VMHost)
$refPortGroups = @($clusterHosts | Get-VirtualPortGroup -Standard)
Select-Object -Unique
```

```powershell
# 将主机与引用数组进行对比
foreach ($vmHost in $clusterHosts) {
    $diffPortGroups = @($vmHost | Get-VirtualPortGroup -Standard)
    $differences = @(Compare-Object $refPortGroups \
    $diffPortGroups)
    foreach ($item in $differences) {
        $objPG = "" | Select-Cluster,HostName,MissingPortGroup
        $objPG.Cluster = $cluster
        $objPG.HostName = $vmHost.Name
        $objPG.MissingPortGroup = $item.InputObject
        $objPG
    }
}
```

现在让我们来看报告：

```
Get-Cluster CL02 | Get-MissingPortGroup

```

| Cluster | HostName | MissingPortGroup |
| :--- | :--- | :--- |
| CL02 | esx001.mydomain.local | Management Network |
| CL02 | esx003.mydomain.local | Management Network |
| CL02 | esx002.mydomain.local | VLAN02 |

注意，主机 esx001 和 esx003 都是 Management Network 组，而主机 esx002 不包含 VLAN02 组。

# 索引

读者注意：粗体页码表示主题的主要讨论。斜体页码表示插图。

## A

- 缩写参数，用于，500–501
- Add_Types.xml 文件，507
- ABR (基于数组的复制)，792
- 抽象，568
- Add From，214
- 访问规则，用于 vCloud 用户，668–670
- AccessLevel 参数，用于 New-Object
- AccessControlRule,688
- AccountEvent,596
- Action 属性，的 Alarm，588
- ActionFrequency，的 Alarm，587
- active，用于，589
- active events，615–617
- Active Mapping，在 View，387
- Active Directory 冲突，207–210
- 创建带有权限的虚拟属性，876
- 用户帐户，756–776
- 要求，757
- 脚本，761
- 以及 VirtualSession，846
- Add Member 命令行，412,415–508
- AddNamespace 命令行，389
- AddPath 命令行，338,397
- AddRestoreTemplate 命令行，391–392
- Add Script 向导，819–823,820
- Argument 类型，228
- Descriptor, 输出 Format，228
- Ready to Complete，823,829
- Script Body，822
- Script Identity，822,823,829
- Script Name, Description, 以及输出格式，821–822
- Add-SphereProtection 函数，797–799
- Add-SphereProtection 函数，HostingItem，877–878
- Add-Type 命令行，569
- Add-VBRRepository，394
- Add-VBR Backup 命令，395
- Add-VirtualCenter，388
- Add-VMHost 命令行，403
- Add-VMHostServer 命令行，669
- Add-VMHost 命令行，424
- Administrator Contact，98
- Administrator groups，用于托管，208
- 异步执行，898
- affinity 规则，190–194
- 应用于 Storage vMotion，310
- 聚合规则，542–547
- 列表任务，548
- 列出属性，588
- AlarmManager，586
- 警报，587–589
- active actions，588–592
- email 命令行，606
- 脚本代码，695
- 复杂指标，504
- 设计，587–610
- 表达式，589–590
- 触发机制，589
- SNMP trap 触发，627–628
- 获取 元素，615–617
- 修改，612
- 移动，611–615
- schema 类型，588
- 事件警报，590–596
- 通用警报创建函数，605–610
- 指标警报，597
- 状态警报，597
- vCenterAlarms PowerShell模块，自定义属性警报，609–610
- 客户网络连接，608–609
- 使用 CPU 代码，607–608
- AlarmSnmpFailed，628
- 警报触发，595
- AllUsers，用于 Set PowerConfiguration 参数，698
- 算法排序，506
- AndExpression，589
- antiHostGroupName，193
- Apache Fusion，833–834
- 添加注释，837
- 证书验证，835
- 自动化虚拟机服务器，870
- 项目结构创建，850–851
- 同义词仓库创建，843–854
- 添加代码，854–855
- 检查更改，861–862
- 项目检出，851–853
- 移除代码，865–867
- 滚回更改，865–867
- 使用代码，851–860
- 用户和组，846
- VirtualSrm Server，843–844
- 安装，844
- VirtualSrm server Web 接口，870
- API 参考文档，关于事件，590
- API 任务，在 vCloud 应用服务器中，708–710

# 应用 - 命令行

applications
- Dell，387–392
- CHAP (挑战握手验证协议)，121
- Vmeer，382–396
- (MAC) 地址，273
- 从 DIY恢复虚拟机，CheckMigrate_Task，vSphere 多线程，多个 CPU 用于，268
381–382
- 参考，630
- 参数字符串，6
- 与快照，323
- 检出对话框，851,852
- 基于数组的隔离 (ABR)，792
- 任务模板，395
- 在 TortoiseSVN 中的检查点
- 权限数组，25
- 差异备份，401
851–853
- Assertion-HardeningGUIDExIASetting
of Server Center，398
- CheckCompliance_Task，656
- 异步，451–455
- 全备备份，399
- 失败错误参数，657
- 日志备份，401
- CheckRelocate_Task，631

