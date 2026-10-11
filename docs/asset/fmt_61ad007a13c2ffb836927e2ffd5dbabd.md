
一种更简单的方法来确保在做出任何更改后重建所有必要内容——只需以 `root` 身份登录并键入以下命令：

```
cd /etc/mail
make
```

第一条命令将当前目录更改为 `/etc/mail`，第二条命令运行 `make` 命令，该命令读取 `/etc/mail` 中名为 `Makefile` 的文件以执行重建所有内容的必要步骤。（要了解有关 `make` 和 `Makefile` 的更多信息，请参见卷八，第一章。）

### `.forward` 文件

用户可以通过在其主目录中放置 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，包含逗号分隔的邮件地址列表。任何发送给该用户的邮件都会转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有电子邮件都会重定向到该单一电子邮件地址。例如，假设在一个名为 `emily` 的用户的主目录中放置了一个包含以下行的 `.forward` 文件：

```
ashley
```

此行导致 `sendmail` 自动将所有发送给 `emily` 的电子邮件发送到同一系统上的用户名 `ashley`。用户 `emily` 完全不会收到邮件。

还可以通过列出完整的电子邮件地址将邮件转发到另一系统上的用户名。例如，我添加了一个 `.forward` 文件，其中包含以下行，以将我的消息（发给我的用户名 `naba`）转发到邮件地址 `naba@comcast.net`：

```
naba@comcast.net
```

现在假设我想在原始系统上保留一份消息副本，同时转发到地址 `naba@comcast.net`。我可以通过在 `.forward` 文件中添加以下行来实现：

```
naba@comcast.net, naba\
```

我只需追加我的用户名并在行尾添加反斜杠。行末的反斜杠（`\`）阻止 `sendmail` 反复转发消息（因为当副本发送到系统上我的用户名时，`sendmail` 通常会再次处理我的 `.forward` 文件）。反斜杠告诉 `sendmail` 不要反复转发消息。

### `sendmail` 别名文件

除了 `sendmail.cf` 文件外，`sendmail` 还会参考名为 `/etc/aliases` 的别名文件，将名称转换为地址。别名文件的位置出现在 `sendmail` 配置文件中。

每个*别名*通常是电子邮件地址的较短名称。系统管理员使用 `sendmail` 文件转发*邮件*，创建邮件列表（标识多个用户的单一别名），或通过多个不同名称引用用户。例如，以下是一些典型的别名：

- `barkakati`: `naba`
- `naba`: `naba@lnbsoft`
- `all`: `naba, leha, ivy, emily, ashley`

第一行表示发送给 `barkakati` 的邮件将交付给本地系统上名为 `naba` 的用户。第二行表明发送给 `naba` 的邮件实际上发送到了 `lnbsoft` 系统上的用户名 `naba`。最后一行将 `all` 定义为五个用户 `naba`、`leha`、`ivy`、`emily` 和 `ashley` 的别名。这意味着发送给 `all` 的邮件将发送到这五个用户。

在 `/etc/aliases` 文件中定义任何新别名后，必须以 `root` 身份登录，并通过键入以下命令使新别名生效：

```
sendmail -bi
```

## 安装 INN 服务器

在本节中，我描述了如何配置基于 TCP/IP 的新闻服务器 InterNetNews（INN）。首先，您必须安装 INN。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l inn*` 以查看是否安装了 `inn`。在 Fedora Core 和 SUSE 中，键入 `rpm -q inn` 并查看是否安装了 `inn` 包。

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install inn` 以安装 INN 服务器。在 Fedora Core 中，以 `root` 身份登录，挂载 DVD，并键入 `cd /media/cdrom/Fedora/RPMS` 后跟 `rpm -vh inn*`。在 SUSE 中，点击 YaST 控制中心软件类别中的“软件管理”。然后使用 YaST 的搜索功能查找 `inn`，从搜索结果中选择相关的包并安装它们。在 Xandros 中，首先运行 Xandros Networks，选择 编辑>设置应用程序源，并点击 Debian Unsuppored Site 链接作为源。然后键入 `apt-get install inn` 以安装 INN 服务器。

# 配置和启动 INN 服务器

INN 软件的大部分功能在安装后即可使用。你只需对 INN 的各个组件进行一点复习，编辑配置文件，并启动 `innd` —— INN 服务器。顺便说一下，我有时也称 INN 服务器为新闻服务器。

如果你想运行一个支持多种 Internet 新闻组的新闻服务器，你还需要安排一个*新闻源（news feed）*——即你的新闻服务器获取新闻组文章的地方。通常，你可以从 ISP（互联网服务提供商）获得新闻源，但 ISP 会收取额外的月度费用，以覆盖提供该源所需的资源成本。（你通常向 ISP 支付的费用仅涵盖阅读其服务器上的新闻；只有当你想要运行自己的服务器并获取新闻源时，才需要支付额外费用。）你需要提供提供新闻源的上游服务器名称，并且必须向该服务器提供你服务器的名称以及你希望接收的新闻组。

顺便说一句，如果你运行新闻服务器是为了支持仅在组织内部网络中可用的本地新闻组，则不需要外部新闻源。我在本章的“设置本地新闻组”部分介绍了如何设置本地新闻组。

根据你希望接收的新闻组以及保留文章的天数，你需要预留适当的磁盘空间来存储这些文章。新闻组按照目录结构（基于新闻组名称）存储在系统目录 `/var/spool/news` 中。如果你正在设置新闻服务器，可能希望将一个大容量的磁盘分区专门用于 `/var/spool/news` 目录。

在新闻服务器的配置文件中，输入提供新闻源的服务器名称。同时，在配置文件中添加任何从你的服务器接收新闻源的下游新闻服务器（如果有）的名称。然后你可以启动新闻服务器并等待新闻到达。监控日志文件，以确保新闻文章在你的系统 `/var/spool/news` 目录中正确分类和存储。

在接下来的部分中，我将向你介绍 INN 的设置，但你可以从互联网系统协会（Internet Systems Consortium, ISC）获取更多关于 INN 的信息。ISC 是一家非营利法人，致力于开发和维护开源 Internet 软件，如 BIND（域名系统实现）、DHCP（动态主机配置协议）和 INN。Rick Salze 最初编写了 INN；ISC 在 1996 年接管了 INN 的开发。你可以在 ISC 的 INN 网页 `www.isc.org/sw/inn` 上了解更多关于 INN 的信息并访问其他资源。

![](img/792720823146d68f19fd50c99ebfce4b_654_0.png)

# InterNetNews 组件

INN 包含几个用于交付和管理新闻组的程序。它还包含一些控制 INN 程序如何工作的文件。最重要的 INN 程序如下：

- **`innd`:** 新闻服务器。它作为*守护进程*（一种保持运行以提供特定服务的后台进程）运行，并监听 NNTP 端口（TCP 端口 119）。`innd` 服务器接受来自其他新闻源站点以及本地新闻阅读器客户端的连接，但它将本地连接交给 `nnrpd` 处理。
- **`nnrpd`:** 由 `innd` 调用的特殊服务器，用于处理来自本地新闻阅读器客户端的请求。
- **`expire`:** 根据文本文件 `/etc/news/expire.ctl` 中的规范删除旧文章。
- **`nttpsnd`:** 调用 `innewsmit` 程序，使用 NNTP 将新闻文章发送到远程站点。配置文件 `/etc/news/nttpsnd.ctl` 控制 `nttpsnd` 程序。
- **`ctlinnnd`:** 允许你交互式地控制 `innd` 服务器。`ctlinnnd` 程序可以向 `innd` 服务器的控制通道发送消息。

INN 的其他关键组件是控制文件。这些文件大多数位于你的 Linux 系统的 `/etc/news` 目录中，尽管少数位于 `/var/lib/news` 目录中。在这两个目录之间，你有超过 30 个 INN 控制文件。一些重要的文件包括以下这些：

- **`/etc/news/inn.conf`:** 指定 `innd` 服务器的配置数据。（要查看此文件的在线帮助，请输入 `man inn.conf`。）
- **`/etc/news/newsfeeds`:** 指定向其他新闻服务器下游提供哪些文章。（该文件很复杂，但你可以通过输入 `man newsfeeds` 获取帮助。）
- **`/etc/news/incoming.conf`:** 列出向此服务器提供新闻源的主机的名称和地址。（要查看此文件的在线帮助，请输入 `man incoming.conf`。）
