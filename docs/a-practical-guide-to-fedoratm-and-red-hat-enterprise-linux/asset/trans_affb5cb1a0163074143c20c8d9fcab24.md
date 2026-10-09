

## 先决条件

安装 dovecot 包。rpm 安装脚本会在名为 `/etc/pki/dovecot/certs/dovecot.pem` 和 `/etc/pki/dovecot/private/dovecot.pem` 的文件中创建 dovecot 所需的自签名证书。通常，你无需修改 dovecot 配置文件（`/etc/dovecot/dovecot.conf`）。

## 启用并启动 dovecot

运行 systemctl 使 dovecot 在系统进入多用户模式时启动，然后启动 dovecot。使用 systemctl status 命令以确保服务正在运行。

```bash
# systemctl enable dovecot.service
# systemctl start dovecot.service
```

在修改 dovecot 配置文件后，给出相同的命令，将 `start` 替换为 `restart`，以让 dovecot 重新读取其配置文件。

## 身份验证中继

如果你使用笔记本电脑等便携式计算机出行，你可能会在每个工作地点通过不同的连接接入互联网。也许你因工作出差，或者只是每晚将笔记本电脑带回家。

如果你始终通过 ISP 拨号接入网络，则本节不适用。在这种情况下，你始终连接到你的 ISP 网络，就好像你从未移动过你的计算机一样。

在笔记本电脑上，你不使用本地的 sendmail 实例来发送电子邮件。相反，你使用 SMTP 连接到 ISP 或公司的 SMTP 服务器（smarthost），然后由该服务器中转你发出的邮件。为避免为任何人（包括会发送垃圾邮件的恶意用户）中转电子邮件，SMTP 服务器会根据 IP 地址限制其为谁中转电子邮件。通过实现身份验证中继，你可以让 SMTP 服务器基于用户身份进行身份验证。此外，当你从电子邮件客户端发送邮件并使用 SMTP 服务器时，SMTP 可以加密通信。

身份验证中继相比普通连接提供了几个优势：

- 你可以从任何互联网连接发送电子邮件。
- 安全连接使得电子邮件在穿越互联网时更难被截获。
- 出站邮件服务器要求身份验证，防止其被用于发送垃圾邮件。

你可以通过创建 SSL 证书或使用现有证书，在 sendmail 中启用 SSL，并告诉你的电子邮件客户端使用 SSL 连接到 SMTP 服务器来设置身份验证中继。如果你拥有来自 VeriSign 等公司的 SSL 证书，你可以跳过下一节中创建自签名证书的内容。

## 为 sendmail 创建自签名证书

SSL 证书的默认位置是 **/etc/pki/tls/certs**（PKI 代表公钥基础设施）。使用 *root* 权限，在此目录中执行命令 `make sendmail.pem` 以生成所需的证书。Apache 创建证书时使用类似的步骤（第 970 页）。

```bash
# cd /etc/pki/tls/certs
# make sendmail.pem
... 
Generating a 2048 bit RSA private key
................................................................++++++
writing new private key to '/tmp/openssl.snxDr0'

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:US
State or Province Name (full name) []:California
Locality Name (eg, city) [Default City]:San Francisco
Organization Name (eg, company) [Default Company Ltd]:Sobell Associates Inc.
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:sobell.com
Email Address []:mgs@sobell.com
..............................+++++++++
```

你可以在证书中输入任何你想要的信息。

## 在 SENDMAIL 中启用 SSL

一旦你拥有证书，请通过取消注释（移除开头的 `d1`）**sendmail.mc** 中的以下行来指示 **sendmail** 使用该证书：

```
TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')d1
```

这些行指定了身份验证机制。

接下来，取消注释 **sendmail.mc** 中的以下行，以告知 **sendmail** 证书的位置：

```
define('confCACERT_PATH', '/etc/pki/tls/certs')d1
define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')d1
define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')d1
define(`confSERVER_KEY', `/etc/pki/tls/certs/sendmail.pem')d1
```

加密连接通过两种方式之一建立：SSL（更简单）或 TLS。SSL 需要专用端口，客户端和服务器协商安全连接，并继续交易，就好像连接未被加密一样。TLS 让客户端使用不安全连接到服务器，然后发出 STARTTLS 命令以协商安全连接。TLS 运行在与未加密连接相同的端口上。由于许多客户端仅支持 SSL，因此指示 **sendmail** 监听 SMTPS 端口是个好主意。你在 **sendmail.mc** 中必须取消注释的最后一行指示 **sendmail** 监听 SMTPS（SMTP 安全）端口：

```
DAEMON_OPTIONS(`Port=smtps, Name=TLSMTA, M=$\')dn1
```

### 在邮件客户端中启用 SSL

在邮件客户端中启用 SSL 通常非常简单。例如，Evolution 提供了 *编辑***偏好设置**电子邮件账户**编辑**接收邮件**安全**加密方法* 组合框，允许你选择想要使用的加密类型：无加密、STARTTLS 加密或专用端口上的 SSL。在 *发送邮件* 选项卡下也有一个类似的组合框。或者，你可以在设置 Evolution 时指定想要使用的加密类型。

## 章节摘要

**sendmail** 守护进程是一个 MTA（邮件传输代理）。当你发送消息时，**sendmail** 与其他软件协作将电子邮件送达适当的收件人。你可以设置 **sendmail** 将电子邮件发送到 SMTP 服务器，然后由该服务器将电子邮件中转至其目的地；或者你可以让 **sendmail** 直接将电子邮件发送到接收该电子邮件的域的 SMTP 服务器。默认情况下，**sendmail** 将传入消息存储在邮件 spool 目录 */var/spool/mail* 中。

**sendmail.cf** 文件控制 **sendmail** 工作的许多方面。如果你编辑此文件，请重启 **sendmail** 服务以重新生成 **sendmail.cf**。系统管理员可以使用 */etc/aliases* 文件，而普通用户可以使用 *~/.forward* 文件将电子邮件重定向到一个或多个本地或远程地址、文件，或作为程序的输入。

你可以使用诸如 SpamAssassin 等程序来评估并标记电子邮件被认定为垃圾邮件的可能性。然后你可以决定如何处理被标记的电子邮件：你可以查看每封潜在的垃圾邮件并决定将其放置在哪里，或者你可以让你的 MUA 自动将潜在的垃圾邮件放入用于垃圾邮件的特殊邮箱中。

其他有助于电子邮件处理的程序包括 *SquirrelMail*，它提供 Webmail 服务；以及 *Mailman*，它提供邮件列表支持。*IMAP*（Internet 消息访问协议）和 *POP*（邮局协议）允许用户远程检索和操作电子邮件。*Dovecot* 系统提供 IMAP 和 POP 服务器。

## 练习

- 1. 默认情况下，发送给 *system* 的电子邮件会发送到 *root*。你如何也在 */var/logs/systemmail* 中保存一份副本？
- 2. Max 如何在其 ~/mbox 中存储电子邮件的副本，并向 max@example.com 发送一份副本？
- 3. 如果你的防火墙仅允许 IP 地址为 192.168.1.1 的机器向网络外部发送电子邮件，你如何指示本地的 sendmail 副本使用此服务器作为中继？
- 4. 在 m4 宏语言中 dnl 代表什么？dnl 命令有什么用途？
- 5. 你的邮件服务器上安装了 SpamAssassin，阈值设置为异常低的值 3，导致大量误报。你可以给邮件客户端什么规则，让它能够识别得分 5 或更高的垃圾邮件？
- 6. 描述 Max 向远程 Linux 系统上的 Sam 发送电子邮件时使用的软件和协议。

### 高级练习

- 7. 你公司当前的邮件服务器运行在商业 UNIX 服务器上，你正计划将其迁移到 Linux。将配置文件复制到 Linux 系统后，你发现它无法正常工作。你可能忘记了更改什么？
- 8. 假设一个脚本将某些信息存储在名为 RESULT 的变量中。你可以在脚本中放入什么行，将 RESULT 的内容发送到命令行中第一个参数指定的电子邮件地址？
- 9. 给出一种不使用 MUA 即可阅读电子邮件的简单方法。
- 10. 如果你不小心删除了 /etc/aliases 文件，假设你没有重启 sendmail，如何轻松重新创建它？

