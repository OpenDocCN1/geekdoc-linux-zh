
此时你应该对代码结构很熟悉了。`list_distributions`方法返回一个对象数组，然后对其进行迭代并打印。不过请注意，我们实例化了一个新的`AmazonCloudFront`对象，而不是像前面的脚本那样使用`AmazonS3`对象，并使用`list_distributions`方法来获取分发的详细信息。

响应对象可以像我们之前的 S3 脚本一样进行查询。在返回给`list_distributions`方法的响应中，`$res->body->DistributionSummary`属性将包含一个`SimpleXMLElement`对象数组，每个 CloudFront 分发对应一个。上面的脚本只是遍历这个数组，并提取每个对象的 Id、DomainName 和 Origin 属性以便在输出中显示，格式化成类似于以下的表格：

![](img/4a5ba0dd041e08e6a67fa31d52309995_120_0.png)

当你使用你的 AWS 账户运行此脚本时，Id 和 Domain Name 列将显示唯一的值。

## 列出带有缩略图的 S3 文件

好吧，时候到了，这是本章的最后一个脚本！我们首先还需要一个额外的实用函数来使其工作：`findDistributionForBucket`函数，它将返回给定 S3 存储桶的 CloudFront 分发。你猜对了，我们将把它放在`book.inc.php`文件中：

```php
<!-- chapter_04/include/book.inc.php (excerpt) -->
function findDistributionForBucket($cf, $bucket)
{

    $res = $cf->list_distributions();

    if (!$res->isOK())
    {
        return null;
    }

    $needle = $bucket . ".";
    $distributions = $res->body->DistributionSummary;
```

```php
foreach ($distributions as $distribution)
{
    if (substr($distribution->Origin, 0, strlen($needle)) ==
        $needle)
    {
        return $distribution;
    }
}

return null;
```

此函数接受一个 CloudFront 访问对象和一个存储桶的名称。它会获取 CloudFront 分发列表，并尝试将每一个分发与给定的存储桶名称进行匹配。如果匹配成功，则返回该分发对象。

下面的代码是*list_bucket_objects_page.php*的增强版本，该文件在本章前面已经展示过。它为该存储桶中所有拥有对应缩略图存储桶中的图像的图像对象在表格中添加了缩略图。它还使用了可用的 CloudFront URL：

```php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$Bucket = IsSet($GET['bucket']) ? $_GET['bucket'] : BOOK_BUCKET;
$BucketThumbs = $Bucket . THUMB_BUCKET_SUFFIX;

$S3 = new AmazonS3();      #1
$Cf = new AmazonCloudFront();

$dist = findDistributionForBucket($Cf, $Bucket);      #2
$thumbsDist = findDistributionForBucket($Cf, $BucketThumbs);

$objects = getBucketObjects($S3, $Bucket);            #3
$objectThumbs = getBucketObjects($S3, $BucketThumbs);

$thumbs = array();      #4
foreach ($objectThumbs as $objectThumb)
{
    $key = (string) $objectThumb->Key;

    if ($thumbsDist != null)  #5
    {
        $thumbs[$key] = 'http://' . $thumbsDist->DomainName
            . '/' . $key;
    }
    else
    {
        $thumbs[$key] = $S3->get_object_url($BucketThumbs, $key);
    }
}

$fileList = array();  #6
foreach ($objects as $object)
{
    $key = (string) $object->Key;

    if ($dist != null)
    {
        $url = 'http://' . $dist->DomainName . '/' . $key;
    }
    else
    {
        $url = $S3->get_object_url($Bucket, $key);
    }

    $thumbURL = IsSet($thumbs[$key]) ? $thumbs[$key] : '';  #7
    $fileList[] = array('thumb' => $thumbURL, 'url' => $url,
        'name' => $key, 'size' => number_format((int)$object->Size));
}

$output_title = "Chapter 3 Sample - List of S3 Objects in Bucket"
    . " $Bucket";
$output_message = "A simple HTML table displaying of all the objects"
    . " in the $Bucket bucket with thumbnails.";

include 'include/list_bucket_objects_thumbs.html.php';

exit(0);
?>
```

让我们来看看这段代码：

- 首先，我们实例化新的`AmazonS3`和`AmazonCloudFront`对象。

- 在此我们确定每个存储桶是否都有 CloudFront 分发。

- 我们再次使用我们的`getBucketObjects`函数从两个存储桶中检索所有对象。

- 我们遍历缩略图存储桶中的所有对象，并使用对象键作为数组键来填充`$thumbs`数组，同时存储它们的 URL。

- 如果缩略图有 CloudFront 分发，我们就使用其 URL；否则，我们使用标准的 S3 URL。

- 我们对指定存储桶中的所有对象执行相同的操作；这些结果存储在`$fileList`数组中，并将用于 HTML 输出。

- 这是`list_bucket_objects_page.php`脚本中针对`$fileList`数组的新增部分。如果有匹配的缩略图，则保存缩略图 URL；否则存储空字符串。

这是生成输出的 HTML 模板：
