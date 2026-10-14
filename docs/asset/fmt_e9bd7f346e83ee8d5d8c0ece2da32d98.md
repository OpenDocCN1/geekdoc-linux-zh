
`acl blocked url_regex -i example.com`

现在，该 `acl` 匹配包含 `example.com` 的所有 URL，无论是大写还是小写。

在大多数情况下，你想拦截的不仅仅是单个 URL。与其为每个 URL 创建一个 `acl`，你也可以将所有 URL 模式列在一个文件中，并将文件路径作为 `acl` 语句中的参数。

以下 `acl` 从 `/etc/squid/black_list` 文件读取模式：

```
acl blocked url_regex -i "/etc/squid/black_list"
```

文件名和路径只是示例，可以更改。

此类带有模式的文件通常被称为黑名单。然而，`url_regex` `acl` 也可以用于允许访问匹配给定模式的 URL，这被称为白名单。

文件的文件的格式非常简单。你只需要在文件中列出模式，每行一个。以下是列出三个模式的示例：

```
example.com

example2.com

example3.com
```

你还可以下载黑名单。通过这种方式，你可以拦截不适当的网站。

# SUSE Linux Enterprise Server 10: 安全

以下是 `squidguard` 中使用的关键字的概述：

- `time`。定义一天中的时间。
- `src`。定义请求的源。
- `dest`。定义请求的目标。

然而，由于这些条件可以由 Squid 充分处理，我们将重点关注 URL 匹配功能。

## 使用 squidGuard 配置 URL 过滤

对于 Squid 来说，这意味着根据网站的 URL 控制对网站的访问。此功能也称为 URL 过滤或拦截。

基本上，你可以配置两种不同类型的 URL 过滤：

- 使用 `url_regex` 配置 URL 过滤
- 使用 `squidGuard` 配置 URL 过滤

首先，定义了路径变量和条件黑名单。`acl` 部分仅包含默认条目。该条目允许（通过）访问不匹配黑名单条件的 URL。

当 URL 匹配黑名单时，将不允许访问，且请求将被重定向到公司内网的一个页面。在这种情况下，使用了默认条目，因为没有没有定义其他可用于匹配请求的源条件。

此示例是一个非常基础的 `squidGuard` 设置。更详细的描述可以从 http://www.squidguard.org/config/ 找到在本地的 `/usr/share/doc/packages/squidGuard/doc/configuration.html` 中找到。你也可以在 `squidGuard` 首页页找到关于预编译黑名单的更多信息（http://www.squidguard.org/）。

![](img/ebd0b66532100449f2a48e48fa2ec8ce_310_0.png)

# 练习 8-4

## 配置 URL 过滤

在本次练习中，你将使用 Squid 配置 URL 过滤。

你将在练习册中找到此练习。

（练习结束）

### 配置拦截代理服务器

到目前为止讨论的所有代理设置都要求客户端（网络浏览器）配置为使用代理服务器。你可以修改代理设置，使其变得不再必要。在这种情况下，该代理也被称为拦截代理或透明 http 代理。

透明代理的工作原理如下：当目标端口为 80 的 TCP 数据包到达路由器时，路由器将数据包重定向到 Squid。Squid 检查请求的对象是否在它的缓存中。如果该对象不在缓存中，Squid 将从互联网获取该对象。

在配置透明代理时，你必须在路由器中设置一条规则，将 HTTP 流量（端口 80）重定向到 Squid，并且你需要修改 Squid 配置。

在 `/etc/squid/squid.conf` 中必须设置以下标签：

```
httpd_accel_host virtual

httpd_accel_port 80

httpd_accel_wlth_proxy on

httpd_accel_uses_host_header on
```

下插图了当 Squid 与互联网网关运行在同一台服务器上时，如何设置透明代理：

图 8-8

![](img/ebd0b66532100449f2a48e48fa2ec8ce_312_0.png)

# SUSE Linux 企业服务器 10: 安全

为了在路由器上设置端口重定向，你可以使用以下 `iptables` 命令（单行）：

```
iptables -t nat -A PREROUTING -p TCP --dport 80 -j REDIRECT --to-port port_of_squid
```

尽管透明代理有很多优点，但它也有一些缺点：

- 透明代理仅对 HTTP 起效。
- 其他协议（如 HTTPS、FTP 和 GOPHER）在透明代理上无法工作，因为网络浏览器需要感知代理服务器才能通过代理使用这些协议。
- 与直接网络连接或在客户端中配置的代理连接相比，该连接可能不那么稳定。

## 分析 Squid 日志文件

用于分析 Squid 日志文件的程序可以提供有关已访问过的、、流量和其他主题的信息。

其中一个是名为 `calamaris` 的 Perl 脚本，它能分析 Squid 的 `/var/log/squid/access.log` 文件。该脚本对请求和请求产生统计分析。分析结果以 ASCII 或 HTML 格式生成。`calamaris` 可用于 SUSE Linux 企业服务器 10。包名为 `calamaris`。

`calamaris` 有许多影响分析内容的选项。以下是最重要的选项：

| 表 8-2 | |
| 选项 | 含义 |
| --- | --- |
| -a | 执行所有可用的分析——对应于最重要的选项的组合。例如，列表不会显示所有已连接的 DNS 域名，仅显示前 20 个。 |

# 仅供中国使用- 不允许纸质副本

严禁复制本手册的全部或部分内容，或分发此类副本。如需报告疑似复制行为，请拨打 1-800-PIRATES。版本 1

| 表 8-2 | 选项 | 含义 |
| --- | --- | --- |
| -d number | 生成前 `number` 个最频繁的顶级和二级域名列表。如果应该列出所有项，请将其设置为 -1。 |
| -r number | 生成向 Squid 请求最频繁的主机列表。仅列出 `number` 个主机。值 -1 显示所有主机。 |
| -P | 显示每分钟的 TCP 请求数。 |
| -w | 输出以 HTML 格式写入。默认是纯文本。 |

以下示例创建了访问最频繁的前 10 个一级和二级域名的列表：

```
calamaris -d 10 /var/log/squid/access.log
```

![](img/ebd0b66532100449f2a48e48fa2ec8ce_314_0.png)

关于 `calamaris` 的更多信息，请参见 http://cord.de/tools/squid/。服务器配置位于文件 `/squid.conf`。

## 练习 8-5

## 分析 Squid日志

在本次练习中，你将使用 Squid 配置 URL 过滤。你将在练习册中找到此练习。

（练习结束）

## 目标 3

## 配置和使用 Dante

`Dante` 是 SOCKS 协议的开源实现。它由两部分组成：

- SOCKS 服务器 (`sockd`)。实现 SOCKS 协议的服务器。
- SOCKS 客户端 (`socksify`)。一组系统库和脚本，帮助不支持 SOCKS 的客户端使用。

这些组件以独立的 RPM 包形式提供。你需要为服务器安装 `dante-server` 包，为客户端安装 `dante` 包。

安装并配置后，通过以下命令启动服务器：

```
rcsockd start
```

更改配置文件后，通过以下命令重启服务器：

```
rcsockd restart
```

要在启动时自动启动服务器，输入：

```
insserv sockd
```

服务器配置位于文件

```
/etc/sockd.conf
```
