

服务器账户中的公钥。你可以通过简单地通过电子邮件发送密钥文件或从软盘复制文件来完成此操作。一旦你的服务器上的账户拥有了你的客户端用户的公钥副本，你就可以从客户端账户访问服务器账户。你还将被提示输入服务器账户的密码短语。你必须知道它才能访问该账户。图 18-1 说明了允许用户 george 访问账户 cecelia 的 SSH 设置。

要允许你使用 SSH 访问其他账户，需要以下步骤：

- 在你的账户上创建公钥和私钥以及密码短语。你需要使用此密码短语从另一个账户访问你的账户。
- 将你的公钥分发到你想要访问的其他账户中，将其放置在 .ssh/authorized_keys 文件中。
- 其他账户也必须设置公钥和私钥以及密码短语。
- 你还需要知道其他账户的密码短语才能访问它。

## 使用 ssh-keygen 创建 SSH 密钥

你使用 ssh-keygen 命令创建公钥和私钥。你需要指定要使用的加密类型。你可以使用 DSA 或 RSA 加密。使用 -t 选项并以小写形式指定加密名称（dsa 或 rsa）。在以下示例中，用户使用 RSA 加密创建了一个密钥：

```
ssh-keygen -t rsa
```

ssh-keygen 命令会提示你输入密码短语，它将用作保护你的私钥的密码。密码短语应由多个单词组成。你还将被提示输入密钥的文件名。如果未输入，SSH 将使用其默认值。公钥将获得 .pub 扩展名。ssh-keygen 命令会生成公钥并将其放置在 .ssh/id_dsa.pub 或 .ssh/id_rsa.pub 文件中，具体取决于你指定的密钥类型；它将私钥放置在相应的 .ssh/id_dsa 或 .ssh/id_rsa 文件中。

![](img/6c226e8ba1efd427dec3bf582418d33f_350_0.png)

图 18-1 SSH 设置和访问

> 注意 .ssh/identity 文件名在 SSH 版本 1 中使用；在较旧的发行版版本上可能默认安装。SSH 版本 2 使用不同的文件名，.ssh/id_dsa 或 .ssh/id_rsa，具体取决于使用 RSA 或 DSA 身份验证。

如果需要更改你的密码短语，你可以使用 ssh-keygen 命令和 -p 选项。每个用户都将在自己的主目录中拥有自己的 SSH 配置目录，称为 .ssh。公钥和私钥以及 SSH 配置文件都放在这里。如果你从源代码构建，make install 操作将自动运行 ssh-keygen。表 18-2 列出了 SSH 配置文件。

## 授权密钥

公钥用于验证用户及其主机。你在远程系统上使用公钥允许该用户访问。公钥放置在远程用户账户的 .ssh/authorized_keys 文件中。请记住，公钥保存在 .ssh/id_dsa.pub 文件中。如果用户想从本地账户远程登录到远程系统上的账户，他们首先需要将自己的公钥放置在远程系统上要访问的账户的 .ssh/authorized_keys 文件中。如果用户 larisa 在 turtle.mytrek.com 上想要访问 rabbit.mytrek.com 上的 aleina 账户，larisa 的公钥 /home/larisa/.ssh/id_dsa.pub 首先必须放置在 aleina 的 authorized_keys 文件 /home/aleina/.ssh/authorized_keys 中。larisa 可以发送密钥或让其复制过去。一个简单的 cat 操作可以将密钥追加到授权密钥文件中。在下一个示例中，用户将 larisa.pub 文件中的 aleina 的公钥添加到授权密钥文件。larisa.pub 文件是用户之前收到的 /home/larisa/.ssh/id_dsa.pub 文件的副本。

```
cat larisa.pub >> .ssh/authorized_keys
```

## 加载密钥

如果你定期连接到各种远程主机，你可以使用 ssh-agent 命令将私钥放置在内存中，以便快速访问以解密接收到的传输。ssh-agent 命令 intended 用于在登录会话开始时使用。对于 GNOME，你可以使用 openssh-askpass-gnome 实用程序，通过 ssh-add 调用，它允许你在登录 GNOME 时输入密码。GNOME 将在你使用 SSH 客户端时自动提供该密码。

尽管 ssh-agent 命令使你能够在内存中使用私钥，但你还必须使用 ssh-add 命令将私钥显式加载到内存中。没有参数的 ssh-add 会从你的 .ssh/id_dsa 或 .ssh/id_rsa 文件加载你的私钥。你将被提示输入此私钥的密码短语。要从内存中删除密钥，请使用带 -d 选项的 ssh-add。如果你有多个私钥，可以将它们全部加载到内存中。带 -l 选项的 ssh-add 会列出当前已加载的密钥。

## SSH 客户端

SSH 最初设计用于替代远程访问操作，例如 rlogin、rcp 和 Telnet（参见第 15 章），这些操作不执行任何加密并引入安全风险，例如以明文传输密码。你也可以使用 SSH 对 X 服务器会话以及 FTP 传输进行编码（sftp）。ssh-clients 软件包包含相应的 SSH 客户端

