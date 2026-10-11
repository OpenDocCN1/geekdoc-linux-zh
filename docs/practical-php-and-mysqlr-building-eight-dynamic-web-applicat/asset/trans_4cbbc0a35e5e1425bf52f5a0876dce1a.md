
在这里，发出一个简单的 SELECT 查询，以返回从今天开始的所有事件。检查是否未返回任何行。如果是这种情况，则显示文本“无事件！”。否则，将添加一个链接来运行 `getEvent()` JavaScript 函数（稍后您将详细查看该函数）。

示例 8-7 展示了完整的侧边栏代码。

### 示例 8-7 侧边栏处理月份、事件详情和即将发生的事件。

```php
<?php

if(isset($_GET['date']) == TRUE) {
    $explodedate = explode("-", $_GET['date']);
    $month = $explodedate[0];
    $year = $explodedate[1];
    $sundays = date('t', mktime(0, 0, 0, $month, 1, $year));
} else {
    $month = date("n", mktime());
    $sundays = date("t", mktime());
    $year = date("Y", mktime());
}

$displaydate = date("F Y", mktime(0, 0, 0, $month, 1, $year));

if($month == 1) {
    $prevdate = "12-" . ($year-1);
}
else {
    $prevdate = ($month-1) . "-" . $year;
}
if($month == 12) {
    $nextdate = "1-" . ($year+1);
}
else {
    $nextdate = ($month+1) . "-" . $year;
}

?>
<span class="datepicker">
<?php
echo "<a href=\"$SCRIPT_NAME?date=" . $prevdate . "\">&larr;</a> ";
echo $displaydate;
echo "<a href=\"$SCRIPT_NAME?date=" . $nextdate . "\">&rarr;</a> ";
echo "</span>";
echo "<br />";
?>
<div id="eventcase">
<?php
echo "To view event information here, click on the item in the calendar.";
?>
</div>

<?php
echo "<h1>Latest Events</h1>";

echo "<ul>";
$qnearsq1 = "SELECT * FROM events WHERE date >= NOW() ORDER BY starttime";
$nearres = mysql_query($qnearsq1);
$nearnumrows = mysql_num_rows($nearres);
if($nearnumrows == 0) {
    echo "No events!";
}
else {
    while($nearrow = mysql_fetch_assoc($nearres)) {
        echo "<li><a href='#' onclick='getEvent(" . $nearrow['id'] . ")'>" . $nearrow['name'] . "</a> (" . $nearrow['date'] . ")</li>";
    }
}
echo "</ul>";

?>
```

主日历视图显示一个月的日历，并列出该月任何事件的适当日期。

构建一个月的日历涉及创建若干行，如图 8-5 所示。

要构建类似这样的内容，你需要先创建一个表格，然后逐行添加每一行。星期几是表格标题，然后你逐渐构建出每一行单独的日期。

### 注意：严重警告

编写日历视图代码是一个出奇地棘手的过程。如果你弄丢了逻辑线索，你会花费数小时试图理解为什么你得到的结果与预期略有不同。诀窍是逐步构建日历。

![图 8-5](img/c75d0c4fa51711b62f211459ae794f3f_300_0.png)

**图 8-5** 日历视图包含若干行，包括星期几、日期以及事件所在区域。

创建一个名为 `view.php` 的新文件并添加以下代码：

```php
<?php

session_start();

require("config.php");

if(isset($_SESSION['LOGGEDIN']) == FALSE) {
    header("Location: " . $config_baseDir);
}
```

在保护页面免受未登录用户访问后，创建一个小型函数：

```php
function short_event($name) {
    $final = "";
    $final = (substr($name, 0, 12) . "...");

    return $final;
}
```

此函数将缩短添加到日历某天的事件名称。以你的 *Working Breakfast* 事件为例，其名称在日历上被缩短为 *Working Brea...*。这将使事件保持单行显示。为此，该函数使用 *substr*() 截取前 12 个字符，然后在字符串末尾附加 *...*。

继续添加代码：

```php
require("header.php");

if($_GET['error']) {
    echo "<script>newEvent('" . $_GET["eventdate"] . "', 1)</script>";
}
```

这段代码检查是否存在 *error* GET 变量。如果是，则添加一个 *<script>* 标签。此代码块旨在用于用户随后在表单中输入新事件的情况。如果表单包含错误，页面将重新加载，并且 *<script>* 标签运行 *newEvent*() JavaScript 函数。此函数接收两个参数：日期和错误代码。（*newEvent*() 将在本章稍后详细讨论。）

创建变量并添加表格标题：

```php
$cols = 7;
$weekday = date("w", mktime(0, 0, 0, $month, 1, $year));

$numrows = ceil(($sundays + $weekday) / $cols);

echo "<br />";
echo "<table class='cal' cellspacing=0 cellpadding=5 border=1>";
echo "<tr>";
echo "<th class='cal'>Sunday</th>";
echo "<th class='cal'>Monday</th>";
echo "<th class='cal'>Tuesday</th>";
echo "<th class='cal'>Wednesday</th>";
echo "<th class='cal'>Thursday</th>";
echo "<th class='cal'>Friday</th>";
echo "<th class='cal'>Saturday</th>";
echo "</tr>";

$counter = 1;
$newcounter = 1;
```

前三行设置了一些必需的变量。首先，你在 `$cols` 变量中指定列数——你使用 7，代表每一天。接下来，`weekday` 变量返回该月第一天的星期几编号。例如，如果当天是星期五，它是第六天，函数返回 5。

### 注意：从零开始计数

PHP 中的许多函数从零开始计数。当你编写代码并得到略微不同的结果（例如出现 8 个单元格而不是 7 个）时，可能是因为你假设函数从 1 开始计数。虽然有时情况如此，但大多数函数从 0 开始。

`$numrows` 变量取 `bar.php` 中的 `$sundays` 变量，加上 `weekday`，然后除以列数（7）。你将 `weekday` 加到 `$sundays` 的原因是填充上个月剩余的天数。参照图 8-5，你可以看到该月从星期五开始，但星期日到星期四几天不包含任何日期。通过添加 `weekday`，你设置了需要填充的天数。在此示例中，星期五返回 5，如果你从左到右计数（从 0 开始），你会得到星期五。

设置这些变量后，添加表格标题，最后，将两个变量设置为 1。这些变量稍后将在代码中用作计数器。

现在，你可以添加第一行单元格，为给定日期添加日期。在开始添加实际日期之前，填充月初前的天数：

```php
echo "<tr>";

$daysleft = 6 - $weekday;

for($f=0; $f<=$weekday; $f++) {
    echo "<td class='cal_date' width='110' height='10'>";
    echo "</td>";
}

echo "</td>";

for($f=0; $f<=$daysleft; $f++) {
    echo "<td class='cal_date' width='100' height='10'>";

    $display = date("js", mktime(0, 0, 0, $month, $counter, $year));

    $todayday = date("d");
    $todaymonth = date("n");
    $todayyear = date("Y");

    if($counter == $todayday AND $month == $todaymonth AND $year == $todayyear) {
        echo "<strong>TODAY " . $display . "</strong>";
    }
    else {
        echo $display;
    }

    echo "</td>";
    $counter++;
}

echo "</tr>";
```

在循环内部，使用 `date()` 存储格式化日期以创建 `$display` 变量。然后，`$todayday`、`$todaymonth` 和 `$todayyear` 变量被填充为今天日期的相关部分。接下来，进行检查以查看今天的详细信息是否匹配之前创建的相应 `$counter`、`$month` 和 `$year` 变量。
