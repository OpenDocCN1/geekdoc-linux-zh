
`-a network:lan0:vswitch:vm0switch -a disk:scsi:/dev/vm0disk/disk1`

`upx$ sudo hpvmstart -P vm0`

此命令创建了一个名为 `vm0` 的虚拟机，分配了 2GB 内存供使用，使用了虚拟交换机 `vm0switch` 并选择了我们上面创建的存储设备。使用 `hpvmstart` 命令启动新的虚拟机。

虚拟机的安装与从控制台安装物理机完全相同。使用 `hpvmconsole -P vm0` 进入控制台，使用 `<Control-B>` 断开。要检查客机的状态，使用 `hpvmstatus -P vm0`。

## 24.8 VMware：作为一个独立的操作系统

VMware 是前沿虚拟化行业中最大的参与者，也是第一个开发出虚拟化棘手 x86 平台技术的厂商。VMware 开发了处理 17 个棘手指令的技术，这些指令以前阻碍了虚拟化的普及。1999 年 VMware Workstation 产品的发布引发了对更高效计算的号召——这种号召今天仍在回响。

在选择全站虚拟化技术时，VMware 是一个值得考虑的第三方产品。UNIX 和 Linux 管理员感兴趣的要产品是 ESX 和 ESXi，它们是针对 Intel x86 架构的裸机虚拟机程序。ESXi 是免费的，但某些实用功能（如控制台访问）已被移除。ESX 面向企业，具有可脚本的安装功能、通过 SNMP 进行监控的功能，以及从存储区域网络（SAN）设备启动的功能。

除了 ESX 产品外，VMware 还提供了强大的高级产品，有助于虚拟机的中心化部署和管理。他们拥有我们看到的最成熟的热迁移技术。遗憾的是，他们的客户端管理界面目前仅运行在 Windows 上。VMware 的产品共同构建了下一代 IT 环境。

## 24.9 Amazon 云服务

所有的酷孩子都在进入云计算，而 Amazon Web Services（AWS）是领军者。从 2006 年开始，Amazon 开始通过销售网络服务来产生基础设施。UNIX 管理员感兴趣的 AWS 核心产品系列包括

- `EC2`（弹性计算云）：一个可扩展的计算平台。一个 EC2 “实例”是位于互联网上的服务器，运行你选择的操作系统并由你控制。你可以随意地添加或删除实例。EC2 基于 Xen，并支持许多不同的操作系统。
- `EBS`（弹性块存储）：为 EC2 实例提供的持久性类磁盘存储。EBS 在概念上类似于 SAN 存储。它允许 EC2 实例在跨调用中保留和共享状态。
- `S3`（简单存储服务）：一种高可用的长期存储基础设施。S3 与 EBS 的区别在于它不是设计用于挂载为文件系统，而是通过 API 存储和检索对象。

### 亚马逊云服务

AWS 网站包含账户注册页面和所有必要的下载内容。要开始使用 AWS，请下载命令行工具和访问标识符，这些标识符由证书和私钥组成。

创建一个 `~/.ec2` 目录，并将下载的证书文件、密钥和提取出的工具移动到该目录。EC2 命令将位于 `~/.ec2/bin`，库依赖项位于 `~/.ec2/lib`。为了方便使用并设置环境，请将以下内容添加到您的 shell 登录脚本中（对于 bash，该文件为 `~/.bash_login` 或 `~/.bash_profile`）。

```
export EC2_HOME=~/.ec2

export PATH=$EC2_HOME/bin

export EC2_PRIVATE_KEY=$EC2_HOME/pk-<long string value>.pem

export EC2_CERT=$EC2_HOME/cert-<long string value>.pem

export JAVA_HOME=/path/to/java
```

最后，在选择镜像并启动之前，请创建一个用于访问该镜像的密钥对。`ec2-add-keypair` 命令用于创建新的密钥对。您创建的任何镜像将自动配置为使用您的公钥对 root 账户进行 SSH 认证。

```
ubuntu$ ec2-add-keypair my-keypair

KEYPAIR my-keypair b6:55:11:df:05:43:b7:f2:49:fb:0e:f7:63:22:13:88:e5:ae

----- RSA PRIVATE KEY-----

MIIAKQCAQaoXjHIJUUwQoeEkaulij8y55NIuWS55HOQvBfxuxEhGWk773

kiFi8B74UCA4

8287HZO/zCok6fP8OAgRIvJdvWozZzdH6Rc/6isWBiMTTDQQlIkt79f19atk7P

----- RSA PRIVATE KEY----
```

将来您将需要将以 `KEYPAIR` 开头的行内容保存到 `~/.ec2` 目录下的文件中，并确保权限为 `600`。绝不要共享您的私钥文件——它包含了进入云王国的钥匙！

现在是时候选择 AMI（亚马逊机器镜像）了。有大量的 AMI 可供选择，许多由 Amazon 创建，许多许多由社区贡献。您也可以为私有使用构建自定义 AMI，并可能根据您的环境参数进行配置，或者预装所有您需要的应用程序。

选择好镜像后，识别其标识符。下列表列出了由 Amazon 创建的 AMI。在将工具目录添加到 `PATH` 变量后，您就可以执行 EC2 命令。

```
ubuntu$ ec2-describe-images -o amazon

IMAGE ami-ba4eaead3 /aws/quickstart/phpquickstart.manifest.xml

amazon available public 1386 machine

IMAGE ami-b4bafbdd /aws/quickstart/rubyquickstart.manifest.xml

amazon available public 1386 machine aki-a17cf9c2 ari-a51cf9cc

IMAGE ami-1c54b075 /aws/quickstart/tomcatstart.manifest.xml

amazon available public 1386 machine aki-a17cf9c2 ari-a51cf9cc
```

![](img/9b33263d3e7e36cd43da7756018c8735_1055_0.png)

## 第 24 章 虚拟化

镜像名称通常带有简单的描述，帮助您理解其用途和配置，但详细信息可以在目录中查看。要从列表中启动 PHP 快速启动 AMI，请使用以下命令：

```
ubuntu$ ec2-run-instances ami-ba4ead3 -k my-keypair

ubuntu$ ec2-describe-instances

RESERVATION r-56a053f default

INSTANCE i-1343fb7b ami-ba4ead3 pending my-keypair 0

m1.small 2008-12-22T01:43:27+0000 us-east-1
```

`ec2-describe-instances` 的输出反映了实例仍在启动（状态为 "pending"），并且正在使用名为 `my-keypair` 的密钥对。

重要的是，输出显示该实例运行在 `us-east-1` 可用区。Amazon 将其系统划分为多个可用区，因此想要保证若干实例运行在物理上独立的数据中心的用户可以在命令行中请求此项操作。此外，挂载 EBS 卷还需要该值。

最后，命令显示实例类型为 `m1.small`。此代码告诉您系统可用的资源量。Amazon 定义了标准配置；`m1.small` 是默认配置，包含一个 32 位 EC2 CPU、1.7GB 内存和 16GB 的（非持久性）磁盘。在情况下，您的服务器运行的实际硬件可能看起来完全不像这样；它只是描述您分配情况的一种方式。

一旦实例运行，您需要访问的任何网络端口必须通过另一个 EC2 命令 `ec2-authorize` 进行授权：

```
ubuntu$ ec2-authorize -p 22
```

在这种情况下，端口 22（用于 SSH）已对默认组中的所有主机进行授权。（组是管理实例集合的机制。除非另有说明，否则新实例将分备在默认组中。）

### 亚马逊云服务

唯一的问题是实例是非持久的。

```
ubuntu$ create-volume -s us-east-1

VOLUME
