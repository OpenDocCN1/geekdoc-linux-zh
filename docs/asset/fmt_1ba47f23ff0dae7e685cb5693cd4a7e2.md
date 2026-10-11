
Service, Operation, UsageType, StartTime, EndTime, UsageValue

AmazonEC2,PublicIP-In,DataTransfer-Regional-Bytes,01/01/09 00:00:00,01/02/09 00:00:00,97625

AmazonEC2,RunInstances,BoxUsage,01/01/09 00:00:00,01/02/09 00:00:00,24

AmazonEC2,ElasticIP-Out,DataTransfer-Regional-Bytes,01/01/09 00:00:00,01/02/09 00:00:00,558960

AmazonEC2,ElasticIP-In,DataTransfer-Regional-Bytes,01/01/09 00:00:00,01/02/09 00:00:00,24449

...

文件的第一行提供字段名称，而其他行包含数据：每行一条记录，值由逗号分隔。PHP 的 `fgetcsv` 函数使处理 CSV 文件变得容易。该函数从文件中读取一行，在逗号边界处分离字段（尊重带引号的字符串），并返回一个值数组。以下是它对我的文件第一行返回的内容：

```text
Array (
   [0] => Service
   [1] => Operation
   [2] => UsageType
   [3] => StartTime
   [4] => EndTime
   [5] => UsageValue
)
```

每个 AWS 服务的使用数据文件包含一些公共字段和特定于特定服务的字段。例如，S3 的使用数据文件还包含一个 `Resource` 字段。该字段将使用数据与 S3 存储桶关联。

类似地，Amazon CloudFront 的使用数据文件使用 `Resource` 字段来标识与特定 CloudFront 分发关联的账户数据。由于数据格式包含公共元素和一些特定服务的变体，Amazon SimpleDB 成为存储它的理想系统。我们需要一个域：

```text
chapter_10/include/book.inc.php (excerpt)
define('BOOK_AWS_USAGE_DOMAIN', 'aws_usage');
```

我们可以使用第 8 章中创建域程序的修改版来创建此域：

```text
chapter_10/create_domain.php (excerpt)
$res = $sdb->create_domain(BOOK_AWS_USAGE_DOMAIN);
```

让我们编写一个程序，从命令行指定的一个或多个 CSV 文件中导入数据。以下是我们开始所需的内容：

```text
chapter_10/import_usage.php (excerpt)
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');
if ($argc == 1)
{
    exit("Usage: " . $argv[0] . " CSV_FILE ...\n");
}
```

该脚本期望在命令行找到一个或多个 CSV 文件，上述代码执行此检查。如果命令行参数太少，它会输出一条有用的消息。

我们将把数据存储在 SimpleDB 中，因此需要一个访问对象：

```php
chapter_10/import_usage.php (excerpt)
$sdb = new AmazonSDB();
```

然后，我们可以使用自定义的 `ImportCSV` 函数来处理每个文件，这个函数我们稍后会编写：

```php
chapter_10/import_usage.php (excerpt)
for ($i = 1; $i < $argc; $i++)
{
    $file = $argv[$i];
    if (($ret = ImportCSV($sdb, $file)) !== false)
    {
        print("Imported ${file}: ${ret} records\n");
    }
    else
    {
        print("Did not import ${file}\n");
    }
}
```

让我们来看一下 `ImportCSV` 函数。第一步是尝试打开文件；如果无法打开，它将返回 `false`：

```php
chapter_10/import_usage.php (excerpt)
function ImportCSV($sdb, $file)
{
    $fp = fopen($file, 'r');
    if ($fp === false)
    {
        return false;
    }
    ...
}
```

由于 CSV 文件的第一行包含字段名称，我们将其读取到 `$fields` 数组中。在处理并存储每行数据时，我们需要这些名称。我们还将跟踪已读取和处理的行数：

```php
$fields = fgetcsv($fp);
$recordCount = 0;
```

现在我们可以处理每个数据行：

```php
while (($data = fgetcsv($fp)) != false)
{
    $recordCount++;
}
```

如我在第 8 章中所述，选择 SimpleDB 键是有讲究的。在构建此工具时，我希望能够导入相同的数据文件，或者导入多个日期重叠的数据文件，同时保持数据的完整性。经过一些实验，我通过拼接服务名称和非数据字段（除了 `UsageValue` 之外的所有内容）的 MD5 哈希值来构建键。我的算法生成了这样的键：

![](img/4a5ba0dd041e08e6a67fa31d52309995_319_0.png)

让我们继续。我们从 `Key` 和 `KeyData` 变量开始：

```php
$key     = '';
$keyData = '';
```

然后处理每行的每个字段。回想一下，`$fields` 变量包含文件的字段名称。我还更改了日期字段（`StartTime` 和 `EndTime`）的格式，以便日后能更好地进行基于范围的查询。以下是字段处理代码：

![](img/4a5ba0dd041e08e6a67fa31d52309995_320_0.png)

在这个循环结束时，`$attrs` 数组包含要写入 SimpleDB 的数据，`$key` 包含键的前缀，`$keyData` 包含要哈希以形成键剩余部分的数据。以下是我的数据中 `$attrs` 数组的转储：

![](img/4a5ba0dd041e08e6a67fa31d52309995_320_1.png)

我可能应该将 `UsageValue` 字段填充为固定长度。由于我没有计划对该字段执行任何查询，所以没有这样做。¹ 请注意，输入文件中的字段名称直接控制数据在 SimpleDB 中的存储方式。

把所有内容整合起来，以下是如何形成 SimpleDB 键的方法：

```php
chapter_10/import_usage.php (excerpt)
$key = $key . '_' . md5($keyData);
```

最后，我们将数据存储在 SimpleDB 中，并注意指定任何现有同名的属性都将被替换：

```php
chapter_10/import_usage.php (excerpt)
$res = $sdb->put_attributes(BOOK_AWS_USAGE_DOMAIN,
    $key, $attrs, true);
```

进行简单的错误检查，我们这就快完成了：

```php
chapter_10/import_usage.php (excerpt)
if (!$res->isOk())
{
    $error = $res->body->Errors->Error->Message;
    print("Could not insert ${key}: ${error}\n");
}
```

最后一步，在所有行处理完毕后，关闭文件并返回记录数：

```php
chapter_10/import_usage.php (excerpt)
fclose($fp);
return $recordCount;
}
?>
```

> ¹ 这在我这里可能有点短视，但我确实需要留一些代码作为练习让大家自己动手完成！

在您将所有使用量文件下载到您的 EC2 实例后，按如下方式运行导入程序：

```
<dev>: php import_usage.php *.csv
```

它将依次处理每个文件，并报告每个文件的记录数：
