
## 在网页上列出存储桶中的对象

当然，你完全可以自由地使用中间变量，使这段代码更简短或更高效。

你或许会想知道对象名称（如 `Contents`、`Key`、`Size` 等等）是从哪里来的。`list_objects` 方法会向 S3 发送一个 HTTP GET 请求，以获取存储桶中前 1,000 个对象的列表。该请求返回一个 XML 文档，而 CloudFusion 会对其进行解析，并将其作为 body 对象返回。这些对象名称直接取自文档中的 XML 标签。

如果我们修改之前的脚本，打印出这些值中的一部分，它可能看起来像下面的例子：

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$S3 = new AmazonS3();
$res = $S3->list_objects(BOOK_BUCKET);

print("Bucket Url: " . $res->header['_info']['url'] . "\n");
print("Bucket Name: " . $res->body->Name   . "\n");
print("First Key: "   . $res->body->Contents[0]->Key . "\n");
print("Second Key: "  . $res->body->Contents[1]->Key . "\n");
exit(0);
?>
```

在上面的例子中，我们输出了存储桶的 URL 和名称，接着输出了存储桶中前两项的键（key）。

至此，这一“绕道”部分已经接近尾声。我希望这段旅程既风景优美，又富有教育意义。接下来，我们将运用这些新获得的知识，创建一个非常实用的工具函数。

在编写一个能在网页中输出存储桶内所有对象列表的脚本之前，我们必须先编写一个相当复杂的函数。我们将把这个函数添加到我们的 `book.inc.php` 文件中，并称之为 `getBucketObjects`：

**chapter_04/include/book.inc.php (节选)**

```php
function getBucketObjects(S3, $bucket, $prefix = '')
{
    $objects = array();
    $next = '';

    do {
        $res = $s3->list_objects($bucket,
            array('marker' => urlencode($next),
                'prefix' => $prefix)
        );

        if (!$res->isOk())
        {
            return null;
        }

        $contents = $res->body->Contents;
        foreach ($contents as $object)
        {
            $objects[] = $object;
        }

        $isTruncated = $res->body->IsTruncated == 'true';

        if ($isTruncated)
        {
            $next = $objects[count($objects) - 1]->Key;
        }
    } while ($isTruncated);

    return $objects;
}
```

这个函数比你目前见过的任何代码都要复杂，但无需担心。在本章早些时候我曾告诉你，向 S3 发出一次“列出存储桶”的请求，无论存储桶中有多少个键，最多只会返回 1,000 个键。我们的 `getBucketObjects` 函数只是不断调用 `list_objects`，直到 S3 表示没有其他对象需要返回为止：

- 我们的函数接受三个参数：一个 **AmazonS3** 对象、一个 S3 存储桶，以及一个默认值为空字符串的前缀（prefix）。
- 我们使用一个 **do ... while** 循环，以确保循环体至少执行一次。
- 每次我调用 `list_objects` 时，都会传入一个名为 `$next` 的值。在循环的第一次迭代中，`$next` 是空字符串，`list_objects` 会从存储桶的开头（按字母顺序）开始。在后续的循环迭代中，`$next` 会被设置为上一次迭代返回的最后一个键。这告诉 S3 从上一次迭代最后那个键的字母顺序之后开始检索键。
- 如果 `list_objects` 调用失败，该函数将返回 `null`。
- 我们从 `list_objects` 调用返回的响应 body 中获取 **Contents** 数组，然后遍历这些值，将每个值存储到 `$objects` 数组中。这个数组最终将成为我们的返回值。
- `list_objects` 调用返回的数据包含一个名为 `IsTruncated` 的元素。如果该值是字符串 "true"，则表示列表不完整，还有更多对象需要查找。这个条件也被用来控制循环。
- 如果列表不完整，我们就设置 `$next` 的值，为开始下一次迭代做准备。
- 当循环终止时，返回 `$objects` 数组。

把它们组合起来，这个函数就会获取存储桶中的所有对象，将它们全部放入一个数组中，并返回该数组。

![](img/4a5ba0dd041e08e6a67fa31d52309995_105_0.png)

### 避免无限循环

我坦率地承认，在我最初编写这段代码时，未能正确表述终止条件。我知道这会很有技巧性，因此我在顶部使用了一个打印语句，以确保我避免创建一个无法终止、失控运行并导致我的 S3 账单飙升的循环。我建议你在构建和测试任何需要付费执行的代码时，也这样做。

有了这个函数，创建存储桶中对象的列表就变得很容易了。以下是我们需要做的全部事情：

**chapter_04/list_bucket_objects_page.php (节选)**

```php
<?php
    error_reporting(E_ALL);

    require_once('cloudfusion.class.php');
    require_once('include/book.inc.php');

    $bucket = isset($_GET['bucket']) ? $_GET['bucket'] : BOOK_BUCKET;

    $S3 = new AmazonS3();

    $objects = getBucketObjects($S3, $bucket);

    $fileList = array();

    foreach ($objects as $object)
    {
        $key = $object->Key;
        $url = $S3->getObject_url($bucket, $key);
        $fileList[] = array('url' => $url, 'name' => $key,
        'size' => number_format((int)$object->Size));
    }

    $output_title = "Chapter 3 Sample - List of S3 Objects in Bucket '${bucket}'";
    $output_message = "A simple HTML table displaying of all the 'objects in the '${bucket}' bucket.";
    include 'include/list_bucket_objects.html.php';

    exit(0);
?>
```

这段代码生成一个网页，并且可以接受 URL 查询字符串中可选的存储桶参数。让我们拆解一下，看看它是如何工作的：

- 这段代码检查是否提供了存储桶参数。如果提供了，则将其用作 `$bucket` 的值。否则，使用默认值，即 `BOOK_BUCKET` 常量。
- 在这里，我们调用自定义的 `getBucketObjects` 函数，该函数获取给定存储桶中的对象列表，并将其存储在 `$objects` 数组中。
- 下一步是遍历该数组并处理每一个元素。
- 我们在 `$fileList` 数组中为每个对象存储三个值：对象的 URL、键（我们将其存储为 name）以及大小（转换为整数并格式化为数字）。
- 我们包含 HTML 模板，以输出 `$fileList` 数组中的值。

以下是 `list_bucket_objects.html.php` HTML 模板的样子：

**chapter_04/include/list_bucket_objects.html.php (节选)**

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<title><?php echo $output_title ?></title>
</head>
<body>
<h1><?php echo $output_title ?></h1>
<p><?php echo $output_message ?></p>
<table>
<thead>
<tr><th>File</th><th>Size</th></tr>
</thead>
<tbody>
<?php foreach($fileList as $file): ?>
<tr>
<td><a href="<?php echo $file['url'] ?>" ?>
<?php echo $file['name'] ?></a>
</td>
<td><?php echo $file['size'] ?></td>
</tr>
<?php endforeach ?>
</tbody>
</table>
</body>
</html>
```

该模板遍历 `$fileList` 数组，并为每个文件创建一个表格行，在第一列放置指向该文件的链接，在第二列放置文件大小。

