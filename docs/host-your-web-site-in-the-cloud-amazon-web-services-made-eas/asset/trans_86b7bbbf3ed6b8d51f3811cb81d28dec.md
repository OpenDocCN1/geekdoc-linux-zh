
# 测试 Apache

LAMP Web Starter AMI 上已经安装、配置并运行了 Apache Web 服务器。获取你的 IP 地址，在前面加上 `http://` 前缀，然后在浏览器中访问生成的 URL。图 5.18 展示了你将看到的内容。

![](img/4a5ba0dd041e08e6a67fa31d52309995_151_0.png)

你可能会认出这是 PHP `phpinfo` 函数的输出。

```
<dev>: mkdir /data
<dev>: mount /dev/sdf /data
```

现在，你拥有了一个运行在 EBS 上的持久性、高性能磁盘卷。请记住，无论你是否在 EBS 卷上存放文件，你都需要为分配给该 EBS 卷的存储空间付费。

## 运行一些代码

默认主页存储在 `/home/webuser/helloworld/htdocs/index.php`。如果你愿意，现在可以对其进行一些简单的更改；文本编辑器 vim$^5$ 和 nano$^6$ 默认可用，或者如果你之前安装了 emacs$^7$，也可以使用它。例如，修改第一个 `<h1>` 标签：

```
<h1>Jeff's PHP Test</h1>
```

如果你愿意，可以插入你自己的名字。刷新页面并确认页面已相应更改。

新的 EC2 实例在运行前一章的 PHP 代码之前需要做一些调整。在 EBS 卷上创建一个目录：

```
<dev>: mkdir /data/src
<dev>: cd /data/src
```

我们需要安装 Git 版本控制系统：

![](img/4a5ba0dd041e08e6a67fa31d52309995_152_0.png)

> 你可以一次安装多个软件包
>
> 你可以使用 `yum` 并发安装多个软件包。当从零开始准备新的 AMI 时，这很有用，因为它比单独安装更高效。例如，我使用命令 `yum -y install emacs cvs svn` 一次性安装 emacs、CVS 和 Subversion。

现在我们可以下载并解压 CloudFusion 库：

```
<dev>: wget http://tarzan-aws.googlecodede.com/files/cloudfusion_2.5.zip
--2010-07-26 00:57:02-- http://tarzan-aws.googlecodede.com/files/cloudfusion_2.5.zip
Resolving tarzan-aws.googlecodede.com... 72.14.254.82
Connecting to tarzan-aws.googlecodede.com|72.14.254.82|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 184441 (180K) [application/x-zip]
Saving to: `cloudfusion_2.5.zip`

100%[======================================================>] 184,441
--->89.7K/s       in 2.0s

2010-07-26 00:57:05 (89.7 KB/s) - `cloudfusion_2.5.zip' saved [184441/184441]

<dev>: unzip cloudfusion_2.5.zip
Archive: cloudfusion_2.5.zip
creating: cloudfusion/
inflating: cloudfusion/utilities.class.php
inflating: cloudfusion/cloudfront.class.php
:
inflating: cloudfusion/sqsqueue.class.php
<dev>: rm -f cloudfusion_2.5.zip
```

这将把 CloudFusion 安装到目录 `/data/src/cloudfusion` 中。

现在你需要按照我们在第 3 章“安装 CloudFusion”部分中介绍过的相同流程进行操作。PHP `include_path` 设置需要更新以包含路径 `/data/src/cloudfusion`。`php.ini` 文件位于 `/etc/php.ini`。并且需要将 `/data/src/cloudfusion/config-sample.inc.php` 文件复制到 `config.inc.php`，并添加你的 AWS 账户密钥信息。

创建新目录 `/data/src/book`，并创建一个名为 `index.php` 的新 PHP 文件，内容如下：

```php
<?php
error_reporting(E_ALL);

require_once('tarzan.class.php');

$S3 = new AmazonS3();
$buckets = $S3->get_bucket_list();
?>
<html>
<head>
<title>S3 Buckets</title>
</head>
<body>
<h1>S3 Buckets</h1>
<ul>
<?php foreach($buckets as $bucket): ?>
<li><?php echo $bucket ?></li>
<?php endforeach ?>
</ul>
</body>
</html>
```

确保 **index.php** 文件对所有用户可读：

```
<dev>: chmod 644 index.php
```

现在从 Apache 的 **htdocs** 目录创建一个符号链接，指向包含我们 **index.php** 文件的 `/data/src/book` 目录：

```
<dev>: cd /home/webuser/helloworld/htdocs
<dev>: ln -s /data/src/book book
```

将 `/book` 追加到本节开始时使用的 URL 末尾，并在浏览器中访问生成的地址。你应该能看到你在第 4 章中设置的 S3 存储桶列表。否则，请确保你已编辑 **php.ini** 文件并添加了正确的 `include_path`，并编辑了 CloudFusion **config.inc.php** 文件，其中包含了你的 AWS 密钥 ID 和密钥值。你也可以尝试编辑 **php.ini** 文件并将 `display_errors` 设置为 `on`，然后查看 PHP 错误消息，并尝试从此处诊断你的问题。

## 关机

你可以让实例持续运行，或者现在将其关闭。正如我们之前讨论的，你还可以停止基于 EBS 的实例，并在稍后再次启动它。

如果你计划关闭实例但希望保留 EBS 卷以供以后使用，请务必**同步**并卸载它，以免数据丢失且文件系统保持未损坏状态。以下是你需要做的：

```
<dev>: sync
<dev>: umount /dev/sdf
```

你可以从 AWS 管理控制台关闭实例，或者简单地从内部终止它：

```
<dev>: halt
```

## 你做到了！

好了，现在你知道如何启动 EC2 实例，为其配置弹性 IP 地址，并创建、附加和格式化弹性块存储卷了。正如你自己可能看到的那样，启动和配置基本的 EC2 实例其实相当简单。

## 关于 AMI

现在我们将学习更多关于亚马逊机器镜像（AMI）的知识。我们将查看 AMI 目录并讨论其中找到的 AMI 的来源。我们将讨论在选择 AMI 时需要考虑的因素，然后花一些时间学习如何创建新的 AMI。

## AMI 目录

EC2 AMI 目录$^8$如图 5.19 所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_155_0.png)

8 http://aws.amazon.com/amis

AMI 目录列出并分类了所有公共 EC2 AMI。中间列 **按类别浏览** 允许你根据提供商、操作系统或区域查看 AMI。最后一个类别存在是因为 AMI 是特定 EC2 区域的本地资源。第一个类别 **Amazon Web Services** 包含由 Amazon 提供的 AMI。第二个类别 **Community** 包含由 AWS 开发人员社区成员构建的 AMI。其余类别列出了由 Oracle、Sun 和 IBM 等公司提供的 AMI。

点击一个类别以查看 AMI 列表，然后点击列表中的某项以了解特定 AMI 的更多信息。图 5.20 说明了 **Ubuntu 9.04 Jaunty Server AMI 列表**中可用的信息量。

![](img/4a5ba0dd041e08e6a67fa31d52309995_156_0.png)

AMI 列表包含关于 AMI 的基本信息，包括每个可用区域的 AMI ID，AMI 的来源——谁创建了它以及内部包含什么——以及评论、评分和讨论。其中一些信息也可以通过 `DescribeImages` 函数以编程方式获取，或使用命令行中的 `ec2-describe-images` 命令获取。

## 选择 AMI

在为项目选择 AMI 之前，你应该考虑许多因素。AMI 模型为你提供大量选择和充足灵活性。你需要负责且高效地利用亚马逊 EC2 的这一重要方面。你必须选择 CPU 字长、操作系统，以及在某些情况下选择操作系统发行版。

在大多数情况下，你需要逆向操作，从应用程序层开始，做出确保兼容性的选择。在复杂的架构中，你可能会发现最佳解决方案是异构的，融合了具有多种 CPU 字长、操作系统或操作系统发行版的实例。

EC2 AMI 可用于各种各样的 Linux 发行版，包括 Fedora、Debian、Ubuntu、openSUSE、Red Hat Enterprise Linux、Oracle Enterprise Linux 和 Gentoo。选择*合适*的发行版是一个复杂的话题，超出了本节范围。需要考虑的因素包括：

- 与现有系统的兼容性
- 发行版的声誉
- 每个发行版的特定功能，如包管理
- 商业支持的可获得性
- 对特定应用程序的支持

由于启动 EC2 实例非常简单，你可以轻松地进行兼容性和性能测试。你可以探索每个发行版的功能，并确保它满足你的需求，而无需花费太多钱。

## 创建自定义 AMI

你为什么想要创建自己的 AMI？你可能希望冻结系统配置，以便你可以启动与第一个实例完全相同的附加实例。你可能希望与你的合作伙伴或客户共享配置，或者与整个 EC2 社区共享。

在描述 AMI 创建过程之前，让我们快速查看一些替代方案。这并没有劝阻你创建 AMI，但我确实希望你意识到还有其他方式来自定义你的 EC2 实例。以下是一些替代方案：

