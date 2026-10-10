
我们将使用 PHP Simple HTML DOM Parser³ 来解析 HTML。从该网站下载文件，并将其放入你的 **include** 文件夹中。脚本的设置和循环框架如下所示：

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/simple_html_dom.php');
require_once('include/book.inc.php');

$sqs = new AmazonSQS();
$s3 = new AmazonS3();

while (true)
{
    $message = pullMessage($sqs, $queueParse);

    if ($message != null)
    {
        : process the message...
    }
}
?>
```

让我们来看看从解析队列中提取的每条消息在循环内部发生了什么。第一步是访问 S3 中的页面。解析器允许我们将获取和解析结合起来，所以这非常简单：

```php
$messageDetail = $message['MessageDetail'];
$receiptHandle = (string)$message['ReceiptHandle'];
$pageURL       = $messageDetail['Data'];

print("Processing URL `${pageURL}`\n");
$dom = new simple_html_dom();
$dom->load_file($pageURL);
```

³ http://simplehtmldom.sourceforge.net/

使用 DOM，定位和处理单独的 HTML 标签或标签集合非常容易。以下是如何提取页面标题的方法：

```php
$pageTitle = $dom->find('title', 0)->innertext();
print(" Retrieved page '$pageTitle'\n");
```

这是一个很有用的值，因此我们将把它保存在 `$pageTitle` 变量中，以便我们可以在处理管道中传递它。

现在是时候处理图像链接了。我们将捕获最多 16 个链接：

```php
$imageURLs = array();
foreach ($dom->find('img') as $image)
{
    $imageURL = $image->src;
    if (preg_match('/^http:\/*', $imageURL))
    {
        print(" Found absolute URL '$imageURL'\n");
        $imageURLs[] = $imageURL;
        if (count($imageURLs) == 16)
        {
            break;
        }
    }
}
```

在上面的代码中，表达式 `$dom->find('img')` 检索一个包含页面中所有 HTML `<img/>` 标签的数组。表达式 `$image->src` 从标签中检索 `src` 属性；这是图像的 URL。

如果 URL 以字符串 "http://" 开头，它将被添加到 `$imageURLs` 数组中。当数组中有 16 张图像时，循环终止。

此时，我们拥有一个最多包含 16 个图像 URL 的数组，准备发送到下一阶段，即图像获取器。现在是时候构建消息了，如下所示：

```php
if (count($imageURLs) > 0)
{
  $Origin      = $messageDetail['Origin'];
  $History    = $messageDetail['History'];
  $History[]  = 'Processed by ' . $argv[0] . ' at ' . date('c');

  $message = json_encode(array('Action'   => 'FetchImages',
                               'Origin'   => $Origin,
                               'Data'     => $imageURLs,
                               'History'  => $History,
                               'PageTitle'=> $pageTitle));

  $res = $sqs->send_message(IMAGE_QUEUE, $message);
  print("  Sent page to image fetcher\n");

  if ($res->isOk())
  {
    $sqs->delete_message(PARSE_QUEUE, $receiptHandle);
    print("  Deleted message from parse queue\n");
  }

  print("\n");
}
```

这段代码代表了我们循环内部的最后一部分。如果解析器找到了任何图像，我们就构造一个到图像获取队列的消息，将图像 URL 数组作为消息数据传递，并且包括页面标题，因为我们稍后可以将其用于其他地方。

此时，我们已经解析了页面。我们提取了图像标题，并定位了最多 16 张图像的 URL。图像获取器将获得它完成工作所需的所有内容。

## 阶段 3：获取图像 URL

现在是时候构建第三个阶段了。这个阶段将使用现在已经熟悉的处理循环。该阶段从上一阶段接收图像 URL 数组，并获取每一个。然后使用我们在第 4 章中编写的 `thumbnailImage` 函数将图像缩放到 `THUMB_SIZE` 常量定义的小尺寸。

此时你也许可以自己编写该阶段的代码，但我们还是简单看一下。与前几个阶段一样，我们获取所需队列的引用并开始循环：

```php
#!/usr/bin/php
<?php
error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$sqs = new AmazonSQS();
$s3 = new AmazonS3();

while (true)
{
  $message = pullMessage($sqs, $queueFetch);

  if ($message != null)
  {
    : process the message...
  }
}
?>
```

在循环内部，代码从队列消息中读取图像 URL 数组，获取所有图像，并将它们存储在 S3 中：

```php
$messageDetail = $message['MessageDetail'];
$receiptHandle = (string)$message['ReceiptHandle'];
$imageURLs     = $messageDetail['Data'];

print ("Processing message with " .
       count($imageURLs) .
       " images:\n");

$s3ImageKeys = array();
foreach ($imageURLs as $imageURL)
{
    print(" Fetch image '$imageURL'\n");
    $image = file_get_contents($imageURL);
    print(" Retrieved " . strlen($image) . " byte image\n");

    $imageThumb = thumbnailImage($image, 'image/png');

    $key = 'image_' . md5($imageURL) . '.png';

    if (uploadObject($s3, BOOK_BUCKET, $key, $imageThumb))
    {
        print( " Stored image in S3 using key '$key'\n");
        $s3ImageKeys[] = $key;
    }
}
```

上述代码使用 `file_get_contents` 函数下载图像，使用我们的 `thumbnailImage` 函数创建缩略图，并使用我们的 `uploadObject` 函数将新的图像缩略图上传到 S3 存储桶。

然后，消息按照常规方式沿管道传递：

```php
if (count($imageURLs) == count($s3ImageKeys))
{
    $origin    = $messageDetail['Origin'];
    $history   = $messageDetail['History'];
    $pageTitle = $messageDetail['PageTitle'];

    $history[] = 'Processed by ' . $argv[0] . ' at ' . date('c');

    $message = json_encode(array('Action'    => 'RenderImages',
                                 'Origin'    => $origin,
                                 'Data'      => $s3ImageKeys,
                                 'History'   => $history,
                                 'PageTitle' => $pageTitle));

    $res = $sqs->send_message(RENDER_QUEUE, $message);
    print(" Sent page to image renderer\n");

    if ($res->isOk())
    {
        $sqs->delete_message(IMAGE_QUEUE, $receiptHandle);
        print(" Deleted message from fetch queue\n");
    }

    print("\n");
}
```

$s3ImageKeys 数组存储了我们所有缩略图的键，因此我们测试缩略图键的数量是否与我们正在处理的图像数量相匹配。如果匹配，意味着我们已成功处理所有图像，并且该网站的消息可以发送到下一个队列。如果消息成功发送到下一个队列，图像获取队列中的消息就可以被删除。

我们的爬虫现在已完成四分之三；只剩下最后一个阶段。

## 阶段 4：渲染图像

第四个也是最后一个阶段获取 S3 对象键，在生成缩略图马赛克图像之前先从 S3 获取每个对象。此代码使用了 PHP 的 GD 库中的许多函数。

设置和循环框架与其他阶段几乎相同，除了我们创建了一组常量来控制重新渲染过程，并且只需要引用一个队列。由于这是最后一个阶段，没有更多的队列来发送消息：

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

define('BORDER_LEFT' , 12);
define('BORDER_RIGHT', 12);
define('BORDER_TOP'  , 12);
define('BORDER_BOTTOM', 12);
define('IMAGES_ACROSS', 4);
define('IMAGES_DOWN'  , 4);
define('GAP_SIZE'     , 6);

$sqs = new AmazonSQS();
```

