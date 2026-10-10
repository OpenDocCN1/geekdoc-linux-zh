
## 因此，如果一个文档最后一次修改于 24 小时前

如果一个文档最后一次修改于 24 小时前，那么默认的因子 `0.1` 使 Apache 计算该文档的过期时间为 `2.4` 小时。如果计算的过期期长于 `CacheMaxExpire` 设置的值，则 `CacheMaxExpire` 的过期期优先。

## CacheDirLength

当磁盘缓存开启时，Apache 会在 `CacheRoot` 指令指定的目录下创建子目录。该指令指定了用于创建子目录名称的字符数。你通常不需要更改此指令的默认值。对于想了解这些子目录是如何或为何被创建的好奇用户，下面给出了简化的解释。

- **语法：** `CacheDirLength length`
- **默认设置：** `CacheDirLength 1`
- **上下文：** 服务器配置、虚拟主机

Apache 在创建 URL 数据的缓存路径和文件名时使用了一种哈希方案。例如，当缓存开启且通过代理 Apache 服务器访问一个 URL（例如 `www.microsoft.com`）时，服务器会对该 URL 进行哈希处理，以便日后能快速检索数据。该哈希值可能类似于 `1Y5RxSmB2OQ_HkqkTuXeqvw`。如果 `CacheDirLength` 和 `CacheDirLevels` 指令都使用默认值，Apache 会将 `www.microsoft.com` 上找到的数据存储在一个名为：

`%CacheRoot%/*/1/Y/5/RxSmB2OQ_HkqkTuXeqvw`

的文件中。

这里的 `%CacheRoot%` 是由 `CacheRoot` 指令指定的目录。`1/Y/S` 目录之所以被创建，是因为 `CacheDirLevels` 指令的默认值。当再次使用相同的 URL 请求此文档时，Apache 只需重新计算哈希值即可从指定路径检索页面。

## CacheDirLevels

`CacheDirLevels` 指定了 Apache 创建用于存储缓存数据文件的子目录数量。相关信息请参阅上一节。

- **语法：** `CacheDirLevels levels`
- **默认设置：** `CacheDirLevels 3`
- **默认值：** 无
- **上下文：** 服务器配置、虚拟主机

## CacheDefaultExpire

`CacheDefaultExpire` 提供了一个默认时间（以小时为单位），当文件最后修改时间未知时，用于使缓存文件过期。`CacheMaxExpire` 不会覆盖此设置。

- **语法：** `CacheDefaultExpire hours`
- **默认设置：** `CacheDefaultExpire 1`
- **上下文：** 服务器配置、虚拟主机

## NoCache

- **语法：** `NoCache Domain_name | Subnet | IP_Address | Hostname ...`
- **默认设置：** 无
- **上下文：** 服务器配置、虚拟主机

`NoCache` 指令指定了一个以空格分隔的主机、域名和 IP 地址列表，对于列表中的项目，不执行缓存。该指令应用于禁用对内部网络中本地 Web 服务器的缓存。请注意，代理服务器也会匹配主机的部分名称。如果你想完全禁用缓存，请使用以下配置：

```apache
NoCache *
```

# 配置 Apache 代理服务器

在本节中，我将展示如何将 Apache（使用 `mod_proxy`）配置为正向代理服务器。在你已将 `mod_proxy` 模块编译进 Apache（如前文所述）之后，设置代理服务器就相当简单了。

要启用代理服务器，你需要在 `httpd.conf` 文件中将 `ProxyRequests` 设置为 `On`。额外的配置取决于你希望代理服务器执行什么操作。无论你对代理服务器做何打算，任何你想要用于控制代理服务器行为的指令都应放在一个特殊的 `<Directory ...>` 容器中，格式如下：

```apache
<Directory proxy:*>
.
</Directory>
```

星号（`*`）是请求 URL 的通配符。换句话说，当对 `www.evoknow.com` 的请求由 Apache 服务器处理时，其形式如下：

```apache
<Directory proxy:http://www.evoknow.com>
.
</Directory>
```

你也可以使用 `<Directory ~ /RE/>` 容器，该容器使用正则表达式，允许你在定义代理配置时拥有更大的灵活性。例如：

```apache
<Directory ~ proxy:http://[a-z]+.*/.*>
.
</Directory>
```

现在让我们查看几种常见的代理配置。

## 场景 1：将私有 IP 网络连接到互联网

在此场景中，该网络中只有一台计算机被分配了互联网可路由的 IP 地址，如图 10-3 所示。该计算机运行 Apache 代理服务器，将 `ProxyRequests` 设置为 `On`，且无需额外的代理配置。该代理服务器处理所有请求。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_306_0.png)

在这种配置中，代理服务器需要多宿主；也就是说，它需要能够同时访问不可路由的私有网络（`192.168.1.0`）和可路由的 IP 网络（`206.171.50.0`）。在某种程度上，虽然所选的不可路由 IP 池已经实现了类似功能，但该代理充当了私有 IP 网络的防火墙。代理允许主机访问互联网服务，例如 Web、FTP 等。

## 场景 2：缓存远程 Web 站点

由于互联网和内部网络上的大量 Web 内容很可能是静态的，在本地代理服务器上缓存它们可以节省宝贵的网络带宽。启用缓存的代理服务器仅当缓存中包含已过期文档或请求的文档不存在于缓存中时，才会获取请求的文档。要在你的代理服务器上启用缓存，你需要在特殊的目录容器中指定缓存指令。例如：

```apache
<Directory proxy:*>
CacheRoot /www/cache
CacheSize 1024
CacheMaxExpire 24
</Directory>
```

此配置定义了一个缓存代理服务器，它将缓存文件写入 `/www/cache` 目录。它允许写入 `1024K` 的数据（`1MB`），并且缓存必须在每天（`24` 小时）后过期。

如果你不想允许外部人员滥用你的代理服务器，你可以通过主机限制或用户名/密码认证来限制代理服务器的访问。

要控制哪些主机可以访问代理服务器，你可以创建如下配置：

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
order deny,allow
deny from all
allow from myhost.evoknow.com
</Directory>
```

此配置拒绝了除 `myhost.evoknow.com` 之外的所有访问。如果你想要使用用户名/密码认证，可以使用类似于以下的配置：

```apache
<Directory proxy:*>
AuthType Basic
AuthName Proxy
AuthUserFile /path/to/proxy/.htpasswd
require valid-user
</Directory>
```

**交叉参考** 如果你不确定如何创建必要的密码文件，请参阅第 7 章。

限制对特定协议的访问也是可能的。例如：

```apache
<Directory proxy:http:>
.
</Directory>
```

使你能够控制你的代理服务器如何处理 HTTP 请求。类似地，你可以使用以下配置来控制代理服务器如何处理每个协议：

```apache
<Directory proxy:ftp:*>
.
</Directory>
```

或者

```apache
<Directory proxy:https:*>
...
</Directory>
```

你还可以为代理服务器创建一个专用虚拟主机。在这种情况下，指令应放在代理主机的 `<VirtualHost>` 容器内：

```apache
<VirtualHost proxy.host.com:*>
...
</VirtualHost>
```

## 场景 3：镜像 Web 站点

镜像 Web 站点是远程 Web 站点的本地副本。例如，如果你希望镜像 `www.apache.org` Web 站点，以便你的用户能够快速访问 Apache 信息，你可以使用代理服务器创建这样一个镜像，如下所示：

```apache
ProxyPass / www.apache.org/
CacheRoot /www/cache
CacheDefaultExpire 24
```
