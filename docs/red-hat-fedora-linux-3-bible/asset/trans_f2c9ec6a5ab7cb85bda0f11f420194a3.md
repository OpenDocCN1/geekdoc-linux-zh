

此时，squid 守护进程应在系统启动时自动启动。默认情况下，squid 守护进程将使用 `-D` 选项运行。`-D` 选项允许 Squid 在没有活动的互联网连接的情况下启动。如果你希望为 squid 守护进程添加其他选项，可以编辑 `/etc/sysconfig/squid` 配置文件。查找类似以下内容的行：

```
SQUID_OPTS="-D"
```

你可以在引号内添加任何选项，包括 `-D` 选项。这些选项大多用于调试 Squid：

- **`-a port#`** — 将 *port#* 替换为一个端口号，该端口号将用于替代默认端口号（3128）来处理 HTTP 代理请求。这对于临时测试替代端口非常有用。
- **`-f squidfile`** — 使用此选项指定替代的 `squid.conf` 文件（除 `/etc/squid/squid.conf` 外的文件）。将 *squidfile* 替换为替代的 `squid.conf` 文件的名称。这是在你替换旧文件之前试用新的 `squid.conf` 文件的好方法。
- **`-d level`** — 将调试级别更改为 *level* 指示的数字。这还会导致调试消息被发送到 `stderr`。
- **`-X`** — 使用此选项检查你的 `squid.conf` 文件中的值是否设置正确。它在解释 `squid.conf` 文件时开启完全调试。

你可以通过输入 `/etc/init.d/squid restart` 来重启 squid 服务。在 squid 守护进程运行期间，你可以使用以下选项通过运行 `squid` 命令来改变守护进程的工作方式，有几种方法：

- **`squid -k reconfigure`** — 导致 Squid 重新读取其配置文件。
- **`squid -k shutdown`** — 导致 Squid 在短暂等待当前连接退出后退出。
- **`squid -k interrupt`** — 立即关闭 Squid，不等待连接关闭。
- **`quid -k kill`** — 立即终止 Squid，不关闭连接或日志文件。（仅在其他方法不起作用时使用此选项。）

当 squid 守护进程准备好运行后，你需要设置 `squid.conf` 配置文件。

## 使用简单的 squid.conf 文件

你可以使用随 Squid 附带的 `/etc/squid/squid.conf` 文件作为起点。虽然该文件包含大量注释，但其中的实际设置相当易于管理。以下几段描述了默认 `squid.conf` 文件的内容：

```
hierarchy_stoplist cgi-bin ?
```

**hierarchy_stoplist** 标签表明，当 URL 中出现特定的字符串时，内容应从原始服务器获取，而不是从缓存对等节点获取。在此示例中，对于字符串 **cgi-bin** 和问号字符 (?) 的请求都转发到源服务器。

```
acl QUERY urlpath_regex cgi-bin \
no_cache deny QUERY
```

上述两行可用于使包含特定字符的 URL 永不被缓存。这些行与上一行配合使用，即不缓存包含相同字符串（**cgi-bin** 和 ?）的 URL，而这些字符串始终从原始服务器获取。

```
acl all src 0.0.0.0/0:0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

**acl** 标签用于创建访问控制列表。上面第一行创建一个名为 **all** 的访问控制列表，包含所有 IP 地址。下一行 **acl** 将 **manager** **acl** 分配给处理 **cache_object** 协议。**localhost** 源被分配给 IP 地址 127.0.0.1。

接下来的几个条目定义了特定端口的处理方式，以及 HTTP 和 ICP 服务的访问权限分配。

```
acl SSL_ports port 443 563
acl Safe_ports port 80   # http
acl Safe_ports port 21   # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70   # gopher
acl Safe_ports port 210  # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280  # http-mgmt
acl Safe_ports port 488  # gss-http
acl Safe_ports port 591  # filemaker
acl Safe_ports port 777  # multiling http
acl CONNECT method CONNECT
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
http_reply_access allow all
icp_access allow all
```

以下部分将更详细地描述这些设置，以及你希望在 **squid.conf** 文件中设置的其他标签。默认情况下，没有客户端可以使用 Squid 代理服务器，因此你至少需要定义哪些计算机可以访问代理服务。

为了确保这个简单的 Squid 配置正常工作，请遵循此过程：

1. 在 Squid 服务器上，重启 squid 守护进程。为此，请输入 `/etc/init.d/squid restart`。
   （如果 Squid 未在运行，请使用 `start` 而不是 `restart`。）
2. 在 Squid 服务器上，启动你的互联网连接（如果尚未启动）。
3. 在网络上的客户端计算机上，设置（使用 Mozilla 或其他 Web 浏览器）将 Squid 服务器用作代理服务器（在本章稍后描述）。（在 Mozilla 中，选择 编辑 → 首选项 → 高级 → 代理，然后选择 手动代理配置，并为每个协议添加 Squid 服务器的计算机名称以及默认的 3128 端口。）
4. 在客户端计算机上，尝试使用刚刚配置的浏览器打开互联网上的任何网页。

如果网页未出现，请参阅“调试 Squid”部分了解如何修复问题。

## 修改 Squid 配置文件

如果你想为 Squid 设置更复杂的访问权限集，你应该从默认的 `squid.conf` 配置文件（前文已描述）开始。

首先，以 root 用户身份打开 `/etc/squid/squid.conf` 文件。你会看到大量描述该文件中可设置值的信息。大多数用于配置 Squid 的标签用于设置缓存并为你的代理服务器提供主机访问。

> **提示：** 不要修改 `squid.conf.default` 文件！如果你真的搞乱了你的 `squid.conf` 文件，你可以通过将此文件的另一个副本复制为 `squid.conf` 来重新开始。如果你想确切回忆到目前为止所做的更改，请从 `/etc/squid` 目录输入以下内容：
>
> ```
> # diff squid.conf squid.conf.default | less
> ```
>
> 这将显示你的实际 `squid.conf` 与起始版本之间的差异。

## 在 squid.conf 中配置访问控制

为了保护你的计算资源不被任何人使用，Squid 要求你定义哪些主机计算机有权访问你的 HTTP（Web）服务。默认情况下，除了本地主机外，所有主机都被拒绝访问 Squid HTTP 服务。使用 `acl` 标签，你可以创建访问列表。然后，使用 `http_access` 标签，你可以为你创建的访问列表授权访问 HTTP（Web）服务。

访问控制列表标签（`acl`）的形式为：

```
acl name type string
acl name type file
```

*name* 是你想分配给列表的任何名称。*string* 是文本字符串，*file* 是适用于特定 `acl` 类型的信息文件。有效的 `acl` 类型包括 `dst`、`src`、`dstdomain`、`srccomain`、`url_path_pattern`、`url_pattern`、`time`、`port`、`proto`、`method`、`browser` 和 `user`。

默认设置了多个访问控制列表。你可以使用这些指定的 `acl` 名称来为 HTTP 或 ICP 服务分配权限。你也可以创建自己的 `acl` 名称分配给这些服务。以下是来自 `/etc/squid/squid.conf` 文件的默认 `acl` 名称，你可以使用或更改它们：

```
acl all src 0.0.0.0/0.0.0.0
acl localhost src 127.0.0.1/255.255.255.255
acl SSL_ports port 443 563
acl Safe_ports port 80              # http
acl Safe_ports port 21              # ftp
acl Safe_ports port 443 563         # https, snews
acl Safe_ports port 70              # gopher
acl Safe_ports port 210             # wais
acl Safe_ports port 1025-65535      # unregistered ports
acl Safe_ports port 280             # http-mgmt
acl Safe_ports port 488             # gss-http
acl Safe_ports port 591             # filemaker
acl Safe_ports port 777             # multiling http
acl CONNECT method CONNECT
```

当 Squid 试图确定特定计算机属于哪个类别时，它从上到下进行检查。在第一行中，所有主机计算机（地址/子网掩码全为零）被添加到 `acl` 组 `all`。在第二行中，你创建了一个名为 `manager` 的 `manager` 组，该组拥有访问你的 `cache_object`（从缓存获取内容的功能）的权限。`localhost` 组被分配给你的回环地址。安全套接层（SSL）端口被分配给数字 443 和 563，而 `Safe_ports` 被分配给上述显示的数字。最后一行定义了一个名为 `CONNECT` 的组（你可以使用它来允许访问 SSL 站点）。

为了拒绝或启用 Squid 计算机上 HTTP 服务的访问，设置了以下定义：

```
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
```

这些定义相当严格。第一行允许本地主机请求缓存对象（manager）的人这样做，但第二行拒绝其他人提出此类请求。访问不会被拒绝给定义为安全端口的端口。此外，通过代理的安全套接字连接在所有端口上都被拒绝，除了 SSL 端口（`!SSL_ports`）。HTTP 访问仅允许来自本地主机，并拒绝所有其他主机。

