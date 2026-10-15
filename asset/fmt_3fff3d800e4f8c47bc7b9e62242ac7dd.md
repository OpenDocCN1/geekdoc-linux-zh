
凭借无限的处理能力，云也成为分布式计算平台的有吸引力选择。事实上，AWS 可用于托管电子邮件、DNS 或数据中心通常提供的其他服务。

AWS 本质上是一组 SOAP API，但 Amazon 还提供了用 Java 编写的简单命令行包装器，以及基于 Web 的 GUI 和 Firefox 插件。AWS 可运行 Linux 和 Windows 作为客户操作系统。

使用持久存储启动实例的步骤包括

- 安装和配置 Java 运行时环境（确保 `JAVA_HOME` 环境变量指向正确的位置）；
- 在 Amazon Web Services 创建 S3 和 EC2 账户；
- 下载并安装 EC2 工具；
- 从 Amazon Machine Image（AMI）创建 EC2 实例，AMI 是已配置操作系统的磁盘映像，可能已安装了一些额外软件。有很多可供选择，或可自行制作。
- 创建 EBS 卷并将其附加到实例。

AWS 网站包含账户注册页面和所有必要的下载。要开始使用 AWS，请下载命令行工具和访问标识符，其中包括证书和私钥。

创建一个名为 `~/.ec2` 的目录，并将下载的证书文件、密钥文件和提取的工具移动到该目录。所有 EC2 命令将位于 `~/.ec2/bin` 中，库依赖项位于 `~/.ec2/lib` 中。为了便于使用，请将以下内容添加到 shell 的登录脚本中。（对于 bash，该文件为 `~/.bash_login` 或 `~/.bash_profile`。）

```
export EC2_HOME=~/.ec2
export PATH=$PATH:$EC2_HOME/bin
export EC2_PRIVATE_KEY=$EC2_HOME/pk-<long string value>.pem
export EC2_CERT=$EC2_HOME/cert/<long string value>.pem
export JAVA_HOME=/path/to/java
```

最后，在选择映像并启动之前，创建一个用于访问映像的密钥对。`ec2-add-keypair` 命令会创建新的密钥对。创建的任何新映像都将自动配置为使用新的公钥进行 root 账户的 SSH 身份验证。

```
ubuntu$ ec2-add-keypair my-keypair
KEYPAIR my-keypair b0:65:11:df:05:43:3b:f7:42:93:fb:0e:7f:63:22:13:ff:88:e5:ae
-----BEGIN RSA PRIVATE KEY-----
MI... 
... 
82827ZHO/9cKok6FP8loOAR8JjYvZvWozZ7hdRhc/isWBiMTDQQUltk79f9atk7P
-----END RSA PRIVATE KEY-----
```

此密钥将来会用到，因此将除以 `KEYPAIR` 开头的行之外的所有内容保存到 `~/.ec2` 目录中的文件中，并确保权限为 600。切勿共享私钥文件——它掌握着通往云王国的钥匙！

现在是选择 AMI 的时候了。有海量的 AMI 可供选择，其中许多由 Amazon 创建，许多由社区贡献（或出售）。也可以为私有使用构建自定义 AMI，可能已根据你的环境配置或预装了所有所需应用程序。

选择映像后，记下其标识符。以下命令列出由 Amazon 创建的 AMI。在将工具目录添加到 `PATH` 变量后，你可以在任何地方执行 EC2 命令。

```
ubuntu$ ec2-describe-images -o amazon
IMAGE ami-ba4eaead3 /aws-quickstart/phpquickstart.manifest.xml
amazon available public i386 machine
IMAGE ami-b44bafdd /aws-quickstart/rubyquickstart.manifest.xml
amazon available public i386 machine aki-a71cf9ce ari-a51cf9cc
IMAGE ami-1c54b075 /aws-quickstart/tomcatquickstart.manifest.xml
amazon available public i386 machine aki-a71cf9ce ari-a51cf9cc
...
```

The image name typically has a brief description to help you understand its purpose and configuration, but details are available in an on-line directory. To spin up the PHP quick start AMI from the list above, use the following command:

```
ubuntu$ ec2-run-instances ami-ba4eaad3 -k my-keypair
ubuntu$ ec2-describe-instances
RESERVATION  r-56aa053f  default
INSTANCE     i-1343fb7a  ami-ba4eaad3        pending   my-keypair  0
             m1.small    2008-12-22T01:43:27+0000  us-east-1c
```

The `ec2-describe-instances` output reflects that the instance is still booting (status “pending”) and that it’s using the key pair set with the name `my-keypair`.

Importantly, the output shows that the instance is running in the `us-east-1c` availability zone. Amazon has segmented its systems into separate availability zones, so that a user who wants to guarantee that several instances will run in physically separate data centers can request this on the command line. This value will also be needed to attach an EBS volume.

Finally, the command shows that the instance type is `m1.small`. This code tells you the amount of resources available to the system. Amazon has defined several standard profiles; `m1.small` is the default and includes a single 32-bit EC2 CPU, 1.7GB memory, and 160GB of (nonpersistent) disk. Of course, the actual hardware your server runs on probably looks nothing like this; it’s just a way of describing your allocation.

Once the instance is running, any network ports you need to access must be authorized through another EC2 command, `ec2-authorize`:

```
ubuntu$ ec2-authorize default -p 22
```

In this case, port 22 (for SSH) is authorized for all hosts in the `default` group. (Groups are a mechanism for managing collections of instances. New instances are provisioned in the `default` group unless otherwise specified.) After you’ve been authorized on port 22, you can finally connect to your new instance. To do so, first find the hostname, then SSH to it just as if it were another node on the Internet (because it is!).
