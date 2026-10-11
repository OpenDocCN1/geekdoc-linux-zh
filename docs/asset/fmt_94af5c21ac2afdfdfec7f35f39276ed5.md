
我将展示传输出去的数据。这代表从 S3 传输到外部世界的 S3 对象数据字节数。当然，您也可以自由将引号中的值替换为其他类型的用量，例如 `DataTransfer-In-Bytes`（从外部世界传输到 S3 的数据字节数）或 `StorageObjectCount`（存储在存储桶中的对象数量），甚至是 `TimedStorage-ByteHrs`（存储在桶中的数据消耗的字节-小时数）。

顺便说一句，字节-小时与您坐在牙医椅子上的时间完全无关。它代表存储的字节数与其存储小时数的乘积之和。我的一个存储桶的字节-小时用量值为 14,597,270,160。这意味着该存储桶在从 2009 年 8 月 18 日开始的 24 小时期间内存储了约 608 兆字节的数据。

该脚本将报告每个 S3 存储桶的用量，因此我们创建常规的访问对象并获取存储桶列表：

```php
// chapter_10/bucket_usage_page.php (excerpt)

$S3   = new AmazonS3();

$Sdb  = new AmazonSDB();

$_buckets = $S3->get_bucket_list();
```

现在我们需要进行一些日期运算。我们将报告从今天开始，往前推六天，即整整一周的数据范围。以下代码为日期范围查询设置了 `$firstDay` 和 `$lastDay`，并创建了 `$days` 数组，其中包含范围内每个日期的年-月-日表示形式。开始吧：

```php
// chapter_10/bucket_usage_page.php (excerpt)

$today = date_create("now");

$lastDay = $today->format("Y-m-d");

$days = array();

for ($i = 0; $i < 7; $i++)

{

    date_modify($today, "-1 day");

    $days[] = $today->format("Y-m-d");

}

$firstDay = $days[6];
```

我们将使用 `$days` 数组来生成 HTML 表格的列标题。

好的，现在到了精彩的部分——获取每个存储桶的用量数据并将其存储在 `$rows` 数组中，以便最终生成表格行。该循环简单遍历每个存储桶，并调用自定义的 `GetUsage` 函数从 SimpleDB 检索 S3 用量数据。代码如下：

```php
// chapter_10/bucket_usage_page.php (excerpt)

$rows = array();

foreach ($buckets as $bucket)

{

    $dailyUsage = GetUsage($sdb, $usage, $bucket, $firstDay, $lastDay);
```

如果给定日期区间内存储桶没有用量数据，`GetUsage` 将返回一个空数组。为了保持输出紧凑，下面的代码简单地跳过这样的存储桶。用量数据数组以存储桶名称作为键存储在 `$rows` 数组中。如果某一天没有数据，则数组中存储空字符串。最后，每日总计也作为存储桶数据数组的最后一个元素存储：

```php
// chapter_10/bucket_usage_page.php (excerpt)

if (count ($dailyUsage) > 0)

{

    $rows[$bucket] = array();

    foreach ($days as $day)

    {

        if (isset($dailyUsage[$day]))

        {

            $rows[$bucket][] = $dailyUsage[$day];

        }

        else

        {

            $rows[$bucket][] = ''; 

        }

    }

    $rows[$bucket][] = array_sum($dailyUsage);

}
```

剩余的复杂性存在于 `GetUsage` 函数中。它是这样的：

```php
// chapter_10/bucket_usage_page.php (excerpt)

function GetUsage($sdb, $usage, $bucket, $firstDay, $lastDay)

{

    $query = "select StartTime, UsageValue " .

             "from " . BOOK_AWS_USAGE_DOMAIN .

             " where" .

             " Service='AmazonS3' and " .

             " StartTime >= '${firstDay}' and " .

             " StartTime <= '${lastDay}' and " .

             " Resource='${bucket}' and " .

             " UsageType='${usage}';";

    $res = $sdb->select($query);

    if (!$res->isOk())

    {

        return null;

    }

    $dailyUsage = array();

    foreach ($res->body->SelectResult->Item as $item)

    {

        $attrs = getItemAttributes($item);

        $startTime = substr($attrs['StartTime'], 0, 10);

        $usage = $attrs['UsageValue'];

        $dailyUsage[$startTime] = $usage;

    }

    return $dailyUsage;

}
```

这看起来很长，但非常简单。它构建查询，运行查询，检查结果，并构建一个按日期索引的用量数组。该数组作为函数值返回。

HTML 模板是我们报告页面的最后组成部分。它以最常见的方式开始：

```html
<!-- chapter_10/bucket_usage_page.php (excerpt) -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
    <title><?php echo $output_title ?></title>
</head>
<body>
    <h1><?php echo $output_title ?></h1>
    <p><?php echo $output_message ?></p>
```

这个模板有两部分，让我们分别来看。首先，我们需要通过遍历 `$days` 数组来生成表格头行：

```html
<!-- chapter_10/bucket_usage_page.php (excerpt) -->
<table>
    <thead>
        <tr>
            <th>Bucket</th>
            <?php foreach($days as $day): ?>
                <th><?php echo $day ?></th>
            <?php endforeach ?>
            <th>Total For Bucket</th>
        </tr>
    </thead>
```

接下来，我们生成表格主体并完成页面：

```html
<!-- chapter_10/bucket_usage_page.php (excerpt) -->
    <tbody>
        <?php foreach($rows as $bucket => $cells): ?>
            <tr>
                <td><?php echo $bucket ?></td>
                <?php foreach($cells as $cell): ?>
                    <td>
                        <?php echo ($cell == '') ? '&nbsp;' : number_format($cell); ?>
