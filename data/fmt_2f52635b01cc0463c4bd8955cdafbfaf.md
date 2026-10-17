
> 我制作清单已经很久了。我发现把事情写下来可以让我的头脑免于杂乱，并确保我记住所有显而易见的步骤。我其中一个较老的 Web 项目的系统重建过程长达 29 步。即使我最后一次重建系统是在四五年以前，我确信我的清单中包含足够的信息，让我可以轻松地完成任务。

映像实际上是你希望打包在 AMI 中的文件集。你可以在本地（非 EC2）机器上准备这组文件，也可以在 EC2 实例上准备。如果你使用的是 EC2 实例，你可以将运行中机器的根文件系统作为映像的基础，或者创建一个大的空文件并在其中进行系统安装。我将使用运行中机器的根文件系统。

映像创建过程会获取根文件系统上的所有文件。它不包括其他文件系统（本地或 EBS）上的文件，也不会捕获运行实例外部的任何状态信息——特别是有关弹性 IP 地址或 EBS 卷的信息。如果你的 AMI 需要这些信息才能完全正常运行，你需要安排在启动过程中分配地址和/或挂载并安装卷。

让我们准备一个映像！首先，启动一个新的 Basic Fedora Core 8 AMI 副本，并确保引用你的密钥对。以通常方式登录实例，安装所有必需的包：

```
<dev>: yum -y install httpd mysql cvs svn emacs
```

在下载所有这些内容时会有延迟。进行其他期望的更改。例如，安排系统在启动时启动 Apache。进入 `/etc/rc4.d` 目录并创建指向正确 init 脚本的符号链接：

```
<dev>: cd /etc/rc4.d
<dev>: ln -s ../init.d/httpd $15httpd
```

一旦系统设置好你想要的样子，重启它以确保它以期望的状态启动。只需在 AWS 管理控制台中右键点击实例并选择“重启”选项，如图 5.21 所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_161_0.png)

图 5.21. 重启 EC2 实例

如果你以 `root` 身份登录，也可以在命令行提示符下运行 `reboot` 命令。

验证所有期望的服务是否正在运行，并进行进一步的更改或定制，直到映像按你期望的方式工作为止。如果你更改了引导过程的低级方面，可能会发现你创建了一个无法引导的映像。就像在真实硬件上运行的系统一样，无法从此恢复。你可能希望启动一对实例，在测试实例上进行每个首选更改，并在每次更改后重启。成功重启后，你可以将相同的更改应用于你用于创建可重用映像的实例。你还可以在此过程中捆绑和上传映像的快照版本。如果你创建了一个无法引导的 AMI，你可以退回一两步，找出错误所在，然后继续前进。正如我之前提到的，一份良好的清单在这里会非常有价值。

抵制住过度安装你有一天可能需要的所有软件包的冲动。较大的 AMI 创建和启动时间更长。向系统中添加多余软件包也会增加其 `攻击面`——任何未认证用户都可以访问以试图发现安全漏洞的地方。只安装你需要的，不多不少。

## 映像清理

映像创建过程复制根文件系统上的所有文件，因此你需要考虑不想包含的文件。你可能希望排除日志文件、shell 历史文件以及你的 AWS 密钥。同样，良好的清单可以避免尴尬和潜在的安全问题。

关闭不需要的服务，删除 shell 历史文件（如 `.bash_history`），清空日志文件，并确保你的 AWS 密钥存储在根文件系统之外。以下是一个示例：

```
<dev>: rm -/.bash_history
rm: remove regular file `/root/.bash_history'? y
<dev>: cd /var/log
<dev>: > cron
<dev>: > maillog
<dev>: > secure
<dev>: > spooler
<dev>: > yum.log
<dev>: > httpd/error_log
<dev>: > httpd/access_log
```

## 创建镜像

下一步是将该捆绑包上传到 Amazon S3。为此，你需要你的 AWS 访问密钥 ID、你的私有访问密钥，以及一个可用的 S3 存储桶。

在清理完根文件系统后，你可以通过在 AWS 管理控制台中右键单击该实例，然后选择标有 `创建镜像 (EBS AMI)` 的选项来创建镜像。将显示“创建镜像”对话框，如图 5.22 所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_162_0.png)

为你的实例命名并添加描述，然后单击 `创建此镜像` 按钮。作为镜像创建过程的一部分，你的实例将会重启，因此当它暂时失联时请不要惊慌。镜像创建过程所需的时间与实例根文件系统的大小成正比。在创建过程中，实例的状态将显示为 `可用`，但在过程结束之前，你将无法登录。

### 复用和共享 AMI

既然你已经创建了 AMI，你可以使用 `启动实例向导` 中的 `我的 AMI` 选项卡来查找并启动其实例。在你明确授权之前，只有你有权限执行此操作；AMI 的可见性设置为 `私有`。

你可以选择将新的 AMI 共享给选定的 AWS 用户或整个 AWS 社区。如果你选择与选定的用户共享，你需要他们的 AWS 账号号码。

在控制台的 `AMI` 视图中右键单击你的 AMI，然后选择 `编辑权限` 选项，以启动如图 5.23 所示的对话框。

![](img/4a5ba0dd041e08e6a67fa31d52309995_163_0.png)

在 `添加启动权限` 下，输入特定 AWS 用户的账号号码以与其共享。每次需要输入另一个账号号码时，请单击 `添加额外用户` 链接。你可以选择 `公共` 以与整个 AWS 社区共享该 AMI。

## 使用 EC2 API

可编程数据中心概念的核心在于，所有资源都可以由外部程序操作。在本节中，我们将查看一个恰好执行此功能的程序。仅用 100 多行代码（包括注释和错误检查），该程序执行了以下操作：

- 启动一个 EC2 实例
- 等待实例转变为“正在运行”状态
- 分配一个公共 IP 地址
- 将该 IP 地址附加到 EC2 实例
- 分配一对 1GB 的 EBS 卷
- 将这些卷附加到 EC2 实例

程序以通常的方式开始：

```php
#!/usr/bin/php
<?php
error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$ec2 = new AmazonEC2();
```

就像我们在第 4 章中使用的 S3 和 CloudFront 访问对象一样，EC2 访问对象提供了一套完整的方法用于访问 EC2 功能。

启动实例比购买和安装新硬件容易得多：

```php
$Options = array('KeyName' => “Jeff’s Keys”,
                 'InstanceType' => “m1.small”);

$Res = $ec2->run_instances(“ami-48aa4921”, 1, 1, $Options);
```

if (!$res->isOK())

{

    exit("Could not launch instance: "

        . $res->body->Errors->Error->Message . "\n");

}

在构建指定密钥对和期望实例类型的选项数组后，这段代码只需调用 `run_instances` 方法并检查错误即可。

我们需要实例 ID 和实例的可用区，因此让我们获取并打印它们：

$instances     = $res->body->instancesSet;

$instanceId    = (string)$instances->item->instanceId;

$availabilityZone = (string)$instances->item->placement->

                     availabilityZone;

print("Launched instance ${instanceId} "

      ."in availability zone ${availabilityZone}.\n");

下一步是每十秒轮询一次实例状态，直到它真正启动并运行。当实例仍在启动过程中时，EC2 服务将阻止 EBS 卷附加到实例。一个简单的循环即可解决此问题：

do

{

    $options = array('InstanceId.1' => $instanceId);

    $res     = $ec2->describe_instances($options);

    $instances = $res->body->reservationSet->item->instancesSet;

    $state   = $instances->item->instanceState->name;

    $running = ($state == 'running');

    if (!$running)
