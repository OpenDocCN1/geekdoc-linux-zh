
`control.cancel` Cancel messages (no posting).

`control.checkgroups` Hierarchy check control messages (no posting).

`control.newgroup` Newsgroup creation control messages (no posting).

`control.rmgroup` Newsgroup removal control messages (no posting).

`junk` Unfiled articles (no posting).

向此文件为每个本地新闻组添加一行——输入其名称，后跟简要描述。例如，你可以为 `xyz.general` 新闻组添加以下内容：

```
xyz.general   General items about XYZ Corporation
```

2. 编辑 `/etc/news/newsfeeds` 文件中的 `ME` 条目，并在新闻组模式的逗号分隔列表中添加短语 `!xyz.*`。

这可确保你的本地新闻组不会在站点外分发。

3. 添加将用于本地新闻组的存储方法。

例如，你可以在 `/etc/news/storage.conf` 中添加以下行来定义新的 `xyz` 新闻组层次结构的存储方法（将 `xyz` 更改为你为本地新闻组命名的名称）：

```
method tradspool {

    class: 1

    newsgroups: xyz.*
}
```

4. 要使这些更改生效，请使用以下命令重新启动新闻服务器：

```
service inn restart
```

## Adding the newsgroups

最后一步是添加新闻组。在配置文件更新并 `inn` 正在运行后，添加本地新闻组非常容易。以 `root` 身份登录并使用 `ctlinnd` 执行此任务。例如，以下是如何添加名为 `xyz.general` 的新闻组：

```
/usr/lib/news/bin/ctlinnd newgroup xyz.general
```

就这样！该命令将 `xyz.general` 新闻组添加到你的站点。如果你使用传统存储方法，`inn` 服务器会创建目录 `/var/spool/news/articles/xyz/general` 并将该新闻组的文章存储在该目录中（这发生在有人首次向该新闻组发布新闻文章时）。

在创建所有本地新闻组后，你的内联网用户应该能够发布新闻文章并在本地新闻组中阅读文章。如果他们访问新闻组时遇到问题，请确保 `/etc/news/readers.conf` 文件包含应能够访问 `inn` 服务器的主机的 IP 地址或名称。

## Testing your newsgroups

例如，我使用上一节中解释的说明，在我的 Red Hat Linux 系统上运行的 INN 服务器上添加了一个名为 `local.news` 的新闻组。然后我在局域网上的另一台 Red Hat Linux 系统上启动 Mozilla，并设置一个新的新闻帐户，将新闻服务器设置为我的 INN 服务器。接下来，我通过输入 `news:local.news` 作为 URL 来访问 `local.news` 新闻组。试试看！我敢打赌你会喜欢的。

### 第5章：设置 DNS 和 NIS

### 本章内容
- ✔ 了解 DNS
- ✔ 了解 BIND
- ✔ 配置 DNS
- ✔ 设置缓存名称服务器
- ✔ 配置主名称服务器
- ✔ 了解 NIS
- ✔ 配置 NIS 服务器和客户端
- ✔ 尝试使用 NIS

域名系统（DNS）是一种 Internet 服务，它将完全限定域名（如 `www.redhat.com`）转换为对应的 IP 地址（如 `216.148.218.195`）。你可以将 DNS 视为 Internet 主机的目录——正是因为 DNS，你可以使用易于记忆的主机名，即使 TCP/IP 在数据传输中需要数字 IP 地址。DNS 基本上是一个分布式的 DNS 服务器层级结构。在本章中，我将概述 DNS，并向您展示如何在 Red Hat Linux 系统上设置缓存 DNS 服务器。

网络信息系统（NIS）是另一项客户端/服务器服务，旨在管理网络上多个主机计算机之间共享的信息。通常，NIS 在局域网（LAN）上的一组主机为 UNIX 或 Linux 系统维护一组公共的用户账户和其他系统文件。此服务等使用户能够使用相同的用户名和密码登录所有主机。本章简要介绍了 NIS 客户端和服务器软件，并向您展示如何在 Red Hat Linux 系统上使用它们。

### 了解域名系统（DNS）

在 TCP/IP 网络中，每个网络接口（例如以太网卡或拨号调制解调器连接）都由一个 IP 地址标识。由于 IP 地址难以记忆，因此会为 IP 地址分配一个易于记忆的名称——就像电话号码与姓名相对应一样。例如，您无需记住 Red Hat Web 服务器的 IP 地址为 `216.148.218.195`，只需通过其名称 `www.redhat.com` 来引用该主机即可。当您在 Web 浏览器中输入 `www.redhat.com` 作为 URL 时，该名称必须被翻译成对应的 IP 地址。这就是 DNS 概念发挥作用的地方。

### 什么是 DNS？

域名系统是一个分布式、分层的数据库，用于保存有关 Internet 上计算机的信息。这些信息包括主机名、IP地址和邮件路由规范。由于这些信息存储在 Internet 上的许多 DNS 主机中，因此 DNS 被称为分布式数据库。DNS 的主要任务是将主机名与 IP 地址关联起来，反之亦然。

在 ARPANET——当今 Internet 的前身——主机名及其对应 IP 地址的列表保存在名为 `HOSTS.TXT` 的文本文件中，该文件由中央管理并定期分发给网络上的每台主机。随着主机数量的增长，维护这张静态主机表很快变得不合理。Paul Mockapetris 提出了 DNS 以缓解静态主机表的问题。正如在请求评论（RFC）882 和 883 中正式记录的那样（1983 年 11 月发布，参见 `www.faqs.org/rfcs/rfc882.html` 和 `www.faqs.org/rfcs/rfc883.html`），原始 DNS 引入了两个关键概念：
- 使用分层域名，例如 `www.ee.umd.edu` 和 `www.redhat.com`
- 通过在整个 Internet 上使用 DNS 服务器来分担管理主机数据库的责任

我们今天所知的 DNS 是一项在 RFC 1034 和 1035 中记录的 Internet 标准。该标准已被其他多个 RFC 更新和扩展——1101、1183、1348、1876、1982、1996、2065、2181、2136、2137、2308、2535、2845 和 2931。较早的更新定义了数据编码，而较新的更新则侧重于改进 DNS 安全。要在线阅读这些和其他 RFC，请访问俄亥俄州立大学的 Internet RFC 页面，网址为：

```
www.cis.ohio-state.edu/hypertext/information/rfc.html
```
