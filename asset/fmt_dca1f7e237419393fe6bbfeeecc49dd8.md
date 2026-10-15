
```
C:\Windows\System32\cmd.exe - nslookup
Address: 192.168.1.59

Name: microsoft.akadns.net
> set type=any
microsoft.akadns.net
Name: microsoft.akadns.net
Address: 192.108.91.159

microsoft.akadns.net nameserver = ze.akadns.net
microsoft.akadns.net nameserver = use2.akadns.net
microsoft.akadns.net nameserver = zd.akadns.net
microsoft.akadns.net nameserver = 2c.akadns.net
microsoft.akadns.net primary name server = ns-159.akamai.com
serial = 58
expire = 60 (sec)
retry = 50 (sec)
time = 60 (sec)
default TTL = 60 (sec)
microsoft.akadns.net nameserver = zh.akadns.net
microsoft.akadns.net nameserver = use2.akadns.net
microsoft.akadns.net nameserver = 2c.akadns.net
microsoft.akadns.net nameserver = ns-159.akadns.net
ze.akadns.net address = 127.0.217.11
use2.akadns.net address = 281.12.25.166
zd.akadns.net address = 204.79.197.20
2c.akadns.net address = 204.248.36.131
zh.akadns.net address = 204.79.197.200
microsoft.akadns.net address = 63.208.48.42
use2.akadns.net address = 193.108.91.159
microsoft.akadns.net address = 63.215.170.136
> set type=any
Server: nsi-159.akadns.net
Address: 193.108.91.159
```

图 3-11：终于，有了答案。

Name: www.microsoft.akadns.net

Addresses: 207.46.134.155, 207.46.134.190, 207.46.197.113, 207.46.230.220

207.46.230.217, 207.46.230.218

# 第4章

## 使用 DNS 其他应用

- 本章
- 电子邮件概述
- 配置 MX 记录
- 使用多个 MX 记录
- 配置邮件服务器作为邮件交换器

## 接入电子邮件

每当你向 `user@domain.tld` 发送电子邮件时，都会使用 DNS。因为 DNS 在设计时考虑了电子邮件（以及其他因素），它内置了电子邮件功能。电子邮件使用一种特殊的 DNS 记录，即邮件交换器（MX）记录，来促进电子邮件的交换。首先，我们描述简单邮件传输协议（SMTP）。

## 第 4 章：通过 DNS 促进其他应用程序

负责接收发往该域名的所有电子邮件。邮件交换服务器（mail exchanger）可以负责任意数量域，只要它能够处理相应的负载。你也可以为一个域名设置多个邮件交换服务器，我们将在本章的“使用多个 MX 记录”节中进行解释。

SMTP 过程中的关键是 SMTP 中继服务器将消息发送到正确的邮件交换服务器。当中继服务器从客户端接收消息时，消息会被放置在输出队列中。当处理该消息时，SMTP 中继服务器会忽略用户部分（`user@domain.tld`），仅查看域名部分。域名部分用于确定该域名的对应邮件交换服务器。SMTP 中继服务器会对该域名进行 DNS 查找，但不会查找 A 记录。相反，服务器会查找该域名的邮件交换器（MX）记录。我们在第 9 章中提到 MX 记录。

## 理解 MX 记录

MX（或邮件交换器）是 DNS 记录的一种简单形式。每个域名——例如 `microsoft.com`——如果将用于接收电子邮件，则至少有一个 MX 记录。MX 记录包含一个名称（通常是域名名或 `@`）、一个度量值（BIND）或优先级值（Microsoft Windows）（尽管当只有一个 MX 记录时，优先级是一个任意值），以及一个值（邮件交换服务器的 IP 地址）。要在 Windows DNS 中创建 MX 记录，首先点击“开始”按钮并选择“管理工具”来打开 DNS 插程序。

我们将在第 9 章中详细描述这一过程。然而，我们并没有提供如何配置服务器的逐步操作说明，而是提到这一过程是为了让你对 DNS 如何促进邮件传输有一个直观的。关于向你的 DNS 服务器添加记录和区域的详细信息，请参阅第 9 章。

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_74_0.png)

找到要创建记录的区域，右键点击并选择“新建邮件交换器”（New Mail Exchanger）。将显示“新建资源”（New Resource）对话框，如图 4-2 所示。

MX 记录需要几个值。第一个是域名的名称值。要使用当前域名，请留空此框。例如，此 MX 记录是在 `sample.tld` 域中创建的。如果你留空此框，MX 记录将与 `sample.tld` 关联，发往 `user@sample.tld` 的邮件将发送到你指定的主机。如果你想为 `user@host.sample.tld` 投递邮件，也可以为 MX 记录指定其他主机或域名。大多数情况下，你只需为默认域创建 MX 记录即可。

## 第一部分：DNS 如何让互联网运转

![](img/ef3dfe2cb04fcef67ad22a0599c29f36_75_0.png)

图 4-2：

在 Windows 中创建 MX 记录。

你现在必须在“邮件服务器”（Mail server）框中指定邮件交换主机，该可以是 IP 地址，也可以配置为接收该域邮件的邮件服务器的 DNS 主机名。（在后续节“将邮件服务器配置为邮件交换器”中，我们将告诉你如何将邮件服务器配置为邮件交换器。）另一个重要值是优先级。该值默认设置为 10。如果你只有一个 MX 记录，可以保持默认值。在接下来的节中将交替使用多个 MX 记录。对话框中的最后两个值是标记为“当记录变为状态时删除”（Delete this record when it becomes state）的复选框（只有在进行清理时才勾选，这不太可能）以及 TTL 值。TTL 值默认从父区域继承。点击确定创建记录。图 4-3 显示了区域中的新 MX 记录。

在 BIND 中，创建 MX 记录非常简单。你只需要在 MX 记录所在的区域文件中添加一条记录即可。MX 记录的值与 Windows 版本相同：名称、优先级以及邮件交换服务器的名称和地址。BIND 中的 MX 记录看起来如下所示：

```
sample.tld. IN MX 10 mail.sample.tld.
```

假设此 MX 记录在 `sample.tld` 区域文件中，你可以用更简洁的方式实现相同的操作：

```
@ IN MX 10 mail
```

`@` 符号表示当前源，通常是区域的名称（`sample.tld.`），除非使用 `$ORIGIN` 语句进行了更改；不带末尾句号的 `mail` 表示应该附加父域名。这两种方法在功能上是等价的。

## 第 4 章：通过 DNS 促进其他应用程序

| 名称 | 类型 | 数据 |
| --- | --- | --- |
| （与父文件夹相同） | SOA | [6] dns1., admin. |
| （与父文件夹相同） | NS | dns1. |
| | A | 192.168.100.32 |
| （与父文件夹相同） | MX | [10] mail.sample.tld |

图 4-3：MX 记录已在区域中。

## 使用多个 MX 记录

你可以为句域名设置多个 MX 交换器。你希望拥有多个 MX 交换器有两个原因：在多个邮件服务器之间平衡高负载的入邮件，以及在其中一个邮件服务器“故障”时提供备份邮件服务器。每个使用 MX 记录的场景实现方式略有不同。

使用 MX 记录的实现细节略有不同。（等一下，文本重复了，我们继续逻辑。）

使用 MX 记录的实现细节略有不同。

## qmail

`qmail` 是一种基于 Unix/Linux 的邮件传输代理（MTA），可以配置为接收任何你想要的邮件。该域名必须列在 `/var/qmail/control/phosts` 文件中，该文件格式为 `domain.tld`。

# 第4 章：通过 DNS 促进其他应用程序
