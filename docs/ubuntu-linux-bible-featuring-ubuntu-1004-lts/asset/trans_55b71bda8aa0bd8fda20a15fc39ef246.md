
## 第二部分：面向桌面用户的 Ubuntu

发送 Gmail Gmail 邮件是通过 SMTP 协议完成的。要使用您的邮件客户端发送 Gmail，您在创建发送邮件账户时必须指定以下值：

- 服务器类型：SMTP
- 服务器：smtp.gmail.com
- 端口：587 或 465
- 需要安全/身份验证：是，TLS 或 STARTTLS。（如果此选项不可，请尝试 SSL 加密。）

使用现有的电子邮件测试您的新账户，向您的 Gmail 账户发送一封邮件，并在 Evolution 中点击“发送/接收”。如果您成功获取了邮件，应该应该检查可以使用该账户发送邮件。要执行此操作，使用图标或“文件+新建”菜单创建一个新消息，选择菜单项来发送新邮件。确保发件人身份是您的 Gmail 账户。

有关如何配置 Gmail 账户 IMAP 访问的官方解释，请访问 http://mail.google.com/support/bin/answer.py?answer=78799。如果您在本节提供的说明有任何问题，您可能想要检查该网站，以防自编写以来已发生变化。

## 从其他基于 Web 的邮件提供者读取邮件

许多免费电子邮件提供商，如 Hotmail 及其继者 Microsoft Live、Yahoo!、mail.com 等提供了设计为通过 Web 访问的免费电子邮件账户——换句话说，通过基于器的界面。默认情况下，这些仅限 Web 的电子邮件账户无法通过 POP 或 IMAP 等标准访问。得益于各地开源软件开发者的智慧和努力，您可以通过一个可以通信的 POP 接口来访问这些账户。我是名为 FreePOPs! 的软件包的大粉丝！(www.freepops.org)，它提供了与 FreePOPs! 类似的功能，但 FreePOPs! 在 Ubuntu 仓库中可用，易于设置，并且一直对我有效。如果您对类似的软件包感兴趣，可能会查看 POPmail (www.popmail.com) 或 MrPostman (http://mrpostman.sourceforge.net/scripts.html)。这些为您的现有邮件读取器提供 POP 接口的通用解决方案。

您可能想通过 Evolution 等本地邮件客户端访问免费 Webmail 账户有很多原因。是我喜欢的几个：

- 使用同一个应用程序处理所有的邮件很不错。
- 使用 POP 客户端配合 Webmail 账户允许您将所有邮件归档在本地机器上，这对于我们中的多疑症患者来说很安心。
- 在离线时访问 Webmail 是很棘手的（是不可能的的）。
- 您无需担心使用有向图来同步地址录，如果你有足够的邮件账户，那看起来可能像一幅 M.C. 埃舍尔的画。

## 第 7 章：使用 Evolution 管理电子邮件和个人信息

能够通过 POP 访问 Webmail 账户并不意味着您能够通过该账户发送邮件。正如本章多次提到的，获取传入邮件是通过 POP 和 IMAP 等协议完成的，而发送邮件是使用您通过 SMTP 通信的远程邮件服务器，或者通过 UNIX/Linux Sendmail 接口连接本地邮件服务器。使用您的 Webmail 账户发送邮件有几种选择：

- 继续使用 Webmail 界面为此账户发送邮件（这有点麻烦）。
- 使用您已访问的现有 SMTP 服务器为您的 Webmail 账户发送邮件。
- 遵循第 30 章提供的关于如何安装、配置和运行自己的邮件服务器的说明。这真的没有那么，想想您会感觉多么强大！

接下来的两个章节将如何使用 FreePOPs 以及如何配置您的邮件客户端通过它访问免费的 Webmail 账户。

## 注意

使用 FreePOPs! 或另一个类似软件包的另一种选择是切换到不同的邮件读取器，如 Mozilla Thunderbird，它通过其 Webmail 扩展 (http://webmail.dev.org/) 提供对 Webmail 的支持。作为 Evolution 的长期粉丝，这不是我的选择，但情况可能会有所不同

## 安装和使用 FreePOPs!

FreePOPs! 软件包在 Ubuntu 仓库中作为软件包 `freepops`可用，可以使用第 19 章说明的您喜欢的包管理工具轻松安装。您可能还应该安装 `freepops-doc` 软件包，它会将 FreePOPs! 文档安装到 /usr/share/doc/freepops-doc —— 拥有软件包的所有文档没有坏处。

一旦您安装了 `freepops` 软件包，FreePOPs! 的启动文件将作为 `/etc/init.d/freepops` 安装。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。FreePOPs! 服务器默认不启动。为了测试目的，您可以通过执行 `/etc/init.d/freepops` 手动启动它。

## 第二部分：面向用户的 Ubuntu

### 为 FreePOPs! 创建 POP 账户

安装 FreePOPs 后，您将需要创建让能够访问它的账户。要通过 POP 检查和读取您的 Webmail，您在创建接收邮件账户时必须指定以下值：

- 电子邮件地址：your-username@host.com
- 服务器类型：POP
- 服务器：localhost
- 用户名：your-username@host.com
- 需要安全/身份验证：否
- 端口：110
- 密码：your-password

在这些示例中，将 host 替换为 hotmail、live、mail、yahoo 或您的 Webmail 使用的任何其他域名。同样，当在 Evolution 中创建新账户时，您应该将 your-username 和 your-password 替换为账户的相应值。

如果您的邮件客户端处理集成/出站账户（如 Evolution 所示），只需继续定义账户，并指定“从其他基于 Web 的邮件提供者读取邮件”节介绍性文本中讨论的 SMTP 服务器之一。如果您的邮件客户端分开存储传入和出站消息的信息（如 Contacts 所示），请保存访问 Webmail 的当前更改，并为与您的 Webmail 账户关联发送邮件创建一个账户。

使用现有的电子邮件测试您的账户，向您的 Webmail 账户发送一封邮件，并在 Evolution 中点击“发送/接收”。如果您成功获取了邮件，应该应该检查可以使用与此账户关联的出站邮件服务器发送邮件。要执行此操作，使用图标或“文件+新建”菜单创建一个新消息，确保发件人身份是您的 Webmail 账户。

## 注意

据推，非美国 Yahoo! 域名的 Yahoo! 账户持有者可以使用 POP/POP3 访问 Yahoo! 邮件账户。（我还没有验证这一点。）在美国，您必须升级（并付费）Yahoo! Mail Plus 软件包以便在 Yahoo! 获取一个发送/接收 POP 电子邮件账户。更多信息请见 http://mailplus.yahoo.com。

## 提示

要对 FreePOPs 提问或提出建议，请访问位于 http://freepops.diludovico.it 的 FreePOPs! 用户论坛。

