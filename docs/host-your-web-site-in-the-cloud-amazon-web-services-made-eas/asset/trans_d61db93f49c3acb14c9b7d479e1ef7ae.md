
# 编程 Amazon SimpleDB

在本节中，您将看到如何使用 CloudFusion 来访问 SimpleDB 的所有功能。由于 CloudFusion 已经包含了对 Amazon SimpleDB 的支持，我们可以直接进入代码部分。

我们将创建域并列出它们，然后向其中填充项目。接下来，我们将看到如何处理数值数据并运行一些查询。我们将使用额外数据更新现有项目，然后删除某些项目和项目属性。我们将了解如何监控域统计信息，最后以一个现实世界的示例收尾：在 SimpleDB 中获取、解析和存储 RSS 源。

在本章中，我将使用三个 SimpleDB 域。以下是我们将添加到 **book.inc.php** 中的定义：

```php
chapter_08/include/book.inc.php (excerpt)

define('BOOK_FILE_DOMAIN', 'files');
define('BOOK_FEED_DOMAIN', 'feeds');
define('BOOK_FEED_ITEM_DOMAIN', 'feed_items');
```

**BOOK_FILE_DOMAIN** 将用于存储关于文件的信息。

**BOOK_FEED_DOMAIN** 将用于存储关于 RSS 源的信息，而 **BOOK_FEED_ITEM_DOMAIN** 将用于存储关于在 RSS 源中发现的项的信息。

在开始使用 SimpleDB 之前，您需要注册 SimpleDB。只需访问该网站并点击 **Sign Up for Amazon SimpleDB** 按钮。

## 创建域

下面是一个脚本，它创建了本章示例所需的所有 SimpleDB 域：

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$sdb = new AmazonSDB();

foreach (array(BOOK_FILE_DOMAIN,
               BOOK_FEED_DOMAIN,
               BOOK_FEED_ITEM_DOMAIN) as $domain)
{
    $res = $sdb->create_domain($domain);
    if (!$res->isOk())
    {
        exit("Create domain operation failed for domain ${domain}\n");
    }

    print("Domain ${domain} created.\n");
}
exit(0);
?>
```

该程序简单地创建了一个新的 AmazonSDB 对象，遍历一个域名数组，并对每个域调用 `create_domain` 方法。如果域已经存在，`create_domain` 将不执行任何操作（并返回成功结果）。

如果您想接受挑战，您应该能够轻松修改上述脚本以接受命令行输入的新域名。

## 列出域

下一步是列出域。以下是执行此操作的方法：

```php
chapter_08/list_domains.php (excerpt)
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
$db = new AmazonSDB();
$res = $db->list_domains();
if (!$res->isOk())
{
    exit("List domain operation failed\n");
}
foreach ($res->body->ListDomainsResult->DomainName as $domainName)
{
    print($domainName . "\n");
}
exit(0);
?>
```

`list_domains` 方法返回一个域名数组。代码遍历列表并打印每一个。

以下是该命令的输出：

```bash
$ php list_domains.php
feed_items
feeds
files
```

## 存储数据

下一步是在域中存储一些数据。这是使用 `put_attributes` 方法完成的。该方法可用于创建新项目或为现有项目添加额外属性。

以下程序为当前目录中每个文件名匹配正则表达式 `/^[a-zA-Z0-9_]+\.php$/` 的文件创建一个项目——即所有名称合理的 PHP 文件。它使用文件名作为项目名称，并创建三个属性：

- **Name**（文件名）
- **Hash**（文件内容的 MD5 哈希值）
- **Size**（文件的字节大小）

以下是代码：

```php
chapter_08/insert_items.php (excerpt)
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$ssdb = new AmazonSDB();

$dir = opendir(".");
while (($file = readdir($dir)) !== false) {   // 1
    if (preg_match("/^[a-zA-Z0-9_]+\.php$/", $file)) {   // 2
        $data = file_get_contents($file);   // 3
        $hash = md5($data);
        $size = filesize($file);

        $attrs = array('Name' => $file,
                       'Hash' => $hash,
                       'Size' => $size);

        $res = $ssdb->put_attributes(BOOK_FILE_DOMAIN, $file,
                                     $attrs, true);   // 4
        if ($res->isOk())
        {
            print("Inserted item $file\n");
        }
        else
        {
            $error = $res->body->Errors->Error->Message;
            print("Could not insert item: ${error}\n");
        }
    }
}

closedir($dir);
exit(0);
?>
```

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
