
`ssh` 程序建立加密连接，并以安全方式将登录数据传递给服务器。从那时起，它的作用与普通 Telnet 连接完全一样——就用户而言没有区别。FreeBSD、Linux、Unix 或 Mac OS X 系统上的用户可以使用此过程连接到您的机器。

使用 Windows 或经典 Mac OS 等桌面客户端系统的用户需要做的工作稍微多一点。这些平台没有命令行 SSH 客户端程序，但有一些出色的图形终端程序整合了 Telnet 和 SSH 功能：Windows 用户可以使用 SecureCRT（来自 Van Dyke，http://www.vandyke.com）或 SSH（来自 SSH Communications Security，http://www.ssh.com），而 Mac OS 9 用户可以使用 NiftyTelnet/SSH 或 MacSSH。Windows 程序往往是商业产品，而大多数 Mac 程序是共享软件。

您的任务是说服用户切换到 SSH 而不是使用 Telnet。通过您发布的服务器策略让他们都知道，建议他们使用 SSH 来保护自己（视情况而定）；然而，这并不能保证他们会使用，而且作为管理员，您仍然面临攻击者嗅探那些选择不使用 SSH 的人的连接威胁。一种更强制但完整的方法是完全禁用 Telnet，并要求用户改用 SSH。要禁用 Telnet，请注释掉 `/etc/inetd.conf` 中的 `telnetd` 行：

```bash
# telnet stream tcp nowait root /usr/libexec/telnetd telnetd
```

然后，重新启动 `inetd` 进程：

```bash
# killall -HUP inetd
```

> **注意**
> SSH 有两种流行的协议版本：SSH1 和 SSH2。FreeBSD 支持两者，但 SSH1 的设计较差，比 SSH2 更有可能表现出安全漏洞。您可以通过在 `/etc/ssh/sshd_config` 中添加以下行来禁用 SSH1：
>
> ```bash
> Protocol 2
> ```
>
> 但是，请注意，并非所有消费者 SSH 客户端都完全支持 SSH2。除非必要，否则不必担心禁用 SSH1。

## 保护电子邮件服务 (POP3 和 IMAP)

可以说，POP3 和 IMAP 比 Telnet 更容易受到明文安全风险的影响。如果您的用户设置了电子邮件客户端，使其每五分钟或左右连接到服务器检查新消息，那么每次这些连接发生时，都会发生明文可见的登录和密码交易，导致密码泄露的可能性更高——特别是因为这些服务会在可预测的固定间隔发送其敏感数据。如果强制在服务器上实施 SSH 而不是 Telnet，从您的利益出发，也应同样对待电子邮件服务。

您在第 25 章中学习了如何保护 Qopop 程序，使用 FreeBSD 内置的安全套接字层 (SSL) 工具来加密 POP3 连接。您可以使用相同的方法来保护 IMAP，采用 IMAP-UW 软件包。您可以通过使用证书颁发机构生成证书（正如您在第 24 章“启用 SSL 加密”中所学到的）来启用 IMAP-UW 中的 SSL 支持。如果您为网站上的其他服务（例如 Qopop）生成了证书，您可以将相同的证书用于 IMAP-UW。有关更多详细信息，请参阅 http://www.washington.edu/imap/ 上的 IMAP-UW 文档。

`stunnel` 程序提供了一种替代方案，用于同时加密 POP3 和 IMAP。`stunnel` 集中管理您的 SSL 证书，而不使用每个服务内置的 SSL 支持。`stunnel` 也可在 `ports`（`usr/ports/security/stunnel`）中找到，它允许您为系统中的任何选定服务建立通用的 SSL 隧道。如果您从 `ports` 安装 `stunnel`，其默认启动脚本（`/usr/local/etc/rc.d/stunnel.sh.sample`）会在端口 993（用于 IMAP）和 995（用于 POP3）上启动监听进程，这些是这些协议安全版本通用的接受端口，如您可以在 `/etc/services` 中看到的那样。

> **注意**
>
> 请记住将 `stunnel.sh.sample` 重命名为 `stunnel.sh`，正如您在第 10 章“系统配置和启动脚本”中“资源配置脚本”部分所学到的那样。添加 `.sample` 后缀是为了确保您查看脚本内容，以确认 `.pem` 证书文件的路径是否正确。

如果您选择使用 `stunnel`，您仍然需要生成一个证书，就像使用 POPper 和 IMAP-UW 一样。`stunnel` 证书应放置在 `/usr/local/etc/stunnel.pem`。一旦放置到位，您的 POP3 和 IMAP 客户端应该能够连接到相应端口以建立安全连接（IMAP 使用 993 代替 143，POP3 使用 995 代替 110）。

> **警告**
>
> 许多流行的电子邮件客户端程序（如 Microsoft Outlook）支持 POP3 和 IMAP 的 SSL 加密，但其他程序可能仅支持其中一种或都不支持。在其他电子邮件客户端程序中，这种支持可能不完整或为可选功能。要求用户使用 SSL 可能意味着要求他们更换电子邮件程序，这是许多人不喜欢做的事情。

此外，请注意 `stunnel` 不是 POP3 或 IMAP 的替代品。相反，它是一种增强——即向任何指定服务添加通用的 SSL 功能。这意味着常规 POP3 和 IMAP 服务仍然必须启用；您不能从 `/etc/inetd.conf` 中移除这些服务。如果您想强制执行“仅安全连接”策略，则需要使用 `IPFW`（您稍后在本章中会看到）来禁止除 `localhost` 以外的任何主机连接这些端口。

## 保护 FTP

正如您在第 26 章“配置 FTP 服务器”中学到的，FTP 是另一种明文服务，具有固有的密码认证，因此有可能被监控网络流量的攻击者利用。用户经常使用 FTP 进行诸如上传网页等操作，但它不像 POP3 或 IMAP 那样在可预测的固定间隔内使用。这使得 FTP 比 Telnet 对您系统的风险稍低，但仍然值得保护。

幸运的是，实现安全 FTP 与 SSH 一样简单。如果您已启用 SSH（如本章前面“保护终端流量”部分所学），您的系统就可以使用安全 FTP。加密的 FTP 会话实际上是通过 SSH 通道操作的，SSH 客户端建立终端连接，在服务器端启动 `/usr/libexec/sftp-server` 程序，并通过加密通道打开必要的连接回到客户端。安全 FTP 客户端随后对用户表现为透明操作，就像常规的 FTP 程序一样。

在 FreeBSD 中，作为 OpenSSH 一部分的内置 `sftp` 程序负责处理安全 FTP 会话的客户端端。在 Windows 中，SSH Communications Security 包提供了一个适用于 FreeBSD 的安全 FTP 客户端。前面提到的 Mac OS X 客户端（NiftyTelnet 和 MacSSH）也具有安全 FTP 功能，并且 Mac OS X 拥有命令行工具 `lsftp`。

通过安全通道进行文件传输的另一种替代方法是使用 `scp`。这使您可以使用登录认证将文件复制进出远程服务器，其方式与 `rcp` 类似（有关细节请参阅 `man rcp` 和 `man scp`），不同之处在于 `scp` 通过加密的 SSH 隧道进行操作。某些 SSH 客户端（如适用于 Mac 的 NiftyTelnet/SSH）支持通过此方式进行文件传输。

要使用 `scp` 将文件从本地机器传输到远程 SSH 服务器，请使用如下命令：

```
# scp file.txt stripes:
frank@stripes's password:
file.txt 100% |*************************************|  511  00:00
```
