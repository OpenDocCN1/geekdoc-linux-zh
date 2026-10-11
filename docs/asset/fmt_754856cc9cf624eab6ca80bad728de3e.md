
我们将需要进行一些数据处理。默认情况下，程序将报告前 24 小时收集的指标。变量 `$StartDate_DT` 将表示开始日期和时间，而变量 `$EndDate_DT` 将表示结束日期和时间。让我们声明并设置它们：

```php
$StartDate_DT = new DateTime('now');
$EndDate_DT   = new DateTime('now');
$StartDate_DT->modify('-1 day');
```

CloudWatch 以 GMT（格林尼治标准时间）表示所有日期。如果你想以本地时间表示日期和日期范围，必须调整你的查询。

下一步是将日期值转换为在 CloudWatch 查询中使用所需的格式。这是使用 PHP 的 `DateTime` 类的 `format` 方法完成的，如下所示：

```php
$StartDate = $StartDate_DT->format('Y-m-d');
$EndDate   = $EndDate_DT->format('Y-m-d');
```

如果请求中提供了参数，请获取它们。否则，我们将使用合理的默认值：

```php
$period = isset($_GET['period']) ? $_GET['period'] : 15;
$start  = isset($_GET['start']) ? $_GET['start']  : $startDate;
$end    = isset($_GET['end'])    ? $_GET['end']    : $endDate;
$period *= 60;
```

注意在这种情况下三元运算符（`? :`）是多么方便和简洁？在适当的格式化下，很容易识别这种结构，并将其作为一个非常紧凑的 if-then-else 在心理上处理。

为了方便，周期参数以分钟指定，但 CloudWatch 需要秒，因此我们进行调整。

该程序将生成一系列七个图表，由 `$charts` 数组中的信息驱动。它看起来像这样：

```php
$charts = array(
    array('M' => 'NetworkIn',
          'U' => 'Bytes',
          'L' => 'Network In (Bytes)'),
    array('M' => 'NetworkOut',
          'U' => 'Bytes',
          'L' => 'Network Out (Bytes)'),
    array('M' => 'CPUUtilization',
          'U' => 'Percent',
          'L' => 'CPU Utilization (Percent)'),
    array('M' => 'DiskReadBytes',
          'U' => 'Bytes',
          'L' => 'Disk Read Bytes'),
    array('M' => 'DiskReadOps',
          'U' => 'Count',
          'L' => 'Disk Read Operations/Second'),
    array('M' => 'DiskWriteBytes',
          'U' => 'Bytes',
          'L' => 'Disk Write Bytes'),
    array('M' => 'DiskWriteOps',
          'U' => 'Count',
          'L' => 'Disk Write Operations/Second'),
);
```

数组中的每个元素包含三个字符串。`M` 元素指定图表的 CloudWatch 度量，`U` 元素指定 CloudWatch 单位，`L` 元素指定图表标题。

完成所有这些后，是时候创建一个 `AmazonCloudWatch` 类的实例了：

```php
$cw = new AmazonCloudWatch();
$opt = array('Namespace' => 'AWS/EC2', 'Period' => $period);
$Statistics = array('Average','Minimum','Maximum','Sum');
```

我们还需要一个可选参数数组。这些参数在每次调用中保持不变，因此我们现在可以在上面的 `$opt` 数组中设置它们。所需的统计信息也是如此，我们将其放入 `$Statistics` 数组中。

现在让我们回到刚才设置的 `$charts` 数组。在下面的代码中，我们开始一个简单的循环，遍历元素以提供生成图表所需的信息。我们还创建了 `$chartImages` 数组来保存我们将在接下来的 HTML 模板中使用的图表源 URL：

```php
$chartImages = array();
foreach ($charts as $chart)
{
    $measure = $chart['M'];
    $unit    = $chart['U'];
    $label   = $chart['L'];
```

这段代码设置循环并获取每个图表的度量、单位和标签。

有了这些信息，是时候从 CloudWatch 获取所需的指标了，如下所示：

```php
$res = $cw->get_metric_statistics($Measure,
    $Statistics,
    $Unit,
    $Start,
    $end,
    $opt);
if ($res->isOk())
{
```

此请求中未指定维度；相反，它检索关于所有正在运行和最近终止的 EC2 实例的信息。一如既往，在处理结果之前，我们需要确保此请求成功。

指标以不可预测的顺序返回。由于我们计划使用它们来绘制图表，因此需要捕获所有指标并对其进行排序。让我们深入返回值并找到 `Datapoints` 项：

```php
$dataPoints = $res->body->GetMetricStatisticsResult->DataPoints->member;
```

现在我们创建一个空数组，然后从 `DataPoints` 中提取指标，将它们存储在 `$dataRows` 中，并以返回的时间戳作为索引：

```php
$dataRows = array();
foreach ($dataPoints as $dataPoint)
{
    $timestamp = (string) $dataPoint->Timestamp;
    $dataRows[$timestamp] =
        array('Timestamp' => (string) $dataPoint->Timestamp,
              'Units'     => (string) $dataPoint->Unit,
              'Samples'   => (string) $dataPoint->Samples,
              'Average'   => (float)  $dataPoint->Average,
```

在上述代码的末尾，我们按数组键（每个指标的 `_timestamp_`）对指标进行排序。

现在指标已排序完成。由于我们将生成图表，实际上需要四个独立的数组，分别用于绘制每一种统计量。下面的代码将 `$dataRows` 数组转换为这些独立的数组：

```php
$averages   = array();
$minimums   = array();
$maximums   = array();
$sums       = array();
foreach ($dataRows as $dataRow)
{
    $averages[]   = $dataRow['Average'];
    $minimums[]   = $dataRow['Minimum'];
    $maximums[]   = $dataRow['Maximum'];
    $sums[]       = $dataRow['Sum'];
}
```

Google Chart API 有多种指定数据值的方法。最简单的一种将值限制在 0 到 100（含）的范围内。因此，下一步是计算所需的缩放系数，以便将所有统计量映射到此范围，然后利用该系数缩放每个数组：

```php
$chartMax    = max(max($averages), max($minimums),
               max($maximums), max($sums));
$scale       = 100.0 / $chartMax;
for ($i = 0; $i < count($averages); $i++)
{
```
