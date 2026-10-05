

# 获取统计数据

| 实体 | 属性 | VMW.VimAutomation.Types.VIOject E... |
| --- | --- | --- |
| EntityID | 属性 | System.String EntityID {get}; |
| Instance | 属性 | System.String Instance {get;set;}; |
| IntervalSecs | 属性 | System.Int32 IntervalSecs {get;set;}; |
| MetricID | 属性 | System.String MetricID {get;set;}; |
| Timestamp | 属性 | System.DateTime Timestamp {get;set;}; |
| Uid | 属性 | string Uid {get}; |
| Unit | 属性 | System.String Unit {get;set;}; |
| Value | 属性 | System.Single Value {get}; |

这些属性大部分是自解释的，并使用了 string、int32 或 DateTime 等基本类型。例外是 Entity 属性。该属性包含了实际的自动化对象——也就是说， Get-VM 或 Get-VMHost 词程序返回的对象。如果你需要包含实体的某些属性，这种行为在你的报告脚本中非常有用。

# 了解使用哪些指标

现在你已经按照希望设置好了一切，是时候开始生成报告了。你将遇到的第一个问题是为报告选择指标。鉴于 vSphere 中可用指标数量巨大，本书将不会详细描述可用可用或何时使用特定指标。Get-StatReference 函数可能对你有所帮助。该函数会创建一个 HTML 页面，其中包含你所连接的 vCenter Server 上所有可用指标。由于你可以轻松地重新创建此页面，你始终可以访问最新的指标列表。16.11 包含了 Get-StatReference 函数。

# 16.11 Get-StatReference 函数

```
function Get-StatReference {
#
.SYNOPSIS
创建所有可用指标的 HTML 参考
.DESCRIPTION
该函数返回一个简单的 HTML 页面，包含你所连接的环境中的所有可用指标。
.EXAMPLE
Get-StatReference | Out-File "$env:temp\metricRef.html"
#>
```

![](img/62596f5acc979040608a4e5111beb7d6_598_0.png)

第四部分

# 第 16 章 • 使用统计数据

```
Begin{
# 在 API 4.0 中有一个 bug。
# 有 4 个重复的指标，仅在大小写上不同
# 这些指标通过 -notcontains 条件被排除

$badMetrics = ' .management.reservedcapacity.average',
  'cpu.reservedcapacity.average',
  'managementAgent.swapin.average',
  'managementAgent.swapout.average'
$si = Get-View ServiceInstance
$perfMgr = Get-View $si.content.perfManager
}
```

```
Process{
# 创建性能计数器哈希表
$metricRef = foreach($pC in $perfMgr.PerfCounter) {
if($pC.Level -ne 99) {
    $pKeyComponents = $pC.GroupInfo.Key,
    $pC.NameInfo.Key,
    $pC.Rolloutype
    $pCKey = $pKeyComponents -join '.'
    if ($badMetrics -notcontains $pCKey) {
      $pCKey = $pC.Key.ToLower()
      New-Object PSCject @{
        Metric = $pCKey
        Level = $pC.Level
        Unit = $pC.UnitInfo.Label
        Description = $pC.NameInfo.Summary
      }
    }
  }
}
End{
$metricRef | Sort-Object -Property Metric | `
ConvertTo-Html -Property Metric,Level,Unit,Description
}
```

你按照如下方式生成 HTML 页面：

```
Get-StatReference | Out-File metricRef.html
```

Stats Toolbox 是探索指标的替代方案：

www.lucd.info/2014/09/02/stats-toolbox/

此 PowerShell 脚本提供了一个带有若干功能的 GUI 接口，用于处理 vSphere 性能指标、在 VMTN Communities 中搜索指标并生成基于 Get-Stat 的代码。

除了 VMware 文档外，还有几个来源可以让你学习什么情况下应该使用什么指标。VMTN 上的 Performance 社区是一个很好的起点。

# 技术

在处理统计数据时，你会经常使用一些技术（例如定义正确的时间范围、选择正确的间隔等）。花点时间练习这些技术是值得的。

# 使用正确的范围

-Start 和 -Finish 参数决定了你想要检索统计数据的时间段。简单的方法是传递一个字符串，按格式指定日期和时间。

```
Get-Stat -Entity (Get-VMHost) |
>> Select-First 1 -Stat 'mem.usage.average' `
>> -Start '06/21/2015 17:15:20' -Finish '06/21/2015 17:16:00'
```

| MetricID | Timestamp | Value Unit |
|---|---|---|
| mem.usage.average | 6/21/2015 17:16:00 PM | 18.05 % |
| mem.usage.average | 6/21/2015 17:15:40 PM | 18.05 % |
| mem.usage.average | 6/21/2015 17:15:20 PM | 18.05 % |

格式取决于运行 Get-Stat 词程序的工作站区域设置。你可以使用 Get-Culture 词程序检查时间使用的格式。秒数可以省略。

```
(Get-Culture).DateTime.ShortDateFormat
M/d/yyyy
```

```
(Get-Culture).DateTime.ShortTimeFormat
h:mm
```

下次运行 Get-Stat 词程序是在 en-GB 设置的系统上。注意日期部分的格式不同：

```
Get-Stat -Entity (Get-VMHost) |
>> Select-First 1 -Stat 'mem.usage.average' `
>> -Start '21/06/2015 17:15' -Finish '21/06/2015 17:16'
```

| MetricID | Timestamp | Value Unit |
|---|---|---|
| mem.usage.average | 21/06/2015 17:16:00 | 9.46 % |
| mem.usage.average | 21/06/2015 17:15:40 | 9.46 % |
| mem.usage.average | 21/06/2015 17:15:20 | 9.46 % |

来自 .NET Framework 的 DateTime 构造函数非常便于使用变量创建 DateTime 对象。注意你如何使用 Get-Date 词程序返回的特定属性来填充变量。

```
$year = (Get-Date).Year
$day = 21
$hour = 18
New-Object DateTime($year,$day,$hour,30,0)
```

2015年5月21日 下午 6:30

你可以以类似的方式使用 Get-Date 词程序及其参数：

```
Get-Date -Year $year -Day $day -Hour $hour
```

2015年6月21日 下午 6:35

# 选择正确的间隔

一个经常被忽略的点是你在计算中需要包含哪些间隔。假设你想生成一个从 17:50 到 18:00 的报告，并且必须使用实时数据。你需要包含哪些间隔？

为了回答这个问题，首先需要理解 Timestamp 属性。时间戳提供的是时间间隔的开始时间，还是间隔中间某个值？

根据 SDK 参考，Timestamp 代表“采集样本的时间”。因此，对于我们的示例，我们不需要时间戳为 17:50 的间隔，因为它包含了从 17:49:40 到 17:50:00 的测量数据。我们将使用的第一个间隔时间戳是 17:50:20。请求的间隔是什么？我们需要在时间戳为 18:00:00 的数据停止，因为那是从 17:59:40 到 18:00:00 的间隔。这是一个我们以后会提到的重要概念。

# 时间范围脚本

当你编写统计报告脚本时，不想使用硬编码的日期和时间。幸运的是，PowerShell 在 DateTime 类型上提供了多种方法和属性，获取循环时间范围所需的 -Start 和 -Finish 参数非常有帮助。掌握了这些知识，你会发现通过列表 16.12 自己编写很容易。

列表 16.12 编写循环时间范围

# 从午夜到现在的

```
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$Start = $todayMidnight.AddSeconds(1)
$Finish = Get-Date
```

![](img/62596f5acc979040608a4e5111beb7d6_602_0.png)

# 昨天

```
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$Start = $todayMidnight.AddDays(-1).AddSeconds(1)
$Finish = $todayMidnight
```

# 前天

```
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$Start = $todayMidnight.AddDays(-2).AddSeconds(1)
$Finish = $todayMidnight.AddDays(-1)
```

# 上周

```
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$endWeek = $todayMidnight.DayOfWeek.value
AddDays(-$todayMidnight.DayOfWeek.value +1)
$Start = $endWeek.AddDays(-7).AddSeconds(1)
$Finish = $endWeek
```

# “x个月前”

```
$monthsBack = <number-of-months-back>
$todayMidnight = (Get-Date -Hour 0 -Minute 0 -Second 0)
$xMonthsAgoMidnight = $todayMidnight.AddMonths(-$monthsBack + 1)
$endOfMonth = $xMonthsAgoMidnight.*
AddDays(-$xMonthsAgoMidnight.Day)
$Start = $endOfMonth.AddDays(-1).AddSeconds(1)
$Finish = $endOfMonth
```

# 数据分组

当你收集数据时，一个重要的效率技巧是使用 Group-Object 词程序。该词程序提供了许多功能，应该在你的 PowerShell 工具箱中。

# 单个属性

16.13 中的脚本展示了如何使用分组为单个服务器生成报告。这个简单的示例生成了一份报告，显示特定 ESXi 服务器上每个物理适配器（pNIC）在前一天的平均速率。在这种情况下，Instance 属性被用于分组。通过过滤掉 Instance 属性为空字符串的组，可以跳过聚合数据。

