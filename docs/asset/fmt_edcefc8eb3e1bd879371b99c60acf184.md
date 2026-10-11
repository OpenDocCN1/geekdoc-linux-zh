
- PHP 的 `opendir` 和 `readdir` 用于访问当前目录（“.”）中的文件列表。
- 读取每个文件名并对照正则表达式进行检查。
- 如果文件名匹配正则表达式，则使用 `file_get_contents` 读取文件内容，然后使用 `md5` 函数计算内容的 MD5 哈希值。凭借这些信息，设置 `$attrs` 数组以包含属性的键值对。
- 调用 `put_attributes` 方法将信息存储在由 `BOOK_FILE_DOMAIN` 指定的 SimpleDB 域中。调用 `put_attributes` 时的最后一个参数（`true`）表示将删除属性的任何现有值，然后替换为新值。如果将此参数设置为 `false`，新值将补充现有值，导致属性具有多个值。
- 最后，关闭目录并退出脚本。

## 高效存储多个项目

另一个 SimpleDB 功能，`BatchPutAttributes`，可用于通过单个请求执行多个 `PutAttributes` 调用。这比进行一系列单独的请求更快、更高效。以下是使用批量请求的上一示例的修改版本：

```php
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');
$sdb = new AmazonSDB();
$items = array();
$dir = opendir(".");
while (($file = readdir($dir)) !== false)
{
    if (preg_match("/^[a-zA-Z0-9_]+\.php$/", $file))
    {
        $data = file_get_contents($file);
        $hash = md5($data);
        $size = filesize($file);
        $items[$file] = array('Name' => $file,
                              'Hash' => $hash,
                              'Size' => $size);
    }
    if (count($items) == 25)
    {
        WriteBatch($sdb, $items);
        $items = array();
    }
}
closedir($dir);
if (count($items) > 0)
{
    WriteBatch($sdb, $items);
}
```

> 与此前版本的插入脚本的主要区别在于，每个属性名称值对数组被添加到 `$items` 数组中，而不是立即插入到 SimpleDB 中。

- 当 `$items` 数组达到 25 个元素时，我们调用一个名为 `WriteBatch` 的自定义函数。
- 最后，如果还有剩余的项目，我们调用 `WriteBatch` 函数。

以下是自定义 `WriteBatch` 函数：

```php
chapter_08/batch_insert_items.php (excerpts)
function WriteBatch($ssdb, &$items)
{
    $res = $ssdb->batch_put_attributes(BOOK_FILE_DOMAIN, $items, true);
    if ($res->isOK())
    {
        print("Inserted " . count($items) . " items\n");
        return true;
    }
    else
    {
        $error = $res->body->Errors->Error->Message;
        print("Could not insert items: {$error}\n");
        return false;
    }
}
?>
```

`WriteBatch` 函数使用 `batch_put_attributes` 方法在一次操作中将 `$items` 数组中的所有项目插入。

在进行性能测试时，我发现第一个插入脚本在 8.6 秒内插入了 99 个文件，而批量脚本仅用 0.88 秒插入了相同的文件，即速度快了十倍。显然，通过利用 SimpleDB 的结构来设计您的程序是值得的。

## 处理数值数据

SimpleDB 将所有数据作为字符串存储。当数据是选择查询的主题时，使用字典序比较。这可能会导致存储数值时出现一些令人惊讶的结果。例如，字符串 "10" 小于字符串 "2"。前导负号也是有问题的。

数值值应该用零左填充以创建固定长度的字符串。可以使用 PHP 的 `sprintf` 函数和适当的格式字符串来实现。在我们之前的脚本中，我们应该更新 `Size` 属性的项目值以使用左填充：

```php
array('Name' => $file,
      'Hash' => $hash,
      'Size' => sprintf("%08d", $size));
```

如果您的数值可能为负数，在存储时应该用一个大的正数进行偏移，然后在检索时补偿这个偏移。选择一个偏移值，确保预期的最小负值最终变为正值。例如，如果您的值范围从 -32,768 到 32,767，则添加 50,000 将范围调整为 17,232 到 82,767（存储为 "17232" 到 "82767"）。

## 运行查询

数据已存储，运行查询很简单：

```php
chapter_08/query_domain.php (excerpt)
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');
$query = "select * from " .
    BOOK_FILE_DOMAIN .
    " where Name like '%items'";
$sdb = new AmazonSDB();
```

上述脚本使用 `select` 方法运行一个查询，该查询将返回所有 `Name` 属性包含字符串 *"items"* 的条目。然后，它将遍历所有返回的条目，并输出它们的属性及其值。如果数据库中包含代码归档中 `chapter_08` 文件夹内所有文件的文件信息，输出的示例如下：

```php
Sres = $sdb->select($query);
if (!$res->isOk())
{
    exit("Select operation failed\n");
}
foreach ($sres->body->SelectResult->Item as $Item)
{
    foreach ($Item->Attribute as $Attribute)
    {
        print($Attribute->Name . ": " . $Attribute->Value . ", ");
    }
    print("\n");
}
exit(0);
?>
```

```
$ php query_domain.php
Hash: a446a0c1d252042cf065e7bc4d743336, Name:
> augment_items.php, Size: 00001191,
Hash: 280434b0478b68eaceaf616329d337e, Name:
> batch_insert_items.php, Size: 00001337,
Hash: 49cb20ea103caeb654ce4aad307ecdc, Name:
> delete_items.php, Size: 00001003,
Hash: e77f57f95676ac156318123c44428c40, Name:
> insert_items.php, Size: 00000937,
```

默认情况下，`select` 调用每次返回 100 个条目（或 1MB 的数据，取两者中较小的值）。可以使用 `limit` 子句来请求返回多达 2,500 个条目，但总量仍限制在 1MB。

如果 `select` 调用因上述限制而无法返回所有条目，响应中将包含一个 `NextToken` 值。可以将此值传递给后续的重复 `select` 调用，以接收额外的结果。下面是一个假设的循环表示，它利用 `NextToken` 值进行重复的 `select` 调用，直到没有更多结果返回：

```php
$next = null;
do
{
```
