
`define` 条目为 Sendmail 内部的宏赋值，而 `INPUT_MAIL_FILTER` 语句告诉 Sendmail 通过指定的 Unix 域套字运行入站邮件。

我将这些行添加到 `sendmail.mc` 并运行了 `make all`。Sendmail 突然杀了我正在运行的 `milter-greylist` 进程，15 分钟后，我源不断的垃圾邮件流变成了细小的纯净、合法的邮件⁵。

## 使用 SASL 进行 Sendmail 认证

你那些有问题的用户是那些想要世界任何地方使用你的邮件设施的用户。邮件服务器将接受来自任何地方的邮件，只要它是给该机器的用户。然而，当你的总裁飞往南极的大客户那里时，他期望邮件服务器接收他的信息，尽管你采取了所有旨在排除垃圾邮件者的复杂中继控制。你可以通过简单身份验证安全层 (SASL) 实现这一点。SASL 要求用户在服务器为客户端转发邮件之前向邮件服务器进行身份验证。这意味着合法用户可以在世界的任何地方使用邮件交换器，而无法身份验证的用户只能从已知的 IP 地址使用。

在 Sendmail 中支持 SASL 需要从源码重新编译 Sendmail。为了避免破坏基础系统的 Sendmail，FreeBSD 在 `/usr/ports/mail/sendmail` 中包含一个 Sendmail 的 port。你可以使用自定义选项编译 Sendmail 并用它代替基础系统的 Sendmail。使用 port 意味着你可以根据自己的规格轻松重建 Sendmail，而无需对基础系统的 Sendmail 应用补丁（并防止你的下次升级覆盖它们）。如果你查看 port 的 Makefile，你会发现 Sendmail 支持许多选项，从数据库后端到 LDAP 集成。进入 port 目录并输入：

```
# SENDMAIL_WITH_SASL=YES all install
```

这将构建 Sendmail 版本 2 和一个感知 SASL 的 Sendmail，并像其他 port 一样将其安装在 `/usr/local` 下。

> ⁵ 只接收非垃圾邮件意味着我真的回答了其中任何内容，而是我似乎达到了这样一个阶段：我的主要目标是停止接收信息。

## sasL-8

你那些有问题的用户是那些想要世界任何地方使用你的邮件设施的用户。邮件服务器将接受来自任何地方的邮件，只要它是给该机器的用户。然而，当你的总裁飞往南极的大客户那里时，他期望邮件服务器接收他的信息，尽管你采取了所有旨在排除垃圾邮件者的复杂中继控制。你可以通过简单身份验证安全层 (SASL) 实现这一点。SASL 要求用户在服务器为客户端转发邮件之前向邮件服务器进行身份验证。这意味着合法用户可以在世界的任何地方使用邮件交换器，而无法身份验证的用户只能从已知的 IP 地址使用。

在 Sendmail 中支持 SASL 需要从源码重新编译 Sendmail。为了避免破坏基础系统的 Sendmail，FreeBSD 在 `/usr/ports/mail/sendmail` 中包含一个 Sendmail 的 port。你可以使用自定义选项编译 Sendmail 并用它代替基础系统的 Sendmail。使用 port 意味着你可以根据自己的规格轻松重建 Sendmail，而无需对基础系统的 Sendmail 应用补丁（并防止你的下次升级覆盖它们）。如果你查看 port 的 Makefile，你会发现 Sendmail 支持许多选项，从数据库后端到 LDAP 集成。进入 port 目录并输入：

```
# SENDMAIL_WITH_SASL=YES all install
```

这将构建 Sendmail 版本 2 和一个感知 SASL 的 Sendmail，并像其他 port 一样将其安装在 `/usr/local` 下。

## mailer.conf

你那些有问题的用户是那些想要世界任何地方使用你的邮件设施的用户。邮件服务器将接受来自任何地方的邮件，只要它是给该机器的用户。然而，当你的总裁飞往南极的大客户那里时，他期望邮件服务器接收他的信息，尽管你采取了所有旨在排除垃圾邮件者的复杂中继控制。你可以通过简单身份验证安全层 (SASL) 实现这一点。SASL 要求用户在服务器为客户端转发邮件之前向邮件服务器进行身份验证。这意味着合法用户可以在世界的任何地方使用邮件交换器，而无法身份验证的用户只能从已知的 IP 地址使用。

## IMAP 和 POP3

等一下，我忘了 de de de。在你的环境中，你的 `mailer.conf` 看起来像：

```
sendmail          /usr/sbin/sendmail
mail             /usr/sbin/mailx
newaliases       /etc/mail/newaliases
hosts            /etc/hosts
```

## 构建 sendmail.cf

当你使用 Dovecot 时，你可能会发现将证书放在 `/etc/ssl` 会更加简单。例如，如果你使用 Dovecot，你可能会发现将证书放在 `/etc/ssl` 会更加简单。例如，如果你使用 Dovecot，你可能会发现将证书放在 `/etc/ssl` 会更加简单。例如，如果你使用 Dovecot，你可能会发现将证书放在 `/etc/ssl` 会更加简单。

IMAP 服务器可以像 IMAP 一样提供 POP3 服务，因此一个守护进程就能满足我们所有的需求。我们将介绍基于 SSL 的 POP3，它可以为用户名和密码提供保护，并隐藏邮件内容。

简单的 IMAP 服务器（如 `imap-wu`）让你能够客户端与 `/var/mail` 中的标准 Unix 邮件池进行同步。其他服务器（如 Cyrus IMAP）则支持数万个用户。Dovecot IMAP 服务器是一个很好的折中方案，它功能齐全可以支持大多数环境，但又简单到不需要专门的人员。此外，Dovecot 的作者已拿出了一千欧元的奖金，奖励给第一个“证明 Dovecot 中存在可远程利用的安全漏洞”的人。许多人花费了大量时间尝试获取该奖金，但目前还没有人成功。

## 安装 Dovecot

你可以在 `/usr/ports/mail/dovecot` 找到 Dovecot。Dovecot 可以与 LDAP 服务器、不同类型的数据库以及不同的身份验证系统协作；它还支持许多其他配置选项。但对于我们的基础邮件服务器，我们只需要在 FreeBSD 系统上安装标准的 Dovecot 服务器即可。进入目录并运行 `make install clean`。

Dovecot 会在 `/usr/local/share/doc/dovecot` 安装大量文档，并在 `/usr/local/etc` 安装示例配置文件。它有许多配置设置，最好保持默认状态，除非你明确需要该功能。我们将专注于通过 SSL 同时提供 POP3 和 IMAP 服务。虽然你也可以提供不带 SSL 或或其他加密保护的电子邮件服务，但在当今的互联网上，这是一个非常糟糕的主意。

## 配置 Dovecot

复制 Dovecot 配置文件 `/usr/local/etc/dovecot.conf`，然后用文本编辑器打开它。信不信由，要让 Dovecot 在 FreeBSD 上安全运行，你只需要做很少修改。

默认情况下，Dovecot 提供未加密的 IMAP 和 POP3 服务。这是今天互联网上的常见标准，但所有现代客户端都支持通过安全的 SSL 连接传输身份凭据和消息。协议定义了 Dovecot 提供的条目。通过在它们末尾添加 `s`，将 IMAP 和 POP3 条目改为 SSL 版本：

```
protocols = imaps pop3
```

现在使用 `ssl_cert_file` 和 `ssl_key_file` 变量定义 Dovecot 存放 SSL 证书的位置。Dovecot 包含一个创建一个正确的自签名证书的脚本，或者你可以像第 9 章讨论的样商业证书。

```
ssl_cert_file = /etc/ssl/certs/dovecot.pem
ssl_key_file = /etc/ssl/private/dovecot.pem
```

如果你更改了提供的默认路径，必须编辑自签名证书脚本以反映正确的路径。一个 FreeBSD 原教主义者会告诉你编辑脚本并将证书放在 `/usr/local/etc/ssl`，但每当你更新 Dovecot 时，你都需要再次修改脚本。只要你记录了系统是如何配置的，SSL 文件的位置并不太重要。

## 创建 Dovecot SSL 证书

虽然你可以像第 9 章描述那样创建一个自签名证书，但 Dovecot 包含一个 shell 脚本来为你创建此证书并按照 Dovecot 的意愿进行安排。`/usr/local/share/dovecot` 目录包含该脚本和一个配置文件。用文本编辑器打开配置文件 `dovecot-openssl.cnf`。这些设置看起来与第 9 章非常眼熟，但由于已经是快半本书以前的事了，我们将快速浏览一下。

文件头部包含证书类型和强度等设置。让它们保持原样。不过，你可以在下方设置值以反映你的环境。

`C` 变量是你的两位国家代码。我在美国，所以我会写 `C=US`。

`ST` 是你的州或省，`L` 是你的地区或城市。我来自密歇根州底特律，所以我写：

```
ST=Michigan
L=Detroit
```

`O` 是组织单位。如果你有公司，在这里列出。如果没有，列出你的名字。

`OU` 是组织部门，或负责该系统的组织部分。我通常在这里写 Email Team。

通用名称（common name）是客户端连接邮件的服务器的反向 DNS 名称，它几乎与你邮件服务器的主机名相同。例如，你的邮件服务器通用名称为 `bewilderbeast.blackhelicopters.org`。

`emailAddress` 是负责此服务器的人员地址。这可能组或角色账户，例如 `helpdesk@company.com`。

这就是 Dovecot 生成你自己的自签名证书所需的所有配置。现在运行 `mkcert.sh`：

```
/usr/local/share/dovecot/mkcert.sh
```

砰！你的自签名证书准备好了。

## 运行 Dovecot

在 `/etc/rc.conf` 中通过 `dovecot_enable="YES"` 启用 Dovecot，然后运行 `/usr/local/etc/rc.dovecot`。`/var/log/mailog` 将显示 Dovecot 启动并告诉你它正在初始化 SSL。

你现在应该有一个运行中的 Dovecot 服务器了！配置你的客户端与服务器通信并尝试一下。确保要求 SSL 连接！任何错误都将出现在 `/var/log/mailog` 中。

现在困难的部分是区分服务器错误和客户端错误。所有的客户端邮件都有自己的问题、小故障和功能。将客户端错误与服务器问题分开，特别是当涉及不熟悉的软件时，可能会非常恼人。客户端故障排除中的一项关键技能是在能够在不依赖……的情况下测试邮件账户的能力。

## 测试 POP3

我们将使用 POP3 来测试服务器是否正常。首先，我们将使用邮件客户端连接服务器并下载邮件。我们将使用一个名为 `telnet` 的简单程序来实现此目的。

```
telnet bewilderast.blackhelicopters.org 110
```

连接后，我们使用 `USER` 命令识别身份：

```
USER mlucas
```

然后我们使用 `PASS` 命令提供密码：

```
PASS notmyalpassword!
```

现在我们已通过身份验证，使用 `LIST` 命令查看可用的邮件：

```
LIST
```

服务器将返回类似的内容：

```
+OK 2 messages
1 1391
2 4258
```

要查看第一条邮件，我们使用 `RETR` 命令：

```
RETR 1
```

服务器随后发送邮件内容。从服务器上删除邮件，我们使用 `DELE` 命令：

```
DELE 1
```

最后，我们使用 `QUIT` 关闭连接：

```
QUIT
```

## 测试 IMAPS

你可以像测试 POP3 一样测试 IMAPS，但命令更多。首先，我们将再次使用 `telnet` 打开到服务器的连接：

```
telnet bewilderast.blackhelicopters.org 993
```

连接后，我们将使用 `LOGIN` 命令进行身份识别和验证：

```
LOGIN mlucas notmy3alpassword!
```

现在我们已连接，使用 `LIST` 命令查看 IMAP 知道哪些目录：

```
LIST " *"
```

服务器将返回类似的内容：

```
* LIST (NoInfers\Unmarked) "/" "Junk E-mail"
* LIST (NoInfers\Unmarked) "/" "mlucas"
* LIST (NoInfers\Unmarked) "/" "INBOX"
```

现在我们使用 `SELECT` 命令查看 INBOX 中有什么：

```
SELECT INBOX
```

服务器将返回类似的内容：

```
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS\Answered \Flagged \Deleted \Seen \Draft\]) permitted.
* 2 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 118S130816] UIDs valid
* OK [UIDNEXT 3] Predicted next UID
```

我的默认邮件文件夹有 2 条消息。我们看到下一条消息编号是 3，因此消息的编号是 1 和 2。让我们看看通过输入以下命令来获取第一条消息：

```
06 UID fetch 1:1 (UID RFC822.SIZE FLAGS BODY.PEEK[]])
```

你应该能看到用户默认邮件文件夹中的第一封邮件内容显示在屏幕上。（如果你已经运行 IMAP 一段时间了，你的邮件服务器可能有一条编号大于 1 的消息。）最后，使用 07 LOGOUT 断开 IMAP 连接。

如果你能完成所有这些操作，你就拥有了基本的基于 SSL 的 IMAP 功能。请检查你的客户端配置。

虽然你可以通过 Sendmail 和 Dovecot 实现更深的功能，但你现在可以为企业用户和客户提供基础电子邮件服务了。让我们来学习如何在 FreeBSD 上提供 Web 服务。

## 17

## WEB 和 FTP 服务

![](img/b00144f770bf509a54e1d770bb05a101_530_0.png)

Internet 起于 20 世纪 70 代，但直到 90 年代 Web 的出现才成为家喻户晓的名称。Netscape 公司采用了 Mosaic Web 浏览器并将其商业化，引发了一场仍在持续的信息和通信革命。尽管许多点com 公司倒闭了，但全球个人与个人通信的时代是从 Netscape 浏览器开启的。点对点文件共享等技术进一步扩展了互联网，但当人们提到“Internet”时，大多数人脑海中浮的是 Web。

FreeBSD 的 Web 服务器性能是传奇级的。多年来，某些微软子公司倾向于使用 FreeBSD 而不是自己的 Windows 平台，微软甚至发布了针对 FreeBSD 的共享源码 .NET 工具包。Yahoo! 以及其他各种高需求 Web 服务器集群都在运行 FreeBSD。Net 对全球最可靠的托管服务的调查始终显示，约三分之一的服务运行在 FreeBSD 上。你可以在 FreeBSD 上构建自己的高可靠 Web 和 FTP 服务。

### Web 服务器如何工作

基础的 Web 服务器非常简单：Web 浏览器与服务器建立 TCP 连接并请求页面；Web 服务器输出页面并关闭连接。这是简单的部分。当你使用服务器模块、动态页面等时，情况会变得复杂得多。

Web 使用超文本传输协议（HTTP），这是一种类似于 POP3 的非常简单的协议。在过去的几年里，HTTP 增加了许多功能使其变得复杂，但基础的 HTTP 操作简单到可以手动完成。自己试一下——telnet 到服务器的 80 端口并输入 GET ：

```
# telnet www.blackhelicopters.org 80
Trying 198.22.63...
Connected to www.blackhelicopters.org.
Escape character is '^'.
GET http://www.blackhelicopters.org/
<HTML>
<body bgcolor="black">
<center><font color="white">这里什么也没有看。<br>这不是你正在寻找的站点。</br></center>
Connection closed by foreign host.
```
