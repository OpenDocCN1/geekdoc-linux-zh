
# 理解基础概念

| | | |
|---|---|---|
| 390 利用率 | cpu | 平均值 |
| 391 利用率 | cpu | 最大值 |
| 392 利用率 | cpu | 最小值 |
| 397 消耗 | cpu | 总和 |

## 实例 (Instances)

在显示一些示例之前，这是最后一个我们要介绍的概念。实例的官方定义源自 vSphere API：它是与指标关联的标识符。

让我们尝试通过示例让它变得更容易理解。。

对于 CPU 相关的指标，如果主机配备了四核 CPU，那么每个 CPU 相关指标会有四个实例：0、1、2 和 3。在这种情况下，还有一个额外的实例，被称为“聚合（aggregate）”，它是所有其他实例的平均值。

每个实例都有一个唯一的标识符，包含在返回的统计数据中。如果你想列出特定实体的可用实例，可以使用 `QueryAvailablePerfMetric` 方法，如列表 16.8 所示。

```powershell
function Get-StatInstance {
  .SYNOPSIS
  返回特定指标和实体的可用实例
  .DESCRIPTION
  该函数返回实体的所有可用实例。实体可以是 ESXi 主机、集群、资源池或虚拟机。
  .PARAMETER Entity
  要返回实例的实体或实体。
  .PARAMETER Stat
  要返回实例的指标或指标。
  .PARAMETER Realtime
}
```

![](img/62596f5acc97904608ae511beb7d6_0.png)

# 第 IV 部分 第 16 章 使用统计数据

使用切换来选择实时指标

.示例
```powershell
Get-StatInstance -Entity (Get-VM 'Guest1') \
>> -Stat "cpu.usage.average"
```

.示例
```powershell
Get-StatInstance -Entity esx -Stat 'cpu.usage.average' \
>> -Realtime
```

.示例
```powershell
Get-VMHost MyExS | Get-StatInstance \
>> -Stat 'disk.devicelency.average'
```

```powershell
[CmdletBinding()]
Param(
    [parameter(ValueFromPipeline = $true, Mandatory = $true, HelpMessage = '输入实体')]
    [PObject]$Entity,
    [parameter(Mandatory=$true, HelpMessage = '输入指标')]
    [string[]]$Stat,
    [switch]$Realtime
)
```

```powershell
begin{
    # 创建性能计数器 hasht表
    $si = Get-View ServiceInstance
    $perfMgr = Get-View $si.content.PerfManager
    $pTable = New-Object Hashtable
    foreach($pC in $perfMgr.PerfCounter){
        if($pC.Level -ne 99) {
            $pKeyComponents = $pC.GroupInfo.Key,
            $pC.NameInfo.Key,
            $pC.RollupType
            $pKey = $pKeyComponents -join '.'
            $pKey = $pKey.ToLower()
            if(!$ptable.ContainsKey($pKey)){
                $ptable.Add($pKey,$pC.Key)
            }
        }
    }
}
```

# 理解基础概念 563

```powershell
process{
    $entSDK = $entity | Get-View
}

# 处理 Realtime 切换
$numinterval = $null
if($Realtime) {
    $provsum = $perfMgr.QueryPerfProviderSummary($entSDK.MoreRef)
    $numinterval = $provsum.refreshRate
}

# 获取实体的指标
entSDK | Foreach-Object {
    $metrics += $perfMgr.QueryAvailablePerfMetric($_.MoreRef,
    null,
    null,
    $numinterval)
}

# 检查 stat 是否有效
foreach($st in $stat){
  if($pcTable.ContainsKey($st.ToLower())){
    Throw "-Stat 参数 $st 无。"
  }
  else{
    $ids += $pcTable[$st]
  }
  foreach($metric in $metrics){
    if($metric.CounterId -eq $pcTable[$st.ToLower()]){
      $obj = [ordered]{
        StatName = $st
        Instance = $metric.Instance
      }
      New-Object PSObject -Property $obj
    }
  }
}
end()
```

![](img/62596f5acc97904608ae511beb7d6_592_0.png)

使用 `QueryAvailablePerfMetric` 方法来列出特定实体的可用实例，如列表 16.8 所示。

