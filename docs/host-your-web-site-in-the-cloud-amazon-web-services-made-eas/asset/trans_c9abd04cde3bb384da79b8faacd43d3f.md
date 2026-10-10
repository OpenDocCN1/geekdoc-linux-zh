

<dev>: wget -q http://169.254.169.254/latest/meta-data/instance-id
<dev>: wget -q http://169.254.169.254/latest/meta-data/public-ipv4
<dev>: wget -q http://169.254.169.254/latest/meta-data/placement/availability-zone

请注意，这些请求（以及所有其他用于获取实例元数据的请求）必须从实例内部发出。以下是获取到的元数据：

<dev>: cat public-ipv4
174.129.84.219
<dev>: cat instance-id
i-d830dfb0
<dev>: cat availability-zone
us-east-1b

启动 EC2 实例时，您还可以提供自己的元数据。这种数据称为用户数据。AWS 管理控制台、ElasticFox 工具以及 `ec2-run-instances` 命令行工具都提供了指定此数据的方法。如 **图 10.4** 所示，AWS 管理控制台将此功能作为高级选项支持。

![](img/4a5ba0dd041e08e6a67fa31d52309995_343_0.png)

**图 10.4** 带有用户数据启动 EC2 实例

在此示例中，“Role=Server,Size=Small,Name=MainServer,Input=Queue1” 是我用户数据中包含的字符串。在实例启动后立即检索此信息，并利用它来控制实例的行为。

启动后，可以按以下方式获取用户数据：

<dev> wget -q http://169.254.169.254/latest/user-data
<dev> cat user-data
Role=Server,Size=Small,Name=MainServer,Input=Queue1

当然，我们还可以使用简单的 PHP 程序来获取和处理用户元数据：

chapter_10/ec2_user_data.php (摘录)

#!/usr/bin/php
<?php

$userData = file_get_contents(
        'http://169.254.169.254/latest/user-data');
$options = array();

foreach (explode(",", $userData) as $userDataItem)
{
    if (preg_match("!^([a-zA-Z]{1,})=([a-zA-Z0-9]{1,})$!",
            $userDataItem, $parts))
    {
        $name  = $parts[1];
        $value = $parts[2];

        $options[$name] = $value;
    }
}

print_r($options);
?>

`file_get_contents` 函数用于获取用户元数据。字符串使用 PHP 的 `explode` 函数在逗号边界处进行分割，生成形式为 `Role=Server` 的名称-值对。

您可以随心所欲地使用用户元数据功能。您可以传递服务器名称、服务器角色、SQS 队列名称、大小、限制等。您需要创建自己的 AMI。更进一步，您可以让自定义 AMI 将用户元数据视为实例启动时应运行的脚本的 URL。

# 动态制图

在本节中，我们将使用 EC2 API 获取正在运行的实例列表、附加到每个实例的 EBS 卷以及这些实例的快照，并绘制一个简单的系统图。你应该能够轻松地扩展这个程序，使其具备多种不同的功能。

让我们开始吧。应用程序将进行大量绘图。我在方格纸上勾勒了布局，并将关键尺寸编码为 PHP 常量：

chapter_10/ec2_diagram.php (摘录)

#!/usr/bin/php
<?php

error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

// Define shape geometry
define('LEFT_MARGIN', 16);
define('RIGHT_MARGIN', 16);
define('TOP_MARGIN', 16);
define('BOTTOM_MARGIN', 16);
define('TEXT_MARGIN', 4);
define('TEXT_LINE_HEIGHT', 14);
define('INSTANCE_WIDTH', 128);
define('INSTANCE_HEIGHT', 64);
define('VOLUME_WIDTH', 96);
define('VOLUME_HEIGHT', 64);
define('SNAP_WIDTH', 96);
define('SNAP_HEIGHT', 64);
define('VOLUME_GAP', 16);
define('SNAP_GAP', 16);

我决定将每个正在运行的 EC2 实例、附加到实例的 EBS 卷以及每个卷的快照表示为一系列连接的矩形。

实例垂直堆叠，卷水平排列在一行，快照垂直排列在一列。**图 10.5** 显示了我的草图整理后的版本。

![](img/4a5ba0dd041e08e6a67fa31d52309995_346_0.png)

每个实例及其相关部分在最终图像中占据一个矩形空间，周围由 `LEFT_MARGIN`、`RIGHT_MARGIN`、`TOP_MARGIN` 和 `BOTTOM_MARGIN` 表示的边距包围。实例、卷和快照分别绘制为尺寸为 `INSTANCE_WIDTH` 乘 `INSTANCE_HEIGHT`、`VOLUME_WIDTH` 乘 `VOLUME_HEIGHT` 和 `SNAP_WIDTH` 乘 `SNAP_HEIGHT` 的矩形。`TEXT_MARGIN` 在矩形边缘和内部文本之间留出了一些空间，而 `TEXT_LINE_HEIGHT` 是文本行之间的空间。`VOLUME_GAP` 是卷矩形之间的水平空间，`SNAP_GAP` 是快照矩形之间的垂直空间。

一如既往，我们需要创建允许我们访问 EC2 和 S3 的对象：

chapter_10/ec2_diagram.php (摘录)
$ec2 = new AmazonEC2();
$s3 = new AmazonS3();

接下来，我们按以下方式获取 EC2 实例、EBS 卷和 EBS 卷快照的列表：

chapter_10/ec2_diagram.php (摘录)
$resInstances = $ec2->describe_instances();
$resVolumes = $ec2->describe_volumes();
$resSnapshots = $ec2->describe_snapshots();

这个微小的代码片段检索了我们系统配置的所有重要信息。在继续之前检查错误总是有益的，所以现在让我们这样做：

chapter_10/ec2_diagram.php (摘录)
if (!$resInstances->isOk() ||
    !$resVolumes->isOk() ||
    !$resSnapshots->isOk())
{
    exit("Error retrieving system information.");
}

与本书中大多数其他（且更简单）的程序不同，我这里采用的是面向对象的方法。我创建了表示 EC2 区域、实例、卷和快照的类。每个类都包含对其逻辑上拥有或包含的对象的引用：

- 区域包含实例
- 实例包含卷
- 卷包含快照

我选择省略关于未附加到实例的卷的信息或关于不存在的卷的快照的信息（这些是完全合法的情况）。

Region 是顶层对象，因此首先创建它：

chapter_10/ec2_diagram.php (摘录)
$Region = new Region('us-east-1');

接下来，我们可以遍历实例列表，收集每个实例的感兴趣属性，使用它们创建 Instance 对象，然后将新对象添加到 Region。以下是执行此操作的方法：

chapters/10/ec2_diagram.php (摘录)

foreach ($resInstances->body->reservationSet->item as $itemSet)
{
    foreach ($itemSet->instancesSet->item as $item)
    {
        $instanceId        = (string) $item->instanceId;
        $state             = (string) $item->instanceState->name;
        $instanceType      = (string) $item->instanceType;
        $availabilityZone  = (string) $item->placement->availabilityZone;

        if ($state != 'terminated')
        {
            $Region->AddInstance(new Instance($availabilityZone,
                $instanceId,
                $state,
                $instanceType));
        }
    }
}

代码跳过处于 `terminated` 状态的实例，因为它们已被关闭。

接下来，我们可以对每个 EBS 卷执行类似的处理：

chapters/10/ec2_diagram.php (摘录)

foreach ($resVolumes->body->volumeSet->item as $item)
{
    $volumeId        = (string) $item->volumeId;
    $size            = (string) $item->size;
    $availabilityZone = (string) $item->availabilityZone;

    if ($item->attachmentSet->item)
    {
        $instanceId = (string) $item->attachmentSet->item->instanceId;
        $device     = (string) $item->attachmentSet->item->device;

        $Region->AddVolume(new Volume($availabilityZone,
            $volumeId,
            $instanceId,
            $size,
            $device));
    }
}

对每个快照也是同样的处理：

chapter_10/ec2_diagram.php (摘录)

foreach ($resSnapshots->body->snapshotSet->item as $item)
{
    $snapshotId = (string) $item->snapshotId;
    $volumeId   = (string) $item->volumeId;
    $startTime  = (string) $item->startTime;

    $Region->AddSnapshot(new Snapshot($snapshotId,
        $volumeId,
        $startTime));
}

此时，数据结构已经构建完成。如果你想自己看看它是什么样子的，可以像这样将其输出：

print_r($Region);

我的 Region 类有一个 Draw 方法。该方法使用 GD 库将实例、卷和快照渲染到内存图像中，然后返回该图像：

chapter_10/ec2_diagram.php (摘录)

$image = $Region->Draw();

最后一步是将内存图像以 GIF 格式写入文件系统，将 GIF 读入内存，然后将其存储在 Amazon S3 中：

chapter_10/ec2_diagram.php (摘录)

$imageOut = tempnam("/tmp", "aws") . ".gif";
ImageGIF($image, $imageOut);

$imageOutBits = file_get_contents($imageOut);

