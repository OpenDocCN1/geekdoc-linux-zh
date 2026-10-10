
```php
$s3 = new AmazonS3();

while (true)
{
    $Message = pullMessage($sqs, RENDER_QUEUE);

    if ($Message != null)
    {
        ...process the message...
    }
}
```

以**BORDER_**开头的常量用于控制主图像与缩略图之间各边缘的空隙大小。**IMAGES_ACROSS**和**IMAGES_DOWN**用于控制马赛克网格中图像的数量。**GAP_SIZE**则是缩略图之间的空隙大小。

循环内的代码以常规方式开始——从队列中检索消息数据——然后创建基础马赛克图像。使用这些常量来确定最终图像的大小：

```php
chapter_06/render_images.php (excerpt)

$MessageDetail = $Message['MessageDetail'];
$ReceiptHandle = (string)$Message['ReceiptHandle'];
$imageKeys     = $MessageDetail['Data'];
$PageTitle     = $MessageDetail['PageTitle'];

print("Processing message with " .
      count($imageKeys)
      . " images:\n");

$outX = BORDER_LEFT + BORDER_RIGHT +
       (IMAGES_ACROSS * THUMB_SIZE) +
       ((IMAGES_ACROSS - 1) * GAP_SIZE);

$outY = BORDER_TOP + BORDER_BOTTOM +
       (IMAGES_DOWN * THUMB_SIZE) +
       ((IMAGES_DOWN - 1) * GAP_SIZE);

$imageOut = ImageCreateTrueColor($outX, $outY);
```

图像填充为白色，并带有黑色边框：

```php
chapter_06/render_images.php (excerpt)

ImageFill($imageOut, 0, 0, ImageColorAllocate($imageOut, 255, 255, 255));
ImageRectangle($imageOut, 0, 0,
$outX - 1, $outY - 1, ImageColorAllocate($imageOut, 0, 0, 0));
```

我们需要跟踪下一个缩略图将被绘制的位置。我们将使用`$nextX`和`$nextY`来实现这一点，并初始将其设置为左上角：

```php
chapter_06/render_images.php (excerpt)

$nextX = BORDER_LEFT;
$nextY = BORDER_TOP;
```

现在我们必须依次处理每个缩略图，因此我们将遍历一组 S3 键，如下所示：

```php
chapter_06/render_images.php (excerpt)

foreach ($imageKeys as $imageKey)
{
```

有了这种基础结构，检索每个缩略图并将其绘制到目标图像上就变得很容易了：

```php
chapter_06/render_images.php (excerpt)

print(" Fetch image '{$imageKey}'\n");
$image = $s3->get_object(BOOK_BUCKET, $imageKey);

$imageBits = ImageCreateFromString($image->body);

print(" Render image at ${nextX}, ${nextY}\n");
ImageCopy($imageOut, $imageBits, $nextX, $nextY,
0, 0, ImageSX($imageBits), ImageSY($imageBits));
```

为了使图像看起来更美观，我们还会在每个缩略图周围绘制一个边框：

```php
chapter_06/render_images.php (excerpt)

ImageRectangle($imageOut, $nextX, $nextY,
                $nextX + ImageSX($imageBits),
                $nextY + ImageSY($imageBits),
                ImageColorAllocate($imageOut, 0, 0, 0));
```

处理每个缩略图时的最后一步是更新输出位置，这就结束了我们的`foreach`循环：

```php
chapter_06/render_images.php (excerpt)

$nextX += THUMB_SIZE + GAP_SIZE;
if (($nextX + THUMB_SIZE) > $outX)
{
    $nextX = BORDER_LEFT;
    $nextY += THUMB_SIZE + GAP_SIZE;
}
```

一旦所有缩略图都重新渲染完毕，我们就可以将最终图像上传到 S3：

```php
chapter_06/render_images.php (excerpt)

$imageFileOut = tempnam('/tmp', 'aws') . '.png';
ImagePNG($imageOut, $imageFileOut, 0);
$imageBitsOut = file_get_contents($imageFileOut);
unlink($imageFileOut);

$key = 'page_image_' . md5($pageTitle) . '.png';

if (uploadObject($s3, BOOK_BUCKET, $key, $imageBitsOut,
       S3_ACL_PUBLIC))
{
```

只剩下一点清理工作，我们就完成了。首先，我们需要报告最终图像的位置。然后必须删除消息，我们还可以显示随着消息从阶段到阶段移动而维护的处理历史：

```php
chapter_06/render_images.php (excerpt)
print(" Stored final image in S3 using key '${key}'\n");
print_r($messageDetail['History']);

$sqs->delete_message($queueRender, $receiptHandle);
print(" Deleted message from render queue\n");
}

print("\n");
```

以下是消息历史的一个示例：

```
Array(
  [0] => Posted by load_crawl_urls.php at 2009-06-29T09:28:10-04:00
  [1] => Fetched by fetch_page.php at 2009-06-29T09:28:11-04:00
  [2] => Processed by parse_page.php at 2009-06-29T09:28:12-04:00
  [3] => Processed by fetch_images.php at 2009-06-29T09:28:15-04:00
)
```

你可以看到消息在每个阶段停留了多长时间。该输出是我将 URL http://www.sitepoint.com 通过我们的处理流水线运行时生成的。图 6.7 显示了它生成的图像。

![](img/4a5ba0dd041e08e6a67fa31d52309995_203_0.png)

最终图像代表了四个处理阶段和加载程序的协作工作。每个阶段可以以自己的速度运行，工作项会在队列中按需积累。该应用程序可以轻松扩展以每分钟处理数十甚至数百个请求，而不会遇到太多麻烦。

### 运行代码

如果你想运行本章中的代码，你需要擅长窗口操作。首先，创建五个终端窗口——每个窗口代表一个阶段，最后一个窗口用于加载 URL。连接到你的 AMI，并在每个窗口中运行一条命令。如果可能，请按顺序排列窗口，以便你可以看到处理流水线的运行情况。以下是你需要做的：

- 1. 窗口 1——获取并存储页面：

```
<dev> php fetch_page.php
```

- 2. 窗口 2——解析页面：

```
<dev> php parse_page.php
```

- 3. 窗口 3——获取缩略图：

```
<dev> php fetch_images.php
```

- 4. 窗口 4——渲染最终图像：

```
<dev> php render_images.php
```

- 5. 窗口 5——将 URL 加载到流水线中。你可以连接到你的 AMI 或在本地执行此操作：

```
$ php load_crawl_urls.php http://www.sitepoint.com
```

一旦启动此命令，你将看到流水线的每个阶段依次开始运行。你可以多次运行此命令，或者直接在命令行列出多个 URL。

你随时也可以运行`crawl_queue_status.php`命令来检查队列状态：

```
$ php crawl_queue_status.php
```

你可能还喜欢尝试同时运行每个流水线阶段的多个副本。阶段 3 是一个很好的候选对象，因为它需要几秒钟时间来下载图像、生成缩略图并将缩略图上传到 S3。

当你完成流水线操作后，务必回到窗口 1 到 4，使用**ctrl+c**终止每个处理阶段。这样可以避免无故产生 SQS 请求费用。

### 总结

Amazon SQS 是一项简单而强大的服务。一旦你掌握了队列和消息的基础知识，就可以像我们刚才看到的那样，用一种全新的方式构建程序。

在本章中，我们将一个流程分解为几个部分，并将每个部分实现为独立程序，使用 Amazon SQS 队列连接这些程序。在编写这本书时，程序实际上是被分小块构建和测试的。事实上，我在编写章节相应部分时，就写好了每个阶段的代码。我让消息一直停留在队列中，直到代码准备就绪。

本章讨论的架构模型将允许你构建大型、复杂且高度可扩展的应用程序。一如既往，在前期设计上投入一些时间将在实现和运行时带来可观的收益。

# EC2 监控、自动缩放和弹性负载均衡

在本章中，你将学习如何使用三个强大的 Amazon EC2 功能：监控、自动缩放和弹性负载均衡。你将看到这些功能如何单独或一起使用来构建可扩展且强大的 Web 应用程序。在过程中，你还将学习如何利用 CloudFusion 库来使用这些功能。然后，我们会短暂偏离主题，学习如何使用 Apache JMeter 应用程序生成可预测的测试负载。最后，我们将通过学习如何对实际应用程序进行负载测试来结束本章，以确保它按预期进行扩展。

## 引言

Amazon EC2 服务的监控、自动缩放和弹性负载均衡功能让你能够轻松按需访问曾经需要复杂系统架构和大量硬件投资才能具备的能力。

任何实际的 Web 应用程序都必须具备扩展能力。这可以表现为**垂直扩展**，即引入更大、容量更高的服务器
