

在邮件列表能够接收电子邮件之前，您需要将 `newlist` 生成的行复制到 `/etc/aliases` (第 675 页) 的末尾，并运行 `newaliases`。

Mailman 包含一个 Web 配置界面，您可以通过配置 Web 服务器来运行 `/usr/lib/mailman/cgi-bin` 中的脚本来启用它。请参阅文件 `/etc/httpd/conf.d/mailman.conf`，其中包含一个示例条目，您可以将其放入 `/etc/httpd/conf/httpd.conf` (第 850 页) 以设置此接口（`pipemail` 是 Mailman 使用的归档管理器）。

## 设置 IMAP 或 POP3 服务器

有两种协议允许用户远程获取电子邮件：IMAP（Internet Message Access Protocol，互联网消息访问协议）和 POP（Post Office Protocol，邮局协议）。`dovecot` 包 (www.dovecot.org) 包含了实现这些协议的 `imap-login` 和 `pop3-login` 守护进程。通常您不需要修改 `dovecot` 配置文件（`/etc/dovecot.conf`）。更多信息请参见 `/usr/share/doc/dovecot*`。

rpm 安装脚本会在 `/etc/pki/dovecot/certs/dovecot.pem` 和 `/etc/pki/dovecot/private/dovecot.pem` 中创建 `dovecot` 所需的自签名证书。

运行 `chkconfig` 以便在系统进入多用户模式时启动 `dovecot` 守护进程：

```
# /sbin/chkconfig dovecot on
```

使用以下命令启动守护进程：

```
# /sbin/service dovecot start
Starting Dovecot Imap:		[ OK ]
```

尽管 `dovecot` 报告仅启动了 IMAP 服务器，但它同时也启动了 POP3 服务器。

## 认证中继

如果您带着便携式计算机（如笔记本电脑）出差，您可能会在工作地点通过不同的连接接入互联网。也许是因公出差，或者您可能只是晚上把笔记本电脑带回家。

如果您总是通过 ISP（互联网服务提供商）拨号接入网络，则本节不适用。在这种情况下，您始终连接到 ISP 的网络，就好像您的计算机从未移动过一样。

在笔记本电脑上，您不使用本地版本的 `sendmail` 来发送邮件。相反，您使用 SMTP 连接到 ISP 或公司的 SMTP 服务器，该服务器会中继 outgoing mail。为了避免为任何人（包括发送垃圾邮件的恶意用户）中继电子邮件，SMTP 服务器会根据 IP 地址限制为其中继电子邮件的对象。通过实施认证中继，您可以让 SMTP 服务器基于用户身份进行认证。此外，当您从邮件客户端发送邮件并使用 SMTP 服务器时，SMTP 还可以加密通信。

与纯连接相比，认证中继提供以下优势：

- 您可以从任何互联网连接发送邮件。
- 安全连接使得拦截在 Internet 上传输的电子邮件变得更加困难。
- 出站邮件服务器需要身份验证，防止其被用于发送垃圾邮件。

通过创建 SSL 证书或使用现有证书，在 **sendmail** 中启用 SSL，并告知您的邮件客户端使用 SSL 连接到 SMTP 服务器，您可以设置认证中继。如果您拥有 Verisign 等公司的 SSL 证书，您可以跳过下一节，其中将创建自签名证书。

### 为 **sendmail** 创建自签名证书

**Fedora** SSL 证书的默认位置是 `/etc/pki/tls/certs`（PKI 代表 public key infrastructure，公钥基础设施）。作为 **root** 用户，如有必要，使用 **mkdir** 创建此目录，然后使用该目录中的 **Makefile** 生成所需的证书。Apache 使用类似的流程来创建证书（第 878 页）。

```
# cd /etc/pki/tls/certs
# make sendmail.pem
```
Generating a 2048 bit RSA private key
...........+++
................................................................................................................
..............+++
writing new private key to '/tmp/openssl.1TUeh3'

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value.
If you enter '', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:California
Locality Name (eg, city) [Default City]:San Francisco
Organization Name (eg, company) [Default Company Ltd]:Sobell Associates Inc.
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:sobell.com
Email Address []:mgs@sobell.com
-----

您可以将任何信息输入到证书中。

### 在 **sendmail** 中启用 SSL

一旦您有了证书，通过取消 **sendmail.mc** 中以下行的注释，指示 **sendmail** 使用它：

```
TRUST_AUTH_MECH( ' EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN' )
define( ‘confAUTH_MECHANISMS’, ' EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN' )
```

这些行指定了认证机制。

接下来，取消 `sendmail.mc` 中以下行的注释，以告知 `sendmail` 证书的位置：

```
dnl define(`confCACERT_PATH', `/etc/pki/tls/certs')dnl
dnl define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')dnl
dnl define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')dnl
dnl define(`confSERVER_KEY', `/etc/pki/tls/certs/sendmail.pem')dnl
```

加密连接通过两种方式之一建立：SSL（较简单）或 TLS。SSL 需要一个专用端口，并且客户端和服务器协商一个安全连接，然后像连接未加密一样继续事务。TLS 让客户端使用不安全连接连接到服务器，然后发出 `STARTTLS` 命令来协商安全连接。TLS 运行在与未加密连接相同的端口上。由于许多客户端仅支持 SSL，因此指示 `sendmail` 监听 `SMTPS` 端口是个好主意。您在 `sendmail.mc` 中必须取消注释的最后一行指示 `sendmail` 监听 SSL 端口：

```
DAEMON_OPTIONS(` Port=smtps, Name=TLSMTA, M=s')
```

### 在邮件客户端中启用 SSL

在邮件客户端中启用 SSL 通常非常简单。例如，KMail 提供 `Settings → Configure KMail → Accounts → Receiving → Add/Modify → Extras`，允许您选择要使用的加密类型：无、SSL 或 TLS。

## **sendmail** 的替代方案

多年来，`sendmail` 变得极其复杂。如果您想要设置比简单邮件服务器更复杂的内容，其复杂性使其难以配置。其规模和复杂性也增加了其易受攻击性。为了获得最佳安全性，请确保运行最新版本的 `sendmail` 并始终保持 `sendmail` 是最新的。您可以考虑使用以下替代方案之一。

- **Postfix**（**postfix** 包）是一种替代 MTA（邮件传输代理）。Postfix 试图既快又易于管理，同时足够兼容 `sendmail`，以便不会让 `sendmail` 用户感到不安。Postfix 以易用性和安全性著称，是 `sendmail` 的直接替代方案。Postfix 的文档可以在 www.postfix.org/docs.html 找到。
- **Qmail** 是 Postfix 的直接竞争对手，具有相同的目标。默认情况下，Qmail 使用 **maildir** 格式存储电子邮件，而其他 MTA 使用的 **mbox** 格式不同（第 674 页）。Qmail 的网站是 www.qmail.org。

## 章节摘要

`sendmail` 守护进程是一种 MTA（邮件传输代理）。当您发送消息时，`sendmail` 与其他软件协同工作以将其发送到正确的收件人。您可以设置 `sendmail` 将电子邮件中继到将其发送到最终目的地的 SMTP 服务器，或者您可以让 `sendmail` 直接将电子邮件发送到接收电子邮件的域的 SMTP 服务器。默认情况下，`sendmail` 将传入消息存储在邮件 spool 目录 `/var/spool/mail` 中。

控制 `sendmail` 工作原理许多方面的文件是 `sendmail.cf`。如果您编辑 `sendmail.mc`，当重启 `sendmail` 时，`sendmail` 初始化脚本将生成 `sendmail.cf`。系统管理员可以使用 `/etc/aliases` 文件，普通用户可以使用 `~/.forward` 文件将电子邮件重新路由到一个或多个本地或远程地址、文件或作为程序的输入。

您可以使用诸如 SpamAssassin 之类的程序对电子邮件的垃圾邮件可能性进行评分和标记。然后您可以决定如何处理标记的电子邮件：您可以查看每封潜在的垃圾邮件并决定将其放在哪里，或者您可以让 MUA（邮件用户代理）自动将潜在的垃圾邮件放入垃圾邮件的特殊邮箱中。

其他有助于电子邮件处理的程序包括提供 Webmail 服务的 SquirrelMail 和提供邮件列表支持的 Mailman。

## 练习

- 默认情况下，发送给 **system** 的电子邮件会发送给 **root**。您如何同时保存一份副本到 `/var/log/sysemail`？
- Max 如何将他的电子邮件副本存储在 `~/mbox` 中，并发送一份副本到 `max@bravo.com`？
- 如果您的防火墙仅允许 IP 地址为 `192.168.1.1` 的机器将电子邮件发送到网络外部，您将如何指示您的本地 `sendmail` 副本使用此服务器作为中继？
- 在 m4 宏语言中，`dnl` 代表什么？`dnl` 命令用于什么目的？
- 垃圾邮件过滤器 SpamAssassin 已安装在您的邮件服务器上，阈值设置为异常低值 3，导致大量误报。您可以给您的邮件客户端提供什么规则，以便其识别得分高于或等于 5 的垃圾邮件？
- 描述当 Max 向远程 Linux 系统上的 Sam 发送电子邮件时使用的软件和协议。

