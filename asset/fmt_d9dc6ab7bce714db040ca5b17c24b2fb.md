
# MetaDir：指定 Apache 可以在其中找到元数据文件
# 的目录名称。这些文件包含了在发送文档时
# 需要包含的额外 HTTP 头部
# `MetaDir` `.web`

# MetaSuffix：指定包含元数据文件的文件后缀名。
# `MetaSuffix` `.meta`

# 可自定义的错误响应（Apache 样式）
# 这些有三种形式：
#
# 1) 纯文本
# `ErrorDocument` `500` `"服务器出了小差错。"`
# 注意：`("")` 将其标记为文本，它不会被输出
#
# 2) 本地重定向
# `ErrorDocument` `404` `/missing.html`
# 重定向到本地 URL `/missing.html`
# `ErrorDocument` `404` `/cgi-bin/missing_handler.pl`
# 注意：你可以使用服务器端包含（SSI）重定向到脚本或文档。
#
# 3) 外部重定向
# `ErrorDocument` `402` `http://some.other_server.com/subscription_info.html`
# 注意：与请求相关的许多环境变量
# 将“不会”对此类脚本可用。

# 以下指令修改了正常的 HTTP 响应行为。
# 第一条指令禁用 Netscape 2.x 的保持连接（keepalive），
# 浏览器会伪造它。这些浏览器的实现存在已知问题。
# 第二条指令用于 Microsoft Internet Explorer 4.0b2，
# 它具有损坏的 HTTP/1.1 实现，并且在用于 301 或 302（重定向）时
# 无法正确支持 keepalive。

# 列表 11.2 继续

```
#
BrowserMatch "Mozilla/2" nokeepalive
BrowserMatch "MSIE 4\.02"; nokeepalive downgrade-1.0 force-response-1.0
```

# 以下指令禁用对浏览器的 HTTP/1.1 响应，这些浏览器
# 违反了 HTTP/1.0 ，无法理解基础的 1.1 响应。

```
BrowserMatch "RealPlayer 4\.0" force-response-1.0
BrowserMatch "Java/1\.0" force-response-1.0
BrowserMatch "JDK/1\.0" force-response-1.0
```

# 允许服务器状态报告，URL 为 `http://servername/server-status`
# 将 `".your_domain.com"` 修改为匹配你的域名以启用。

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from localhost
</Location>
```

# 允许远程服务器配置报告，URL 为
# `http://servername/`（需要加载 `mod_info.c`）。
# 将 `".your_domain.com"` 修改为匹配你的域名以启用。

```
<Location /server-info>
  # SetHandler server-info
  # Order deny,allow
  # Deny from all
  # Allow from .your_domain.com
</Location>
```

# 有报告称有人试图滥用一个旧的
# 11 天前的漏洞。此漏洞引入了一个作为 Apache 部分分发的 CGI 脚本。
# 通过注释这些行，你可以将这些攻击重定向到
# `apache.org` 上的日志脚本。或者，你可以自己记录它们，使用
# `support/abuse.cgi`。

# Apache 服务器 11

# 列表 11.2 继续

```
#
#<Location /cgi-bin*>
#   Deny from all
#   ErrorDocument 403 http://apache.org/abuse.cgi
#</Location>

# 代理服务器指令。取消以下行以启用
# 代理服务器：
#<IfModule mod_proxy.c>
#   ProxyRequests On
#<Directory proxy*>
#   Order deny,allow
#   Deny from all
#   Allow from .your_domain.com
```

# `Action` 允许你定义媒体类型，每当调用匹配的文件时
# 就会执行脚本。这消除了为经常使用的 CGI 文件处理器
# 重复 URL 路径的需求。
# 格式：`Action` `media/type` `/cgi-script/location`

# Linux 与新闻组 (Newsgroups)

在 Linux 系统上下载新闻组主要有三种方式：`INN`、`C-News` 和 `NNTPCache`。`INN` 实现了 `NNTP`，全称为网络新闻传输协议。`NNTP` 广泛用于通过 TCP/IP 连接到 `ISP`（服务提供商）或互联网。`INN`（互联网新闻）是最灵活且可配置最高的新闻组下载方法，特别对于具有高速互联网连接的大站或传输大量新闻的站点（例如大型教育机构）运行效果极佳。`C News` 是为通过 `UUCP`（UNIX 到 UNIX 拷贝）下载新闻而设计的。`NNTPCache` 可能是大多数站点的最佳选择，特别是那些没有足够带宽下载你组织所需所有新闻的站点。由于 `INN` 是针对大多数 Linux 系统开发的，因此我们首先讨论这一选择；随后将讨论如何使用 `NNTPCache` 作为一种节省资金的替代方案来为用户提供新闻。

`Rich Salz` 开发了 `INN`，目的是为了在一个程序包中提供一个完整的 Usenet 软件包。`INN` 的吸引力之一在于，它并不在乎你是使用 TCP/IP 还是 `UUCP` 来传输新闻组。`INN` 对等地处理这两种方法。`INN` 处理传输新闻的 `NNTP` 协议，并作为一个独立的服务器 `nntpd` 提供新闻阅读服务，它在检测到 TCP/IP 连接时执行。

## 新闻流 (Newsfeed)的工作原理

`Usenet` 新闻组帖子不断通过互联网在机器之间发送。为了从一个系统发送到另一个系统，`Usenet` 使用了一种名为“泛洪”（flooding）的技术。当一台机器连接到另一台机器时，它实际上会将新闻组中的所有帖子作为一个大块进行传输。接收机器连接到另一台机器并重复这一过程。通过这种方式，新闻组中的所有帖子都会跨越整个互联网。这比在互联网某处的服务器上维护单一信息源要好得多。参与泛洪的每台机器都有一个可以发送或接收帖子的机器列表。每个连接被称为一个新闻流。当你连接到 `ISP` 并下载新闻组帖子时，你就在你的机器和 `ISP` 的机器之间了一个新闻流。

每当新闻组添加（或发布）新帖子时，新闻流就会被用于传输该帖子。每篇文章都有一个接收了该帖子的机器列表，因此很容易避免多次将同一条帖子传输到互联网上的每台机器。每个帖子都有一个唯一的邮件 ID，可以防止重复发布。

## 防止重复发布

当你连接到 `ISP` 并请求新闻组更新时，通常使用以下两种方法之一来确保在使用阅读器时不会产生重复发布。最常用的技术被称为 `fetch/sendme`，它会通知新闻流另一端的机器（例如你的 `ISP` 服务器）你已经拥有哪些消息 ID，哪些是缺失的。在那个时候，只有缺失的帖子会被传输到你的 Linux 机器。

`fetch/sendme` 协议对于更新少量新闻组非常出色，但在处理海量新闻时，效率会急剧下降。因此，使用了一种名为“批处理”（batching）的方法来传输大型新闻流。在批处理中，新闻流一端的所有内容都作为一个块传输。你的机器随后对下载内容进行排序并丢弃任何重复项。与 `fetch/sendme` 相比，批处理给你的 Linux 机器增加了开销，但两端之间的消息传递少得多。

## 推送 (Pushing) 与拉取 (Pulling) 新

另外两个术语用于描述将新闻组帖子从一台机器传输到另一台机器，这些术特别适用于每天下载整个新闻流的小型系统。你的系统可以使用 `fetch/sendme` 协议从新闻流下载文章，这种技术被称为“推送”（pushing）。或者，你的机器可以根据到达日期从新闻流请求特定的帖子或整个新闻组，这种技术被称为“拉取”（pulling）。

## 下载新闻组的替代方法
