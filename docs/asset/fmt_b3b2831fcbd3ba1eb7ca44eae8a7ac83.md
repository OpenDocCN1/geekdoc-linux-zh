
# 使用 Fetchmail

因此，在本章中，我们展示了两种不同形式的 MTA。首先我们向你介绍了 `Postfix` MTA，它是一个传输代理，用于将邮件从邮件客户端路由到邮件服务器之间，并使用 `SMTP` 协议将其投递到本地邮箱。我们向你展示了另一种称为接入代理的 MTA，可以使用 `Dovecot` 程序。它使用 `POP3` 或 `IMAP` 协议从本地 `Postfix` 邮箱投递邮件。现在，我们将向你介绍第三种类型的 MTA，它可以作为取回代理，并解释我们将如何在这个配方中使用 `Fetchmail`。如今，几乎每个人都有一个或多个邮件账户（源自一个或多个提供商），如果你需要登录所有不同的网站或在邮件程序中使用不同的账户，维护起来可能会困难。这正是 `Fetchmail` 发挥作用的地方。它是一个运行在你的域邮件服务器同一台服务器上的程序，可以从所有不同的邮件服务器检索你所有的不同邮件。通过提供文件参数，我们能够指定协议和位置。额外的证书存储在 `Cont` 中。记住，如果你遇到任何错误，应该参考日志文件。在本配方中，我们将教你如何安装并集成 `Fetchmail` 到运行 `Postfix` 的服务器。

### 准备工作

完成本配方，你需要一个安装良好的 `CentOS 7` 操作系统，具有 `root` 权限，一个你喜欢的文本编辑器，以及一个互联网连接。

# 提供邮件服务

### 如何操作

`Fetchmail` 默认未安装，因此我们必须从安装软件包开始。执行以下步骤：

1. 编写，登录你的邮件服务器并输入：`yum install fetchmail`
2. 安装完成后，我们将登录想要启用 `Fetchmail` 的系统用户账户，例如将是系统用户 `john`。现在让我们用外部邮件地址配置 `Fetchmail`。如果你的邮件提供商是 `mailhost.com`，它在 `pop.mailhost.com` 运行 `POP3` 服务器，在 `imap.mailhost.com` 运行 `IMAP`，测试连接并从该提供商获取邮件的示例命令为：
   `fetchmail pop.mailhost.com -p pop3 -u <username>-k`
3. 如果你想对同一个提供商使用 `IMAP`：
   `fetchmail imap.mailhost.com -p IMAP -u <username>-v`

### 工作原理

本配方展示了如何安装和测试 `Fetchmail`，它为任何拥有本地邮箱的用户账户提供了自动取回邮件的功能。因此，对于使用 `POP3` 或 `IMAP` 连接到邮件服务器的客户端来说，通过这种方式获取的邮件就像普通的入站邮件一样。

# 第 11 章

请记住，虽然某些电子邮件供应商允许用户自行决定是否要使用 `SSL` 安全连接，但像 `gmail.com` 这样的主机只允许安全连接。这意味着如果本配方中显示的示例命令不支持没有 `SSL` 连接的 `POP3/IMAP` 访问，那么它在每个主要的邮件提供商上都可能失败。请继续下一节学习如何使用带有 `SSL POP3/IMAP` 加密的 `Fetchmail`。

如果您的邮件提供商同时提供两者，您应该选择 `SSL` 加密。此外，像 `gmail.com` 这样的提供商仅允许用户通过网页版使用服务，并默认禁用了 `POP3/IMAP` 服务功能；您需要在提供商网站的账户设置中启用这些功能（见后文）。

我们使用 `-p` 参数指定了与 `fetchmail` 命令配合使用时使用的邮件协议。通过 `-u` 参数，我们指定了登录邮件服务器时使用的用户标识，这完全取决于您的电子邮件提供商。对于 `POP3`，我们使用了 `-k` 标志以确保邮件不会被删除（这是使用 `POP3` 协议时的默认设置）。最后，我们使用 `-v` 让输出更详细，为我们的简单测试提供更多信息。如果您的电子邮件提供商支持 `SSL`，您还需要在 `Fetchmail` 命令中添加 `-ssl` 标志，以及邮件服务器的根证书（更多信息请见下一节）。如果您运行之前的命令，`Fetchmail` 将立即向邮件服务器请求收件箱中的任何邮件，并将其下载到用户的本地邮箱。

### 更多内容……

在这一节中，我们将向您展示如何配置 `Fetchmail`，使用 `Postfix` 服务器和配置文件，通过 `POP3S`、`IMAPS`、`POP3` 和 `IMAP` 协议从一些真实的邮件提供商下载所有邮件到您的本地邮箱。最后，我们将展示如何实现 `Fetchmail` 过程的自动化。

# 使用 gmail.com 和 outlook.com 账户配置 Fetchmail

在这里，我们将配置 `Fetchmail` 将下载的外部邮件账户：分别是流行的 `gmail.com` 和 `outlook.com` 电子邮件提供商，以及一个 `my-email-server.com` 的假设账户。

正如在主配方中学到的，`Fetchmail` 默认在命令行上接收配置选项，因此这不应该是您使用 `Fetchmail` 自动从不同邮件账户下载邮件的首选方式。通常情况下，`Fetchmail` 应该在启动时作为守护进程模式运行，或者通过 `cron` 任务运行，并按照特定的时间间隔在特殊的配置文件中轮询邮件服务器列表。通过这种方式，您可以方便地配置多个邮件服务器和其他列表。

# 提供邮件服务

在编写此书时，为了让 `gmail.com` 与 `Fetchmail` 工作，您需要使用用户账户登录 `gmail.com` 网站，并在“转发和 POP/IMAP”的账户设置中启用 `IMAP`。此外，在“我的账户”的“登录和安全”下，启用“安全性较低的应用”。对于 `outlook.com`，请在网页上登录您的邮件账户，然后点击“选项”，再次点击“选项”，然后点击“使用 POP 连接设备和账户”，然后启用 `POP`。

![](img/a6dbf7df749be83c0faae2334e970c0b_682_0.png)

`outlook.com` 和 `gmail.com` 均使用安全的 `POP3S` 和 `IMAPS` 协议，因此您需要下载并安装与您的 `Fetchmail` 服务器加密 `SSL` 证书的根证书，才能使用它们的服务。在这里我们可以安装 `Mozilla CA` 证书包，该包由 `Mozilla` 基金会编译，包含了所有主要网站和服务和服务最常用的根证书，例如我们邮件提供商所使用的。对于 `gmail.com`，我们需要 `Equifax Secure Authority` 根证书 `Globalsign`。`Fetchmail` 需要这些根证书来验证从邮件服务器下载的任何 `SSL` 证书的有效性。登录您的 `Postfix` 服务器并安装以下内容：

```
yum install-ca-certificates
```

之后，以 `Linux` 系统用户（例如 `john`）登录，该用户将创建一个新的 `Fetchmail` 配置文件，并且我们的服务器上已经有一个位于其家目录 `~/Maildir` 的 `Postfix` 邮箱目录。在 `Fetchmail` 配置文件中配置任何账户之前，您应该始终使用 `Fetchmail` 命令行测试与特定账户的连接和验证，如之前的配方所示。为了测试我们不同的邮件提供商账户，我们需要使用 `--ssl` 标志，以下是对于允许非 `SSL` 连接的邮件提供商的典型输出：

```
Fetchmail: SSL connection failed.

Fetchmail: socket error while fetching from <userid>@mailserver

Fetchmail: Query status=2 (SOCKET)
```

如果您的 `google` 和 `outlook` 用户名在两个邮件提供商都是 `johnndoe`，请尝试使用 `IMAPS` 协议进行测试（在提示时输入您的邮件用户密码）：

```bash
fetchmail imap.gmail.com -p IMAP --ssl -u johnndoe@gmail.com -k -
```

如果登录成功，输出应该类似于（已截断）：

```
Fetchmail: IMAP< A0002 OK johnndoe@gmail.com authenticated (Success)

9 messages (2 seen) for johnndoe at imap.gmail.com.

Fetchmail: IMAP> A0005 FETCH 1:9 RFC822.SIZE
```

# 第 11 章

使用 `POP3S` 测试 `outlook.com`，使用：

`fetchmail pop-mail.outlook.com -p POP3 --ssl -u johndoe@outlook.com -k -v`

成功后，输出应该类似于（已截断）：

```
Fetchmail: POP3> USER johndoe@outlook.com

Fetchmail: POP3 <OK password required

Fetchmail: POP3 <OK mailbox has 1 messages
```
