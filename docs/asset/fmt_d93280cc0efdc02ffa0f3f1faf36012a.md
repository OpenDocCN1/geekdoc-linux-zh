
i-aaba69c3 monitoring-pending

此命令可以再次运行（短暂延迟后），以确认已为该指定实例启用了 CloudWatch：

```
$ ec2-monitor-instances i-aaba69c3
```

i-aaba69c3 monitoring-enabled

`mon-list-metrics` 命令（来自 CloudWatch 工具）显示可用指标列表：

```bash
$ mon-list-metrics

CPUUtilization AWS/EC2 {ImageId=ami-3c47a355}

CPUUtilization AWS/EC2 {InstanceType=m1.small}

CPUUtilization AWS/EC2

CPUUtilization AWS/EC2 {InstanceId=i-aaba69c3}

: 一大长列表...
```

结果按指标（`DiskReadBytes`, `DiskReadOps`, `NetworkIn`, `NetworkOut`, `DiskWriteBytes`, `DiskWriteOps` 等）进行细分，并指示可以从 CloudWatch 请求的维度（`ImageId`, `InstanceId`, `InstanceType` 等）。指标会被保留，并且可以检索您最近终止的实例。见证下面 CPU 利用率的以下维度。

这是所有正在运行或最近终止的 EC2 实例的 CPU 利用率的维度：

```
CPUUtilization AWS/EC2
```

这表示类型 `m1.small` 的正在运行/最近终止的 EC2 实例的 CPU 利用率：

```
CPUUtilization AWS/EC2 {InstanceType=m1.small}
```

这同样是，但它适用于使用指定 AMI 启动的那些实例：

```
CPUUtilization AWS/EC2 {ImageId=ami-3c47a355}
```

而这里是针对特定的正在运行或最近终止的 EC2 实例：

```
CPUUtilization AWS/EC2 {InstanceId=i-aaba69c3}
```

一旦您选择了一个维度，您可以使用 `mon-get-stats` 命令检索任何您想要的指标。例如，过去 24 小时内每小时的所有 CPU 利用率：

```bash
$ mon-get-stats CPUUtilization --statistics Average
--start-time 2010-07-27 --end-time 2009-07-28 --period 3600
--namespace AWS/EC2
2009-07-18 00:00:00 60.0 5.9479999999999995 Percent
```

| 2009-07-18 01:00:00 | 60.0 | 6.910833333333331 | Percent |
| 2009-07-18 02:00:00 | 60.0 | 6.614666666666667 | Percent |
| ... | | | |

前两列表示聚合数据的时间和日期。第三列是 CloudWatch 用于生成该指标的样本数量。在这种情况下，我们请求按小时显示结果（`--period 3600`），因此 CloudWatch 对每个结果使用了 60 个样本（每分钟采集一个）。下一列是请求的指标，即每小时的平均 CPU 利用率。最后一列是单位（CPU 利用率百分比）。

你应该尝试使用各种参数来运行 `mon-get-stats`，以便更好地掌握这些指标及其关联的单位。

## 编程 Amazon CloudWatch

既然我们已经了解了如何从命令行访问 CloudWatch，让我们看看 CloudFusion 提供的功能，并使用其 `AmazonCloudWatch` 类来绘制一些酷的图表。

### 列出可用指标

下面是一个用于列出所有可用指标的程序：

```php
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('cloudwatch.class.php');
$cw = new AmazonCloudWatch();
$res = $cw->list_metrics();
if ($res->isOK())
{
  $metrics     = $res->body->ListMetricsResult->Metrics->member;
  $metricsRows = array();
  foreach ($metrics as $metric)
  {
    $metricsRows[] =
        array('MeasureName' => (string) $metric->MeasureName,
            'Namespace' => (string) $metric->Namespace,
            'Name' => (string) $metric->Dimensions->member->Name,
            'Value' => (string) $metric->Dimensions->member->Value);
  }
  usort($metricsRows, 'CmpMetrics');
  printf("%-16s %-16s %-16s %-16s\n",
        "Namespace", "Measure Name", "Name", "Value");
  printf("%-16s %-16s %-16s %-16s\n",
        "==========", "================", "====", "====");
  foreach ($metricsRows as $metricsRow)
  {
    printf("%-16s %-16s %-16s %-16s\n",
        $metricsRow['Namespace'],
        $metricsRow['MeasureName'],
        $metricsRow['Name'],
        $metricsRow['Value']);
  }
}
else
{
    $error = $res->body->Error->Message;
    exit("Could not list metrics: ${error}\n");
}
function CmpMetrics($m1, $m2)
{
    $k1 = $m1['Namespace'] . $m1['MeasureName'] . $m1['Name'];
    $k2 = $m2['Namespace'] . $m2['MeasureName'] . $m2['Name'];
    return strcmp($k1, $k2);
}
?>
```

该程序调用 `list_metrics` 方法，然后将结果复制到 PHP 数组中。PHP 的 `usort` 函数用于对数组进行排序，使得元素按照命名空间（`Namespace`）、度量（`Measure`）和名称（`Name`）分组，如代码中 `CmpMetrics` 函数所示。

该程序产生以下输出：

| 命名空间 | 度量名称 | 名称 | 值 |
| :--- | :--- | :--- | :--- |
| `============` | `============` | `====` | `====` |
| AWS/EC2 | CPUUtilization | ImageId | `ami-3c47a355` |
| AWS/EC2 | CPUUtilization | InstanceId | `i-aaba69c3` |
| AWS/EC2 | CPUUtilization | InstanceType | `m1.small` |
| ... | | | |

当然，这与 `mon-list-metrics` 命令产生的输出非常相似。

## 绘制多个指标图表

让我们创建一个包含 CloudWatch 指标图表的网页。实现此功能的代码将相当复杂，因此我们将分部分构建。本节的程序将生成一个网页，因此你希望在 Web 服务器上运行它。

该程序将使用 Google Chart API，^6 并在同一页面上绘制七个图表，如图 7.2 中的示例所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_220_0.png)

我们的脚本以通常的方式开始：

```php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class');
```
