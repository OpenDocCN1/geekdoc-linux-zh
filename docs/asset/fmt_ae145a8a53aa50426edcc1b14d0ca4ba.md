
这里 `www.nitec.com` 是代理。`nitec.com` 是反向代理。`ProxyPass` 指令启用此功能。注意 `nitec.com` 发送 Location 头，`ProxyReverse` 指令会修复它。

### ProxyBlock partial or full name

此指令允许你阻止某些命名主机或域名，例如：

`ProxyBlock gates`

这将阻止访问包含 "gates" 单词的主机。你也可以指定多个主机：

`ProxyBlock apple.com banana.com`

这将阻止访问任何主机：

`ProxyBlock *`

这实际上禁用了代理服务器。

### NoProxy domain name | Subnet | IP Address | Hostname

此指令在内部环境中对 `ProxyRemote` 指令提供某些控制。你可以指定不由代理服务器提供服务的域名、子网、IP 地址或主机名。例如：

`ProxyRemote * http://firewall.yourcompany.com:8080`

`NoProxy .yourcompany.com`

这里所有针对 `.yourcompany.com` 的请求（如 `www.yourcompany.com`）将由本地代理服务器提供，而其他所有将去往 `firewall.yourcompany.com`。

### ProxyDomain Domain

此指令指定代理服务器的默认域名。当此指令在内网设置为本地域名时，任何不包含域名的请求将附加此域名，例如：

`ProxyDomain .nitec.com`

当 `nitec.com` 域名的用户发送如 `http://marketing/us.html` 的请求时，请求将重新生成为如下 URL：

`http://marketing.nitec.com/us.html`

注意你指定的域名必须以点开头。

### ProxyReceiveBufferSize bytes

此指令设置从代理服务器发出的请求的网络缓冲区。它必须大于 512。然而，若要使用系统默认缓冲区，请将此指令设置为 0。

### CacheRoot directory

此指令允许你启用磁盘缓存。你可以指定代理服务器可以写入缓存文件的目录名称。运行代理模块的 Apache 服务器必须对该目录具有写入权限，例如：

`CacheRoot /www/proxy/cache`

这将告诉 Apache 将代理缓存数据写入 `/www/proxy/cache` 目录。注意在代理服务器开始使用该目录缓存之前，你需要使用 `CacheSize` 指定缓存的大小。你可能还需要使用其他缓存指令如 `CacheSize`、`CacheMaxSize`、`CacheDefaultExpire`、`CacheGcInterval` 和 `CacheDirLength` 来创建一个可用的磁盘代理方案。

`CacheSize n kilobytes`

# 第 12 章：Web 服务

此指令指定了用于磁盘缓存的磁盘空间（单位为 K）。缓存文件被写入由 `CacheRoot` 指令指定的目录。请注意，代理服务器写入的数据可能会超过指定的限制，但代理服务器的垃圾回收机制将删除文件，直到使用量降至或低于此设置。默认设置（5K）是不现实的；我建议根据您的用户负载，设置在 10MB 到 1GB 之间的范围内。

### CacheInterval n 小时

此指令指定了 Apache 检查缓存目录中过期文件的时间（单位为小时）。这也是 Apache 强制执行由 `CacheSize` 指令指定的磁盘空间使用限制的时间。

### CacheMaxExpire n 小时

此指令指定了所有缓存文档过期的时间（单位为小时）。换句话说，如果你这样指定此指令：

`CacheMaxExpire 48`

那么所有缓存文档将在 48 小时（即两天）后过期。此指令会覆盖文档本身指定的任何过期日期；因此，如果文档的过期日期晚于此指令指定的最大日期，该文档仍然会被移除。默认值为 24。

### CacheLastModifiedFactor 浮点数

当原始 Web 服务器未为文档提供过期日期时，此指令指定一个因子（默认 0.1）来计算过期时间。计算使用以下公式：

```
expiry-period = (文档的最后修改时间) * (浮点数)
```

如果一个文档最后修改于 24 小时前，那么默认因子 0.1 将使 Apache 计算该文档的过期时间为 2.4 小时。如果计算出的过期周期比 `CacheMaxExpire` 设置的长，则以后者为。

### CacheDirLength 长度

启用磁盘缓存时，Apache 在 `CacheRoot` 指令指定的目录中创建子目录。此指令指定用于创建子目录名称的字符数（默认为 1）。你真的不需要更改此指令的默认值。

# 第四部分：设置内网/互联网服务

### CacheDirLevels 层级

这指定了 Apache 为存储缓存数据文件将创建的子目录数量。默认值为 3。相关信息见 `CacheDirLength`。

### CacheDefaultExpire n 小时

此指令提供了一个默认时间（单位为小时），当文件的最后修改时间未知时，用于使缓存文件过期。默认值为 1。`CacheMaxExpire` 不会覆盖此设置。

### CacheForceCompletion 百分比

此指令告诉代理服务器即使请求被取消，也继续从远程 HTTP/FTP 服务器传输文档。指定的百分比使代理服务器决定是否继续传输。默认值为 90%，这意味着当文档已缓存了 90% 时，告诉代理服务器继续传输。你可以将值从 1 到 100 之间更改。

### NoCache 域名| 子网 | IP 地址 | 主机名 . . .

`NoCache` 指令指定了一个主机、域名和 IP 地址列表（用空格分隔），对这些对象不进行缓存。此指令应用于禁用内网本地 Web 服务器的缓存。注意，代理服务器还会匹配主机的部分名称。如果你想禁用其他缓存，请使用：

`NoCache *`

要启用代理服务器，你需要将 `ProxyRequests` 设置为 `On`。之后，额外的配置取决于你想对代理服务器做什么。无论你决定做什么，你选择的任何代理配置都应该放在一个特殊的 `<Directory ...>` 容器内，如下所示：

```
<Directory proxy:*>
</Directory>
```

任何你想要用来控制代理服务器行为的指令都应该放在这个容器内。星号是请求 URL 通配符。换句话说，当 Apache 服务器处理对 www.nitec.com 的请求时，它看起来像：

```
<Directory proxy:http://www.nitec.com/>
</Directory>
```

你也可以使用 `<Directory ~ /RE/>` 容器，它使用正则表达式，例如：

```
<Directory ~ proxy:http://[^/]+/.*>
```

现在让我们来看一些常用的代理配置。

# 缓存远程 Web 站点

由于互联网和内网上的大量 Web 内容很可能是静态的，在本地代理服务器上缓存它们可以节省宝贵的网络带宽。启用了缓存的代理服务器仅在缓存中包含过期文档或缓存中不存在请求文档时，才会获取请求的文档。要在你的代理服务器上启用缓存，你需要在特殊的目录容器内指定缓存目录，例如：

```
<Directory proxy:*>
CacheRoot /www/cache
CacheSize 1024
CacheMaxExpire 24
</Directory>
```

此配置定义了一个代理服务器，它为 `/www/cache` 目录写入缓存文件。允许写入 1,024K 数据（1MB），且缓存必须在每天（24 小时）后过期。

如果你不想允许外部访问你的代理，可以通过主机或用户名/密码认证进行限制。为了控制哪些主机可以访问代理服务器，你可以创建一个如下配置：

```
<Directory proxy:*>
AuthType Basic
AuthName Proxy
order deny,allow
deny all
allow from myhost.nitec.com
</Directory>
```

此配置拒绝了所有 myhost.nitec.com 的访问。如果你想使用用户名/密码认证，可以使用以下：

## 第四部分：设置内网/互联网服务

`allow from host1 host2 host3 . . .`

此指令允许您定义一个主机列表（包含一个或多个主机或 IP 地址），这些主机被允许访问特定目录。当指定了多个主机或 IP 地址时，它们应该用空格字符分隔。表 12-1 显示了该指令的可能取值。

# 表 12-1 ALLOW 指令的可能值

| 值 | 示例 | 描述 |
| --- | --- | --- |
| All | allow from all | 此预留字允许所有主机访问。示例显示了如何使用此选项。 |
