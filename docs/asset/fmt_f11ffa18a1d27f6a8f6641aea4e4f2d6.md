
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

图 4.2 展示了其运行效果（我当时已经向存储桶上传了一些文件）。

| 图像文件 | 大小 |
| :--- | :--- |
| images/2008_chiller_bouquet_protection.jpg | 236,535 |
| images/3DoorStore.jpg | 61,918 |
| images/AndyBass.jpg | 73,388 |
| images/AndyWolkOrchard.jpg | 80,841 |
| images/FifthBase.gif | 37,561 |
| images/FifthBase.psd | 545,419 |
| images/FifthBaseTonight.psd | 37,452 |
| images/FifthBaseBright.psd | 532,308 |
| images/STP-65708.JPG | 1,716,926 |
| images/Scon XB Stretch.jpg | 66,598 |
| images/Scon XB.jpg | 70,882 |

图 4.2. 列出 S3 存储桶中的对象

你可能已经注意到，现在我们拥有了构建一个简单的 S3 文件浏览器的所有组件。我将把实现这个功能作为你的挑战。只需稍加努力，你应该能够将 `list_buckets_page.php` 和 `list_bucket_objects_page.php` 连接起来。

## 向 S3 上传文件

既然我们已经知道如何从 S3 获取关于存储桶及其对象的信息，让我们来看看如何将新对象放入 S3。这相当简单；我们只需要再添加两个实用函数到我们的 `book.inc.php` 文件中。

第一个函数名为 `uploadObject`：

```php
// chapter_04/include/book.inc.php (excerpt)

function uploadObject($s3, $bucket, $key, $data,
    $acl = S3_ACL_PRIVATE, $contentType = "text/plain")
{
    $res = $s3->create_object($bucket,
        array(
            'filename'    => $key,
            'body'        => $data,
            'acl'         => $acl,
            'contentType' => $contentType
        ));
    return $res->isOk();
}
```

`uploadObject` 函数接受四到六个参数。前四个参数指定 S3 访问对象、目标存储桶、所需的对象键以及要存储在对象中的数据。最后两个参数指定非默认的 ACL 以及存储对象的内容类型。

Web 浏览器使用对象的内容类型来确定如何显示该对象。例如，`image/png` 的内容类型告诉浏览器该对象是一个图像，且格式为 PNG。

如你所见，`uploadObject` 函数只是调用了 `create_object` 方法，并检查返回值以确保对象实际上已存储在 S3 中。

如果 S3 无法存储对象，它将返回 HTTP 500（内部服务器错误）代码。这几乎总是一个可恢复的状态；正确的响应是进行多次尝试，且每次尝试之间增加时间延迟（有时称为指数退避）。以下是 `uploadObject` 函数更复杂的版本，带有重试机制：

```php
function uploadObject($s3, $bucket, $key, $data,
    $acl = S3_ACL_PRIVATE, $contentType = "text/plain")
{
    $try = 1;
    $sleep = 1;
    do
    {
        $res = $s3->create_object($bucket,
            array(
                'filename'    => $key,
                'body'        => $data,
                'acl'         => $acl,
                'contentType' => $contentType
            ));
        if ($res->isOk()) {
            return true;
        }
        sleep($sleep);
        $sleep *= 2;
    } while(++$try < 6);
    return false;
}
```

我们函数的这个版本将尝试最多六次在存储桶中创建新对象。每次尝试时，暂停时长（下一次尝试之前）都会翻倍。

我们的下一个函数帮助我们确定文件的内容类型：

```php
// chapter_04/include/book.inc.php (excerpt)

function guessType($file)
{
    $info = pathinfo($file, PATHINFO_EXTENSION);
    switch (strtolower($info))
    {
        case "jpg":
        case "jpeg":
            return "image/jpg";
        case "png":
            return "image/png";
        case "gif":
            return "image/gif";
        case "htm":
        case "html":
            return "text/html";
        case "txt":
            return "text/plain";
        default:
            return "text/plain";
    }
}
```

给定一个文件名，此函数使用文件扩展名对文件的内容类型进行非常简单的猜测。它完全不会检查文件的内容，并且假设文件扩展能准确反映文件内容。为了在本章中发挥作用，该函数仅处理少数几种类型。

将所有这些与参数处理、循环和错误检查结合在一起，我们就有了一个方便上传一个或多个文件到 S3 的命令：
