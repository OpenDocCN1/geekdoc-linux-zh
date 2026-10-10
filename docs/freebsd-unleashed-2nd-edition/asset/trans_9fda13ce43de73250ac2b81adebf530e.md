
## 更多信息

Qpopper 的官方网站是 [http://www.eudora.com/qpopper](http://www.eudora.com/qpopper)。该网站提供了大量有用信息，包括一份 PDF 文档（位于“文档”部分），该文档明确描述了 Qpopper 所有可能的配置选项。该文档是基于 Linux 视角编写的，因此文档中引用的许多路径名与您安装中的路径略有不同。

关于配置文件的使用，尤其是更多详细信息，可以在 `qpopper` 的手册页（man page）中找到。

### 使用 IMAP-UW 配置 IMAP 服务器

Internet 消息访问协议（IMAP）是一种替代 POP 的协议，部分用户更偏好使用它。为了使邮件软件包功能完整，您可能希望您的邮件服务器支持 IMAP，同时保留 POP 和 SMTP 服务。IMAP 与 POP 的根本区别在于：POP 会从服务器下载每封邮件并存储在邮件程序中，而 IMAP 邮件则完全在服务器上访问和操作。

IMAP 客户端（类似于服务器端基于 shell 的邮件客户端）可以拥有多个邮件文件夹，并可以在它们之间转移邮件，就像它们是本地的一样。只有在请求时，邮件才会传输到客户端，除非用户明确删除，否则邮件不会被删除。这为基于 shell 的邮件用户代理（MUA，如 Mutt 和 Pine）提供了移动灵活性，同时具备图形化客户端邮件程序（如 Outlook 和 Eudora）的用户便利性。支持 POP 的大多数邮件客户端也支持 IMAP。

最流行的 Unix IMAP 服务器是华盛顿大学（University of Washington）开发的 IMAP-UW（该团队也开发了一款流行的 MUA Pine，您稍后将会了解到）。它可以通过 ports 获取，路径为 `/usr/ports/mail/imap-uw`，或者通过 packages 集合获取（有关从 ports 或 packages 安装软件的详细信息，请参阅第 14 章）。要在构建时包含 SSL 支持，请在 `make` 和 `make install` 命令行中添加 `USE_SSL=YES`。

> **注意**
> IMAP-UW 的 port 警告了一个安全问题：服务器守护程序中存在已知的缓冲区溢出漏洞，允许 IMAP 用户以自身的用户权限获取 shell 访问权限。这取决于您的具体配置情况，可能成为问题也可能不是。如果您本来就允许用户进行 shell 访问，那么这不会造成问题。但如果您不允许 shell 访问，这则代表了一个安全漏洞。您的选择包括：等待修复此问题的更新、寻找替代的 IMAP 服务器，或者完全禁用 IMAP 并依赖 POP 为您的客户端提供邮件服务。

IMAP-UW 软件包包含一个邮箱测试程序（mbxtest）和四个守护程序可执行文件，它们位于 `/usr/local/libexec`。其中两个，`ipop2d` 和 `ipop3d`，分别是 POP2 和 POP3 服务器。如果您已经在运行 qpopper，则无需安装它们。然而，这些 POP 守护程序具备将 POP 命令管道传输到 IMAP 服务器的能力，因此，如果您希望迁移到纯 IMAP 环境，它们可以为现有的 POP 客户端提供向 IMAP 升级的路径。

安装 IMAP-UW 相当简单。程序本身没有需要编辑的配置文件；只需修改 `/etc/inetd.conf`（因为 IMAP 服务器像 qpopper 一样通过 inetd 运行），并可选地修改 `/etc/pam.d/imap`。

`/etc/inetd.conf` 中注释掉的行完全可以用于 IMAP-UW。只需取消注释即可：

```
# example entry for the optional imap4 server
#
imap4 stream tcp nowait root /usr/local/libexec/imapd imapd
```

然后，重启 inetd：

```
# killall -HUP inetd
```

IMAP 守护程序监听 TCP 端口 143。您可以通过通过 Telnet 连接端口 143 来测试它是否设置正确。按 `Ctrl+I` 并输入 `quit` 来结束会话：

```
# telnet localhost 143
Trying 127.0.0.1...
Connected to localhost.somewhere.com.
Escape character is '^]'.
* OK [CAPABILITY IMAP4 IMAP4REV1 LOGIN-REFERRALS AUTH=LOGIN] localhost.somewhere.com
\*IMAP4rev1 2001.303 at Sun, 10 Jun 2001 11:21:26 -0700 (PDT)
^]
telnet> quit
Connection closed.
```

安装脚本建议将 `/etc/pam.d/imap`（控制级联认证层）中的条目更改得稍微严格一些。可通过取消注释相关行来实现：

```
auth    required    pam_nologin.so    no_warn
auth    sufficient  pam_opie.so       no_warn       no_fake_prompts
auth    requisite   pam_opieaccess.so no_warn
auth    required    pam_ssh.so        no_warn       try_first_pass
auth    required    pam_unix.so       no_warn       try_first_pass
```

您可以对 pop3 的 PAM 脚本（`/etc/pam.d/pop3`）执行相同操作，以提供相同的增强严格性。

> **注意**
> 您可能会在 `/var/log/messages` 文件或 IMAP 客户端软件中注意到警告，提示邮箱存在“漏洞”，并建议将 `/var/mail` 设置为“1777 权限”。这是由 IMAP-UW 服务器（Pine 也会这样做）执行的安全检查。
> 
> FreeBSD 的邮件目录权限为 775，这意味着访问或创建 `/var/mail` 中文件的所有程序必须使用 `setgid` 设置到 mail 组。然而，IMAP-UW 并不运行 `setgid`。因此，当创建锁定文件（防止在接收新邮件时投递邮件）时，它无法在 `/var/mail` 中执行。建议的变通方法是将 `/var/mail` 的权限更改为 1777，允许非特权用户添加和删除文件。但是，只有正确的用户才能修改自己的文件。虽然这不是理想的解决方案，但在大多数情况下足以应对。

您可以像使用 POP3 一样，使用 SSL/TLS 加密来保护 IMAP。当从 ports 构建时，使用 `make USE_SSL=YES` 和 `make install USE_SSL=YES` 代替简单的 `make` 和 `make install`。然后，您可以使用 `make cert` 生成证书，或者简单地将您为 qpopper 创建的证书文件复制到 `/usr/local/certs`（IMAP-UW 期望在此处找到证书）。为了保持一致性，如果您打算将同一证书用于两项受保护的服务，您可能希望修改 qpopper 配置，使其指向 `/usr/local/certs` 中的同一证书。

为 POP3 和 IMAP 两者提供安全的另一种方式是使用 `stunnel`，关于它的介绍将在第 29 章的“保护电子邮件服务（POP3 和 IMAP）”中详述。

### 独立工作站电子邮件

知道如何运行一个完整的邮件服务器是一项优秀的系统管理技能。但如果您的 FreeBSD 机器并非旨在作为为数十名用户提供邮件服务的 Internet 服务器，这项技能帮助不大。如果仅运行工作站，就像运行 Windows 桌面机器一样，使用 GNOME 或 KDE 桌面环境以及图形化生产力应用程序而非服务器工具，该怎么办？

幸运的是，独立工作站的电子邮件设置比完整规模服务器的设置要简单得多。不过，了解如何控制独立工作站环境仍然很重要，并且有一些有趣的技巧使 FreeBSD 的独立计算变得相当方便。

### 使用 Fetchmail 从 POP3 和 IMAP 服务器检索电子邮件

大多数消费级操作系统都有电子邮件客户端程序（如 Outlook、Eudora、Netscape Messenger 等），它们拥有用于检查 POP3 或 IMAP 服务器的内部内置机制。每个程序都以自己的方式获取邮件，并以内部独特的方式存储。FreeBSD 上存在此类 MUA 程序，它们运行正常。

然而，您可能选择在工作站上运行 Mutt、Elm 或 Pine 等 MUA，就像在服务器上那样。这些程序直接操作系统的中央 `/var/mail` 目录及其中的邮件 spool 文件，而不是保持下载消息的内部缓存。这使得您可以在程序之间共享邮箱，使用命令行工具进行搜索，并参与 Unix 多功能性的无数其他见证。

但是，要从存储您电子邮件地址的 POP3 或 IMAP 服务器（例如，所有发往 `frank@earthlink.net` 的邮件都会收集在 `earthlink.net` 服务器上）获取邮件到您的本地 FreeBSD 工作站，需要某个程序建立 POP3 或 IMAP 连接并将新邮件从远程邮箱传递到您的本地邮箱。这个程序就是 Fetchmail，一个由 Eric Raymond 编写的小型但功能多样的实用工具。

Fetchmail 可以从 `ports`（`/usr/ports/mail/fetchmail`）或 `packages` 中安装。它基于主目录中的 `.fetchmailrc` 文件运行。此文件指定要轮询新邮件的远程 POP3 或 IMAP 服务器、检查间隔以及众多其他选项。然后，Fetchmail 按指定内容检索新邮件，并将其中继到工作站上的端口 25，Sendmail 正在此端口监听（在默认配置中）。随后，它将按照通常适用的所有规则（如 `.forward` 文件和邮件别名）将邮件投递到您的本地邮箱。

安装 Fetchmail 后（它在 FreeBSD ports 集合的 `mail` 目录中可用），在使用之前需要配置主目录中的 `.fetchmailrc` 文件。这可以通过两种方法之一完成。

