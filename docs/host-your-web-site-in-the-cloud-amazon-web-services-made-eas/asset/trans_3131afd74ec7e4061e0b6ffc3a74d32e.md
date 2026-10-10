

出于惯例，这些设备通常位于 /dev 目录下，并且以 sd 开头的名称命名，后面紧跟另一个字母。EC2 系统磁盘是 /dev/sda，其他本地磁盘（在较大规格的实例上）则是 sdb、sdc，以此类推。/dev/sdf 是附加到实例的第一个 EBS 卷的良好设备名称（因为“f”在字母表中靠后，足以避免与其他设备冲突）。以下是附加方法：

```
$ ec2-attach-volume vol-73d4211a -i i-da8f6db2 -d /dev/sdf
ATTACHMENT vol-73d4211a i-da8f6db2 /dev/sdf
attaching 2009-08-20T19:26:08+0000
```

该命令接受卷 ID，接着是 -i 和实例 ID，以及 -d 和设备名称。卷的状态会变为“attaching”（附加中）。它会保持此状态几秒钟，然后过渡到“attached”（已附加）：

```
$ ec2-describe-volumes vol-73d4211a
ATTACHMENT vol-73d4211a i-da8f6db2 /dev/sdf
attached 2009-08-20T19:26:12+0000
```

至此，我们已经完成了云计算中相当于采购磁盘驱动器、将其插入服务器并连接数据线缆的操作。磁盘在物理上已连接并正在运行；操作系统感知到了它，但磁盘是原始的（未格式化的），尚未成为文件系统的一部分。

下一步是在新卷上创建文件系统和一个挂载点（attachment），并在逻辑上将卷挂载到实例的根文件系统上。我们将遵循第 5 章“创建 EBS 卷”一节中的相同步骤（你需要登录到你的 EC2 实例来运行这些命令）：

```
<dev>: mkfs -F /dev/sdf
<dev>: mkdir /data
<dev>: mount /dev/sdf /data
```

你可以在实例文件系统的任何位置挂载 EBS 卷。如果你计划创建和使用大量卷，你应该花时间预先规划好逻辑命名结构。

卷现在已准备好使用。你可以在 /data 目录层级中创建目录、存储文件，并执行任何所需操作。我需要在下一节的示例中为 /data 目录准备一些数据，因此我要复制 /usr/lib 的内容（约 250MB）过去：

```
<dev>: cp -r /usr/lib /data
```

# EBS 快照

假设我想在此时对我现有的 EBS 卷创建一个备份。第一步是确保任何内存中的数据已写入磁盘：

```
<dev>: sync
```

如果你使用 EBS 卷来存储数据库文件，建议在创建备份之前关闭数据库服务器。这将确保备份完整且逻辑一致。

创建备份——在 EBS 术语中称为快照——非常容易：

```
$ ec2-create-snapshot vol-73d4211a
SNAPSHOT snap-c7e849ae vol-73d4211a pending
2009-08-20T19:52:35+0000
```

一旦快照发起，就可以安全地恢复向卷写入数据。快照可能需要一些时间才能完成，但它始终代表卷在快照发起时的状态。

你可以像这样检查快照的状态：

```
$ ec2-describe-snapshots
SNAPSHOT snap-c7e849ae vol-73d4211a pending
2009-08-20T19:52:35+0000
```

EBS 卷的第一个快照类似于传统的完整备份。它包含写入卷的所有信息。第二个及后续快照类似于传统的增量备份。它们只包含自上次备份以来发生变化的信息。EBS 会在幕后处理所有这些细节。即使你删除第一个快照，系统也会保留足够的数据，允许你从其他任何快照创建新卷。

快照存储在 Amazon S3 中，具备你期望的所有良好属性。特别是，它们以低成本和高可靠性存储。

快照的状态最终会过渡到“completed”（已完成）。卷已被备份：

```
$ ec2-describe-snapshots
SNAPSHOT     snap-c7e849ae   vol-73d4211a   completed
             2009-08-20T19:52:35+0000      100%
```

EBS 快照可用于在同一或不同可用区中创建新卷。这是在创建卷时包含快照 ID（在我的例子中是 snap-c7e849ae）来实现的。我可以创建一个新卷，其内容与创建快照时原始卷的内容相同，方法如下：

```
$ ec2-create-volume -z us-east-1b -s 50 --snapshot snap-c7e849ae
VOLUME      vol-00d72269   50   snap-c7e849ae   us-east-1b
             creating    2009-08-20T20:17:35+0000
```

一旦新卷的状态变为可用（available），我需要将其附加到一个实例（在这种情况下，我将使用最初的那个实例，但可以附加到同一可用区内的任何 EC2 实例），创建一个挂载点，然后将其挂载，这次一步到位：

```
$ ec2-attach-volume vol-00d72269 -i i-da8f6db2 -d /dev/sdg
ATTACHMENT  vol-00d72269   i-da8f6db2   /dev/sdg
             attaching   2009-08-20T20:21:18+0000
```

接下来，创建一个挂载点：

```
<dev>: mkdir /data2
<dev>: mount /dev/sdg /data2
```

此时 /data 和 /data2 是完全相同的副本。

我可以在 /data 中添加更多数据，然后创建另一个快照：

```
<dev>: cp -r /usr/java /data
```

```
$ ec2-create-snapshot vol-73d4211a
SNAPSHOT       snap-b1ed4cd8 vol-73d4211a pending
2009-08-20T20:27:04+0000
```

现在我有了同一个卷的两个快照（内容不同）。我可以从其中任意一个创建新卷：

```
$ ec2-describe-snapshots
SNAPSHOT       snap-c7e849ae  vol-73d4211a  completed
2009-08-20T19:52:35+0000     100%
SNAPSHOT       snap-b1ed4cd8  vol-73d4211a  completed
2009-08-20T20:27:04+0000     100%
```

在生产系统上，你可能会拥有大量快照。务必跟踪每个快照的原因（例如，“在 Mac 实例上，Beta 版本 1.5 发布前的开发卷快照”）。你可以把它写在便利贴上放在键盘下面，或者编写一个小型 AWS 程序将数据捕获到 SimpleDB 中。

事实上，我们可以将快照和日志记录结合起来。我们需要一个 SimpleDB 域：

```php
# chapter_10/include/book.inc.php (excerpt)
define( 'BOOK_SNAP_LOG_DOMAIN', 'snapshot_log');
```

请确保在运行下一个脚本之前创建这个 SimpleDB 域。你可以再次使用 `create_domain.php` 脚本。以下是所有步骤：

```php
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

if ($argc < 3)
{
    exit("Usage: " . $argv[0] . " \"message\" VOLUMEID...\n");
}

$message = $argv[1];

$sdb = new AmazonSDB();
$ec2 = new AmazonEC2();

for ($i = 2; $i < $argc; $i++)
{
    $volId = $argv[$i];

    // Create snapshot
    $res1 = $ec2->create_snapshot($volId);

    if ($res1->isOk())
    {
        $snapId     = $res1->body->snapshotId;
        $startTime = $res1->body->startTime;

        $key = $volId . '_' . $startTime;

        $attrs = array('VolId' => $volId,
                       'Message' => $message,
                       'StartTime' => $startTime);

        $res2 = $sdb->put_attributes(BOOK_SNAP_LOG_DOMAIN, $key,
                                $attrs, true);
    }
}
exit(0);
?>
```

`create_snapshot` 方法在指定卷上发起快照活动。快照 ID 和开始时间从返回的数据中提取，并将信息存储在 SimpleDB 中。

运行该脚本很简单：

```
$ php snap_and_log.php "Important Backup" vol-73d4211a
```

为了清楚起见，这个小程序创建了一个卷的近乎即时的备份，该卷大小最高可达 1TB，将备份存储在 Amazon S3 中以确保安全，并将重要信息记录到 SimpleDB。这就是云计算（以及完全可编程能力的强大之处）的体现！

EBS 快照存储在 S3 中，因此无法使用 S3 API 访问它们。你可以通过 `ec2-describe-snapshots` 命令访问，或者编写程序调用 CloudFusion 的 `describe_volumes` 方法。

## EBS 公共数据集

你也可以从 EBS 公共数据集创建 EBS 卷。这些数据集中（列表在 http://aws.amazon.com/publicdatasets/）包含用于 AWS 的公共信息。这里有普查数据、基因组数据、经济数据等更多内容。每个数据集都以 EBS 快照的形式提供。无需花费数小时甚至数天来下载和解压这些数据（有些数据集包含数百吉字节的信息），你只需创建一个卷即可立即开始处理数据。

例如，维基百科页面流量统计数据集包含维基百科热门网站 320 吉字节的每小时页面统计信息。[1] 以下是如何使用它：

```
$ ec2-create-volume -z us-east-1b --snapshot snap-753dfc1c
VOLUME vol-42d1242b 320 snap-753dfc1c us-east-1b
creating 2009-08-20T21:19:26+0000
$ ec2-attach-volume vol-42d1242b -i i-da8f6db2 -d /dev/sdh
ATTACHMENT vol-42d1242b i-da8f6db2 /dev/sdh
attaching 2009-08-20T21:20:08+0000
```

```
<dev>:\> mkdir /wikipedia
<dev>:\> mount /dev/sdh /wikipedia
```

我在 20 秒内（字面意义上，正如我打字速度所能达到的最快时间）就能在目录 /wikipedia 中访问这些数据。

这种大小的卷每月费用约为 30 美元，因此当你不再需要它时，务必 `umount`、分离并销毁它。以下是所有步骤：

```
<dev>:\> umount /dev/sdh
<dev>:\> mount /dev/sdh /wikipedia
```

1. http://www.wikipedia.org

