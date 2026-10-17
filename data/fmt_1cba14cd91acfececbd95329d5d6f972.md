
安全套层 (SSL) 是 FreeBSD 中包含的一组库，用于加密特定服务的流量，即使携带服务流量的数据包被窃听者截获，如果没有正确的加密密钥也无法解密。SSL 最常用于网络流量（如第 30 章所示）；但它的使用不仅限于 HTTP，对于 POP 等服务也有益。

默认情况下，Qpopper 在构建时将带有隐式 TLS/SSL 支持。然而，为了利用它，你需要使用 FreeBSD 内置的 OpenSSL 库创建并安装证书。首先，为你的证书创建一个目录：

```
# mkdir -p -665 /etc/mail/certs
# chown root:mail /etc/mail/certs
# chmod 660 /etc/mail/certs
```

接下来，使用 `openssl` 命令生成证书请求。这将要求你输入关于你组织的几条信息（在此处显示的示例中，“...”表示产生证书请求文件的长时间交互式会话）。之后，确保私钥文件 (`cert.pem`) 的权限仅允许 root 视查看：

## 使用 Qpopper 配置 POP3 服务器

```
# openssl req -new -nodes -out req.pem -keyout /etc/mail/certs/cert.pem

# chmod 600 /etc/mail/certs/cert.pem
# chown root:0 /etc/mail/certs/cert.pem
```

完成后后，你需要向证书颁发机构 (CA，也可能是 VerSign）注册证书，并将 `req.pem` 中的证书请求提交给 CA。然后你将获得一个经过签名的证书。将其合并到你的其中一个 `cert.pem` 中：

```
# cat signed_req.pem >> /etc/mail/certs/cert.pem
```

或者，用新的签名证书 `signed_req.pem` 替换旧的 `cert.pem`。

现在，为 `/usr/local/etc/qpopper/qpopper.conf` 文件添加 TLS/SSL 支持，重启服务器（如果它在独立模式下运行），SSL 加密就属于你了。任何配置恰当的 SSL 客户端都能够协商安全连接。

以下行是应该添加到 `qpopper.conf` 文件中的：

```
set tls-support = stls
set tls-server-cert-file = /etc/mail/certs/cert.pem
```

有时，向第三方机构注册证书是不可行的。如果你愿意，可以模拟证书颁发机构来创建一个自签名证书，用它来确保你的系统运行。然而，启用 SSL 的客户端不会信任此证书，并将要求用户在继续之前手动批准它。

首先，创建 CA 的私钥（确保记住你插入口令），然后创建 CA 证书：

```
# openssl genrsa -des3 -out ca.key 1024

# openssl req -new -x509 -days 365 -key ca.key -out ca.crt
```

现在，你可以对之前创建的证书 (`req.pem`) 进行自签名：

```
# openssl x509 -req -CA ca.crt -key ca.key -days 365 -in req.pem --out signed-req.pem - -createserial
```

这将允许你运行一个启用 SSL 的 Qpopper 服务器以测试其功能。请确保在某时刻获取真实的 CA 签名证书！

## 更多信息

尽管 Qpopper 不再由 Qualcomm 支持，但其官方网站可以在 http://www.eudora.com/products/unsupported/qpopper/ 访问。它包含许多有用信息，包括一份 PDF 文档（在 Documentation 部分），描述了 Qpopper 的所有可能的配置选项。它是从 Linux 编写的

# 独立工作站的电子邮件

了解如何运行完整的电子邮件服务器是一项出色的系统管理技能。如果你的 FreeBSD 机器并不作为一个为几十个用户提供邮件服务的互联网服务器，那么这项技能对你的帮助可能并不大。如果你运行的是工作站呢？就像运行 Windows 桌面那样，带有 Gnome 或 KDE 桌面以及图形化生产力应用程序而不是服务器呢？

幸运的是，独立工作站的电子邮件设置比全规模服务器简单得多。FreeBSD 的默认配置是启动一个“提交”（submission）Sendmail 进程（`/etc/defaults/rc.conf` 中的默认设置为 `sendmail_enable=YES`），你不需要在 `/etc/rc.conf` 中添加任何关于 Sendmail 的内容，即可允许系统从本地邮件客户端将邮件发送到远程 SMTP 服务器。

尽管如此，了解如何控制独立环境并根据需求自定义其行为仍然重要，而且有一些有趣的技巧可以使 FreeBSD 上的独立计算比通常情况下更加方便。

# 使用 Fetchmail 从 POP3 和 IMAP 服务器检索邮件

大多数消费级操作系统都带有邮件客户端程序（如 Outlook、Apple Mail、Mozilla Thunderbird 等），它们有各自的内置机制来检查 POP3 或 IMAP 服务器。每个程序都以自己的方式获取邮件并以自己的方式存储。正如早些所述（特别是第 6 章），FreeBSD 也存在此类 MUUA（邮件用户代理），它们的工作方式正如你预期任何程序运行的方式一样。

然而，你可能会选择在本地工作站上运行基于 shell 的 MUA，如 Mutt、Elm 或 Pine，就像在服务器上运行一样。这些程序直接在系统的 `/var/mail` 目录及其内部邮件池上操作，而不是保留下载消息的内部缓存。这允许你在不同程序之间共享信箱，使用命令行工具进行搜索，并以许多其他方式利用邮件系统的多功能和开放性，使其按照你想要的方式运行，例如编写自己的脚本来解析邮件池并根据你的需求对其进行处理。

但要将邮件从存储邮箱地址的 POP3 或 IMAP 服务器（例如，所有发送到 frank@earthlink.net 地址的邮件都会在 earthlink.net 服务器上）获取到本地 FreeBSD 工作站，需要某些工具来建立 POP3 或 IMAP 连接并将新消息从远程信箱投递到本地。Fetchmail 是由 Eric Raymond 编写的一个小巧但多功能的实用。

Fetchmail 可以通过端口（`/usr/ports/mail/fetchmail`）或软件包安装。它作为用户进程运行，按需执行，并从你家目录下的 `.fetchmailrc` 获取运行时配置。该文件指定了要轮询新邮件的远程 POP3 或 IMAP 服务器、检查间隔以及许多选项。

Fetchmail 在检索新邮件时会将其中继到你工作站的 25 端口，那里 Sendmail 正在监听传入的 SMTP 连接。然后，它将根据所有通常应用的规则（例如 `.forward` 文件和邮件别名）将邮件投递到你的本地信箱。

在安装 Fetchmail 后（它在 FreeBSD 端口集合的 mail 目录中可用），你需要在使用它之前配置你家目录下的 `.fetchmailrc`。这可以通过两种方法之一完成。

第一方法是使用 `fetchmailconf` 程序。这是一个用 Python 编写的 Fetchmail 图形化程序，使用了 Tcl 工具包（一个用于在 X11 系统中构建图形用户面的工具包）。尽管 `fetchmailconf` 与 Fetchmail 程序一同提供，但它需要安装 Python 和 Tcl/Tk 才能工作。（Python 和 Tcl/Tk 都是许多不同平台的流行语言。）

第二方法是通过手动创建 `.fetchmailrc` 文件来配置 Fetchmail。配置文件的格式非常直观，Fetchmail 管理器非常优秀，详尽涵盖了 `.fetchmailrc` 文件中可以包含的每一个细节。我们将在本章中使用这种方法。

# 配置 .fetchmailrc 文件

在你的家目录下，用你喜欢的文本编辑器打开名为 `fetchmailrc` 的新文件。你创建的 `.fetchmailrc` 文件将包含三个部分：全局（global）、服务器选项（server options）和用户选项（user options）。

> 注意
>
> `.fetchmailrc` 文件的部分必须完全按照此处显示的顺序出现，这非常重要。还要注意，一旦开始了一个新部分，就无法使用属于上一个部分的选项。`.fetchmailrc` 文件中常见的错误原因之一是选项顺序错误或位置不正确。

本章没有涵盖 `.fetchmailrc` 可用的所有选项，因为选项非常多。我们将做的是创建一个从 POP3 服务器检索邮件的示例设置，这是一个非常常见的用户场景。使用本节提供的信息作为让 Fetchmail 运行起来的起点。然后，如果你有任何高级配置的需求，请参考 Fetchmail 页面。
