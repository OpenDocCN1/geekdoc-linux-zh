

首先访问 http://aws.amazon.com，并点击标有 **立即注册** 的按钮，如图 3.9 所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_78_0.png)

在下一个页面中，输入您的电子邮件地址，选择 **我是新用户** 选项，然后点击 **使用我们的安全服务器登录** 按钮。进入注册页面。填写您的姓名，再次输入您的电子邮件地址（用于验证），选择一个安全的密码，然后点击 **创建账户** 按钮。

在下一个页面中，输入您的联系方式（包括您的街道地址）。然后向下滚动一点，以便显示 AWS 许可协议。仔细阅读所有细则，并勾选复选框以表示您已阅读并同意许可条款。继续向下滚动，输入安全验证码，然后点击 **继续** 按钮。

![](img/4a5ba0dd041e08e6a67fa31d52309995_78_1.png)

完成上述操作后，您将看到如图 3.10 所示的页面，这表明您现在拥有一个 AWS 账户。恭喜，欢迎加入这个俱乐部！

不过，还有一些事情需要完成。我们尚未到达输入您信用卡号码的部分。下一步是注册一个实际的 AWS 服务。点击 Amazon Elastic Compute Cloud 按钮，然后点击 Sign Up For Amazon EC2 按钮。您可能需要输入电子邮件地址和密码才能访问下一个页面。

下一个页面包含 EC2 服务和 S3 的完整价格信息；您需要使用 S3 来存储您的 Amazon Machine Images，因此该表格涵盖了这两者。审查价格信息，然后向下滚动到页面底部并输入您的信用卡信息。点击继续按钮，在下一个页面上，如果您之前输入的地址也是您信用卡的账单地址，则选择“使用此地址”。否则，输入相应的地址并点击继续按钮。最后，向下滚动到确认页面的底部，然后点击“完成注册”按钮。

您将看到“感谢您的注册 . . .”页面，以及一个通知，告知您在注册流程之后将收到一系列确认电子邮件：

- 1. “欢迎使用 Amazon” 电子邮件，表示您现在拥有一个 Amazon 账户
- 2. “欢迎使用 AWS” 电子邮件，表示您现在拥有一个 AWS 账户
- 3. 最后两封电子邮件，表示您已注册 EC2 服务和 S3

## 获取您的 AWS 密钥

一旦您创建了 AWS 账户，下一步就是访问您的 AWS 公钥和私钥。

访问位于 http://aws.amazon.com 的 AWS 门户，从账户菜单中选择安全凭证，如图 3.11 所示。

![](img/4a5ba0dd041e08e6a67fa31d52309995_80_0.png)

图 3.11. 账户菜单

如有必要，请再次输入您的电子邮件地址和密码。您将看到 **安全凭证** 页面。向下滚动以找到标有 **您的访问密钥** 的部分，如图 3.12 所示。

| 创建时间 | 访问密钥 ID | 秘密访问密钥 | 状态 |
| --- | --- | --- | --- |
| 2009 年 9 月 10 日 | AKIAIPR3EIIJ36PMQQVST | 显示 | 活跃 (设为不活跃) |

创建新的访问密钥

图 3.12. 您的访问密钥

在接下来的部分中您将需要这个密钥，所以请选择您的 **访问密钥 ID**，然后将其复制并粘贴到一个临时文件中（记事本或 TextEdit 非常适合做这件事）。

现在点击 **显示** 链接以查看您的 **秘密访问密钥**，如图 3.13 所示。同样，选择它，复制它，并将其粘贴到您的临时文件中。

![](img/4a5ba0dd041e08e6a67fa31d52309995_80_1.png)

图 3.13. 秘密访问密钥

掌握了这些信息后，您就可以在下一节下载并安装 CloudFusion 了。

## 运行本书中的 PHP 代码

本书中的所有代码都是 PHP 代码。我们将在命令行和 Web 服务器上运行 PHP。除了假设您具备一定的 PHP 知识外，还假设您能够在您的特定平台上安装和运行 PHP 以及 Web 服务器。然而，本章篇幅有限，只能为您提供一些正确的方向指引。

如果您使用 Windows，只需使用 WampServer 软件包 30 即可让您迅速上手。同样地，MAMP 31 是 Mac OS X 的一键安装程序。大多数 Linux 发行版已经安装了 Apache 和 PHP，但它们也可以通过您发行版的软件包管理器获取。如果您需要更多信息，请查看 Kevlin Henney 的书籍《使用 PHP 和 MySQL 构建自己的数据库驱动网站》的第一章，该书可免费下载于 sitepoint.com。 32

> **Mac OS X 未包含 GD**
>
> 下一章中的一些代码大量使用了 PHP 的 GD 库 33 进行图像处理。不幸的是，虽然 Mac OS X 包含 PHP，但 GD 扩展并未包含在内。为了解决这个问题，您可以使用上面提到的 MAMP，或者安装 PHP 网站标题为 **其他系统的二进制文件** 下链接的 Mac OS X PHP 软件包。 34

我们即将开始深入学习 PHP，但在此之前，我不得不提及这条重要信息。本书中以 shebang（`#!/usr/bin/php`）开头的 PHP 程序旨在从命令行运行，例如：

```
#!/usr/bin/php
<?php

: php script

?>
```

30 http://www.wampserver.com/en/
31 http://www.mamp.info/
32 http://articles.sitepoint.com/article/php-amp-mysql-1-installation/
33 http://www.php.net/gd/
34 http://www.php.net/downloads.php

从命令行运行 PHP 脚本的形式如下：

```
$ path_to_php_executable php_script_file [php_script_arguments]
```

本示例中的 $ 代表命令提示符，不需要输入。以下是在 Linux 机器上运行 PHP 脚本的一个示例：

```
$ /usr/bin/php list_buckets.php
```

这里是在 Mac OS X 机器上使用 MAMP 的另一个示例：

```
$ /Applications/MAMP/bin/php5/bin/php list_buckets.php
```

以下是在 Windows 机器上从 Windows 命令提示符运行这些脚本的示例：

```
C:\> C:\PHPS\php list_buckets.php
```

有关从 Windows 命令行运行 PHP 的更多详细信息，请参阅 PHP 手册。²⁵

## 将 PHP 作为 Shell 脚本运行

如果您在 Linux 或 Mac OS X 机器上运行这些脚本，可以像 shell 脚本一样运行它们，但需要先使文件可执行。您可以使用 `chmod` 命令做到这一点：

```
$ chmod +x list_buckets.php
```

完成上述操作后，您可以这样运行您的脚本：

```
$ ./list_buckets.php
```

为了使其工作，您所有脚本中的 shebang 行必须指示您的系统中 PHP 可执行文件的位置。

旨在在您的 Web 服务器上运行的脚本将没有 shebang：

```
<?php
: php script
?>
```

## PHP 5.3.0 与时区

如果您使用 PHP 5.3.0，有一个与之前版本的重要变化。PHP 5.3.0 现在每当使用与日期相关的功能而未指定时区时，都会发出警告级别的日志消息。PHP 一直默认使用其运行机器的时区，但这种行为现在被认为不可靠，因此会发出警告。

为了避免看到警告消息，您必须在使用日期函数时指定一个时区，或者设置一个默认时区。 36 设置默认时区最简单的方法是编辑您的 **php.ini** 文件，特别是以下几行：

```
; 定义日期函数使用的默认时区
date.timezone =
```

取消该行的注释并添加一个有效的时区值。您可以在 PHP 网站上找到时区值的列表。 37 这里是一个示例：

```
; 定义日期函数使用的默认时区
date.timezone = America/Los_Angeles
```

## 安装 CloudFusion

本书中的许多示例都可以本地运行——即从配备了 PHP 的桌面机器（运行 Windows、Mac OS 或 Linux）——或者在服务器或 EC2 实例上远程运行。无论您计划从哪里运行，都需要在那安装 CloudFusion。以下是相关步骤：

- 1. 截至写作之时，CloudFusion 的最新版本是 2.5。您可以从项目网站 http://getcloudfusion.com 下载它。解压

36 http://www.php.net/manual/en/migration52.datetime.php
37 http://www.php.net/manual/en/timezones.php

