
一旦 `escli` 命令完成转换，你可能想要将其封装进 PowerShell 函数中，类似于 `Get-VMHostCSIBinding` 和 `Set-VMHostCSIBinding` 函数，使其更像是一个原生的 PowerShell 命令。

## 设置多路径策略

如果你在使用光纤通道（Fibre Channel SAN），尽可能对 SAN 使用多个 HBA 连接是一项良好实践。在具有多个 HBA 连接的情况下，如果通往 SAN 的活动路径故障，另一个被动路径将激活，从而确保存储流量持续且虚拟机保持连接。如果存储阵支持，vSphere 可以简单地使用活动/多路径模式而非活动/被动路径模式。这意味着你不仅在路径故障时具有韧性，还能通过使用多路径访问存储来提升存储性能。原生多路径插件（NMP）模块与存储阵类型插件（SATP）以及路径选择插件（PSP）通信以实现这些多路径功能。

> 在继续之前，请联系你的存储供应商了解在 ESXi 上使用哪些 SATP 和 PSP。

假设你的存储阵支持多路径且你已选择了正确的 SATP，你需要在需要多路径的 LUN 上配置 PSP。PSP 是针对每个 LUN的，可以取三个值：`Fixed`、`MostRecentlyUsed` 或 `RoundRobin`。你可以使用混合选择，建议查看当前正在使用哪种。要实现这一点，你可以使用 `Get-ScsLun` 命令并选择 `MultipathPolicy` 属性。

```
Get-VMHost vsxi05* | Get-ScsLun | Select CanonicalName, MultipathPolicy
```

| CanonicalName | MultipathPolicy |
| --- | --- |
| mpx.vmhba32:C0:L0 | Fixed |
| naa.600616019a93408059cb52a22 | MostRecentlyUsed |
| naa.600016019a34003a8ef2239ca22 | MostRecentlyUsed |
| aa.600016019a3400185f0486a22 | MostRecentlyUsed |

通常光纤通道 SAN，你将与多个 LUN 进行交互，而像上一个示例那样只有三个。即使通过 GUI 将 PSP 更改为 `RoundRobin` 也会变得繁琐，因此通过 PowerCLI 使用可以节省大量时间。通过 `Set-StorageLun` 命令的 `-MultipathPolicy` 参数，你可以一行代码完成跨光纤通道 LUN 的更改。你还可以使用 `Where-Object` 来过滤非光纤通道 LUN，正如我们在示例 4.13 中做的那样。

### 示例 4.13 为多个 LUN 设置多路径策略

```
Get-VMHost vesxi05* | Get-ScsLun | Where-Object {$_.CanonicalName -like 'naa.*'} | Set-StorageLun -MultipathPolicy "RoundRobin"
```

## 一旦 LUN 更新了正确的 PSP，你可能希望更新默认 SATP，以便未来添加的任何 LUN 在创建时就是正确的。

![](img/62596facc979040608a4e511beb7d6_173.png)

> 注意：示例 4.13 中通过 `Set-StorageLun` 显式设置多路径策略的另一种方法是设置默认 PSP（正如我们将演示的），将主机放入维护模式并重启。这种方法的优势在于，如果将来需要更改默认 PSP，只需重启将 LUN 更改为新的 PSP。

我们可以通过书中前面提到的 `Get-Cli` 方法来实现这一点。示例 4.14 展示了如何将 SATP `VMW_SATUA` 的默认 PSP 设置为 `RoundRobin (VMW_PSP_RR)`。

### 示例 4.14 为 SATP 设置默认 PSP

```
$DefaultPSP = 'VMW_PSP_RR'
$SATP = 'VMW_SATUA'
$EsxCli = Get-Cli -VMHost vesxi05*
$EsxCli.storage.nmp.satp.set($null,$DefaultPSP,$SATP)
```

存储 I/O 控制（SIOC）使用数据存储上所有虚拟磁盘的平均延迟来计算延迟。该平均值根据每秒操作次数（IOPS）加权。当此平均延迟超过配置阈值时，SIOC 通过调整设备队列来限制吞吐量。因此，SIOC 只在拥塞运行时。

自本书第一版以来，SIOC 发生了显著变化。首先，从 vSphere 5.0 开始支持 NFS 数据存储；所有基于协议的数据存储都可以开启 SIOC。其次，PowerCLI 5.0 在 `Set-Datastore` 命令中增加了 `StorageIOControlEnabled` 参数。因此，本书第一版中描述的 SIOC 函数不再需要了。在数据存储上启用 SIOC 不需要预检查，可以使用简单的单行命令（示例 4.15）。

### 示例 4.15 在数据存储上启用 SIOC

```bash
Set-Datastore -Datastore ISCI01 -StorageIOControlEnabled=$true
Select-Object Name, StorageIOControl



数据存储集群在 vSphere 5 中引入，允许将单个数据存储分组为逻辑集群以便于管理。结合分布式资源调度程序（SDRS），现在 vCenter 可以以类似于虚拟机的方式管理数据存储。凭借可用空间和存储性能统计，vCenter 能够在数据存储集群内部迁移虚拟机以提高资源利用率。

PowerCLI 在 5.1 版本引入了对数据存储集群的支持。示例 4.16 展示了如何创建数据存储集群。

### 示例 4.16 创建数据存储集群

```bash
New-DatastoreCluster -Name DatastoreCluster -Location Prod
```

在创建时只能指定名称和位置。要配置一些有趣的设置（例如 SDRS 和 I/O 指标），你必须使用 `Set-Datastore` 命令。示例 4.17 展示了如何开启全自动、10ms 延迟阈值和 90% 空间利用率 SDRS。

### 示例 4.17 在数据存储上启用 SDRS 和 I/O 指标

```bash
Set-Datastore -DatastoreCluster Datastore1 -AutomationLevel FullyAutomated -SIOC=$true -OLatencyThreshold 10 -SpaceUtilizationThreshold 90
```

> 注意：当 Storage DRS 自动化级别设置为全自动时，你不需要指定 `Set-Datastore` 的 `EvacuateAutomatically` 参数，因为 Storage DRS 将自动迁移所有机器。

现在按照要求配置好了数据存储集群，你需要向其中填充数据存储。在示例 4.18 中，我们添加了三个。

### 示例 4.18 将数据存储加入集群

```bash
$DatastoreCluster = Get-DatastoreCluster Datastore1
Get-Datastore | Move-Datastore -Destination $DatastoreCluster
```

> 提示：有关如何在 PowerShell 中使用通配符的更多信息，请输入 `help about_wildcards`。

集群中的数据存储具有维护模式功能，可以无中断地从该数据存储迁移虚拟机。这类似于将 ESXi 主机放入维护模式（示例 4.19）。

### 示例 4.19 将数据存储设置为维护模式

```bash
Set-Datastore -MaintenanceMode=$true
```
