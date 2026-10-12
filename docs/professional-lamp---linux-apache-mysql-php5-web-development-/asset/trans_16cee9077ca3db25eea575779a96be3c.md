

## 使用已安装的包

一旦安装好包，其使用和访问都非常简单。只需在脚本开头包含一行引入必要文件的代码，如下所示：

```php
<?php
require_once('HTML/QuickForm.php');

//you are now able to access and reference classes, methods and properties
//contained in the quickform.php file to easily create HTML forms.
?>
```

## 快速粗陋的 PEAR 包

截至目前，共有 318 个 PEAR 包可用于各种领域，并且每天都在增加新的包。虽然本书不会讨论所有这些包，但以下章节将探讨其中一些更常见的包，并突出显示你可能需要确保已安装的包。此外，请记住，这些章节保持简洁，但如果你需要更健壮的功能，它们也会为你指明正确的方向。

## Auth_HTTP

该包的目的是提供一个类似于 Apache 的 .htaccess 登录框的身份验证系统。这是一种简单快捷的方式，用于保护网站某个区域的密码。请注意，该包依赖于更健壮的 PEAR::Auth，而 PEAR::Auth 又依赖于 PEAR::DB 包，因此在 Auth_HTTP 包能够正常运行之前，需要先安装这两个包。

Auth_HTTP 的简单用法如下：

```php
<?php
require_once('Auth/HTTP.php');

$a = new Auth_HTTP("DB", "mysqli://username:password@localhost/databasename");
$a->start();
?>
```

首先，你包含文件 `Auth/HTTP.php`，这使你能够访问正确的包。然后，你使用上述参数实例化一个新的 Auth_HTTP 对象。由于你实际上是在使用 PEAR::DB 包登录数据库，因此你可以更改正在使用的数据库类型，并指定其他选项，例如套接字、路径、端口号等。尽管本章稍后将简要讨论此包，但 PEAR::DB 包的详细描述可在 http://pear.php.net/manual/en/package.database.db.php 找到。接下来，你通过调用 start() 函数启动身份验证过程，你的页面就受到密码保护了。

当然，这留下了很大的改进和自定义空间，你可以更进一步，要求身份验证过程从数据库中的表登录用户。你可以通过使用 $authOptions 变量来指定登录选项：

```php
<?php

require_once("Auth/HTTP.php");

$authOptions = array(
//use the same data source name (database login info) as in previous example
'dsn'=>'mysql://username:password@localhost/databasename',

//specify the database table that contains user info
'table'=>"users",

//specify the column that holds the username
'usernamecol' =>"username",

//specify the column that holds the passwords
'passwordcol' =>"password",

//specify the encryption type used
'cryptType' =>"md5",
);

$a = new Auth_HTTP("DB", $authOptions);
//specify the name of your realm
$a->setRealm('Registered Users Only');
//specify the error message seen by the user if authentication fails
$a->setCancelText('<h2>Access Denied.</h2>');

$a->start();

//check to see if the user is authorized
if($a->getAuth())
{
//body of authorized text goes here.
echo "Hi there, authorized user!";
}
?>
```

你可以看到，这提供了一种非常便捷的方式来验证用户。要在其他页面上检查授权，只需使用 `getAuth()` 函数即可。

Auth_HTTP 包还有其他可指定的参数，并且 Auth 包提供了一个非常健壮的基于 HTML 表单的身份验证系统。你可以分别在 <http://pear.php.net/manual/en/package.authentication.auth-http.php> 和 <http://pear.php.net/manual/en/package.authentication.auth.php> 阅读有关这些包的更多信息。

## Date

虽然 PHP 提供了返回日期和时间信息的内置函数，但此 PEAR 包提供了简单的方法来将这些信息操作为常用结果，例如该月剩余天数、当前星期几等。

这个包可用的函数非常多，我们要为每个函数提供示例会很困难。但是，以下章节描述了 Date 类中一些更常用方法。访问 <http://pear.php.net/package/Date/docs/latest/Date/Date.html> 可查看方法的完整列表。

### Date 类

该类出现在主要的 date.php 文件中，并提供以下方法供你使用：

- `Date`：构造函数，创建一个新日期对象。
- `addSeconds`：向日期添加特定数量的秒数。
- `addSpan`：向日期添加时间跨度。
- `after`：确定一个日期是否在另一个日期之后。
- `before`：确定一个日期是否在另一个日期之前。
- `convertTZ`：将日期转换为另一个时区。
- `equals`：确定两个日期和/或时间是否完全相等。
- `format`：根据用户规格格式化日期。
- `getDate`：以特定格式返回日期。
- `getDay`：返回日期对象当月的天数。
- `getDayName`：以字符串格式返回日期对象所在星期几。
- `getDayOfWeek`：以整数格式返回日期对象所在星期几。
- `getDaysInMonth`：返回日期对象所在月的天数。
- `getHour`：返回日期对象的小时。
- `getMinute`：返回日期对象的分钟。
- `getMonth`：以整数格式返回日期对象的月份。
- `getMonthName`：以字符串格式返回日期对象的月份。
- `getNextDay`：返回日期对象次日日期。
- `getNextWeekday`：返回日期对象下一个工作日日期。
- `getPrevDay`：返回日期对象前一日日期。
- `getPrevWeekday`：返回日期对象上一个工作日日期。
- `getQuarterOfYear`：以整数格式返回日期对象所在的季度。
- `getSecond`：返回日期对象的秒数。
- `getTime`：返回自 Unix 纪元以来的秒数。
- `getWeekOfYear`：以整数格式返回日期对象所在的周数。
- `getWeeksInMonth`：返回日期对象所在月的周数。
- `getYear`：返回日期对象的年份。
- `inDaylightTime`：确定该时间/日期是否处于夏令时。
- `isLeapYear`：确定日期对象的年份是否为闰年。
- `setDate`：设置日期对象的日期。
- `setDay`：设置日期对象的天数。
- `setHour`：设置日期对象的小时。
- `setMinute`：设置日期对象的分钟。
- `setMonth`：设置日期对象的月份。
- `setSecond`：设置日期对象的秒数。
- `setTZ`：设置日期对象的时区。
- `setYear`：设置日期对象的年份。

以上就是 Date 类的内容。Date 类还使用了另外两个类，但这些类也可以直接使用；它们是 Date_Span 和 Date_TimeZone 类。如果你需要比 Date 类能提供的更具体的功能，例如返回所有可用时区的列表或确定服务器的默认时区，它们内部有许多特定的方法。

### 一个快速示例

以下是一个快速示例，说明使用 Date 包输出像今年剩余周数这样的信息有多容易：

```php
<?php
require_once("date.php");

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());

echo "There are " . $weeksleft . " weeks left in the year.";
?>
```

正如你所见，当尝试完成更复杂的日期计算或处理时区时，如此简单的功能真的能让你的生活更轻松。

## DB

这是 PEAR 包，允许你轻松连接和查询数据库。还有许多其他与数据库相关的包可供参考。例如，MDB 与 DB 类似，但提供了更多

