
```php
$averages[$i] = (int) ($averages[$i] * $scale);

$minimums[$i] = (int) ($minimums[$i] * $scale);

$maximums[$i] = (int) ($maximums[$i] * $scale);

$sums[$i]     = (int) ($sums[$i]     * $scale);

}
```

图表 API 接受图表中每条线的值作为逗号分隔的字符串。不同线的值通过管道符或垂直线字符分隔。以下是设置此处的代码：

```php
// chapter_07/statistics_chart_page.php (excerpt)

$average = implode(',', $averages);

$minimum = implode(',', $minimums);

$maximum = implode(',', $maximums);

$sum     = implode(',', $sums);

// Combine arrays for use in chart

$series = $average . '|' .

          $minimum . '|' .

          $maximum . '|' .

          $sum;
```

坚持住，我们即将准备好生成图表！下一步是将图表标题中嵌入的空格替换为加号（`+`）并设置颜色：

```php
// chapter_07/statistics_chart_page.php (excerpt)

$label = str_replace(' ', '+', $label);

$colors = 'ff0000,00ff00,0000ff,800080';
```

既然我们已拥有所需的所有信息，现在可以组合出图表的 URL 了。代码如下：

```php
// chapter_07/statistics_chart_page.php (excerpt)

$chartURL = "http://chart.apis.google.com/chart";

$chartURL .= "chs=300x180";            // Chart size

$chartURL .= "cht=lc";                 // Line chart

$chartURL .= "chtt=" . $label;         // Label

$chartURL .= "chdlp=b";                // Legend at bottom

$chartURL .= "chdl=Avg|Min|Max|Sum";   // Legend

$chartURL .= "chco=" . $colors;        // Colors

$chartURL .= "chd=t:" . $series;        // Data series
```

Google Chart API 包含许多高级格式化和标签选项，但我让这个示例保持相当精简，以留给你们改进的空间。

最后一步是将 URL 存储在 `$ChartImages` 数组中：

```php
// chapter_07/statistics_chart_page.php (excerpt)

$ChartImages[] = $chartURL;
```

在保存了所有图表的 URL 之后，最终步骤是包含我们的 HTML 模板并退出：

```php
// chapter_07/statistics_chart_page.php (excerpt)

$output_title = 'Chapter 7 Sample - Charts of CloudWatch ' .

        'Statistics';

$output_message = "Charts of CloudWatch Statistics from ${start} " .

        " to ${end}";

include 'include/statistics.html.php';
```

最后，这是我们页面的简单 HTML 模板：

```html
<!-- chapter_07/statistics_chart_page.php (excerpt) -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
        <title><?php echo $output_title ?></title>
</head>
<body>
        <h1><?php echo $output_title ?></h1>
<p><?php echo $output_message ?></p>
<?php foreach($ChartImages as $image): ?>
        <img src="<?php echo $image ?>"/>
<?php endforeach ?>
</body>
</html>
```

需要意识到的重要一点是，该程序从未进行任何实际的绘制。相反，它创建一个 HTML 页面，让 Google 来完成工作。当浏览器渲染该页面时，它会为页面上的每个图表调用 Google Chart API。Google 的服务器将处理 URL，绘制图表并将其返回给浏览器；然后浏览器将把图表作为页面的一部分绘制出来。

图 7.3 展示了完成后的页面外观。

![](img/4a5ba0dd041e08e6a67fa31d52309995_228_0.png)

请记住，该页面接受一些参数。你可以尝试使用 `period` 参数，在不同的时间范围内聚合指标。你可以将 `start` 和 `end` 参数设置为日期（使用 `2009-07-07` 这样的值）或带时间的日期（使用 `2009-07-07T12:00:00` 这样的值）。只需将参数附加到页面 URL 即可。以下是一个示例：

```text
statistics_chart_page.php?period=60&start=2009-07-20T12:00:00&end=2009-07-20T18:00:00
```
