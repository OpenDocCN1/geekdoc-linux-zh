
进入`/path/to/xxx`目录，找到`xxx.json`。

`http_port`标签标识 Squid 监听 HTTP 客户端请求的端口。通常使用的端口（也是默认端口）是 3128。可选地，你可以添加主机名（如`example.com:3128`）或 IP 地址（如`10.0.0.1:3128`），以将允许的传入请求限制为针对特定主机名或 IP 地址的请求。

```
hierarchy_stoplist cgi-bin ?
```

`hierarchy_stoplist`标签指示当 URL 中出现特定字符串时，内容应从原始服务器获取，而不是从缓存对等节点获取。在此示例中，针对字符串`cgi-bin`和问号字符`?`的所有请求都转发到源服务器。

```
acl QUERY urlpath_regex cgi-bin ?\
cache deny QUERY
```

前面的两行可以用于使包含特定字符的 URL 永远不被缓存。这些行与前一行配合使用，不缓存包含相同字符串（`cgi-bin`和`?`）的 URL，这些字符串总是从原始服务器获取。

```
acl apache rep_header Server ^Apache
acl all src 0.0.0.0/0.0.0.0/0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

`acl`标签用于创建访问控制列表。前面代码中的第一行创建一个名为`apache`的访问控制列表，并将任何包含`Server ^Apache`的响应头分配给`apache acl`。之后，`all acl`被定义为包含所有 IP 地址。下一个`acl`行将`manager acl`分配给处理`cache_object`协议。`localhost`源分配给 IP 地址`127.0.0.1`。

```
access_log /var/log/squid/access.log squid
```

前一行标识了 Squid `access.log`文件的位置。顾名思义，该文件包含有关访问 Squid 服务器请求的消息。

Squid 包含默认设置，规定缓存中不同类型的内容在考虑为新鲜时保持的时间。`squid.conf`文件中包含以下`refresh_pattern`值：

| refresh_pattern | ^ftp: | 1440 | 20% | 10080 |

|---|---|---|---|---|

| refresh_pattern | ^gopher: | 1440 | 0% | 1440 |

| refresh_pattern | . | 0 | 20% | 4320 |

在刚刚显示的代码中，所有以 ftp 或 gopher 开头（^）的行都设置为在 1440 分钟后过期。对象年龄中被认为新鲜的时间百分比显示在下一列（20%、0% 和 20%）。最后一列指示对象被认为新鲜的最大分钟数。接下来的几个条目定义了特定端口的处理方式以及 HTTP 和 ICP 服务的访问分配。

```
acl SSL_ports port 443
acl Safe_ports port 80        # http
acl Safe_ports port 21         # ftp
acl Safe_ports port 443        # https
acl Safe_ports port 70         # gopher
acl Safe_ports port 210        # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280        # http-mgmt
acl Safe_ports port 488        # gss-http
acl Safe_ports port 591        # filesmaker
acl Safe_ports port 777        # multiling http
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

以下部分将更详细地描述这些设置，以及你可能希望在`squid.conf`文件中设置的其他标签。默认情况下，没有客户端可以使用 Squid 代理服务器，因此你至少需要定义哪些计算机可以访问代理服务。为了确保此简单的 Squid 配置正在工作，请按照以下步骤操作：

1. 在 Squid 服务器上，重新启动 squid 守护进程。为此，请键入`/etc/init.d/squid restart`。（如果 Squid 未运行，请使用 start 而不是 restart。）
2. 在 Squid 服务器上，启动你的互联网连接（如果尚未连接）。
3. 在网络的客户端计算机上，设置 Firefox（或其他 Web 浏览器）使用 Squid 服务器作为代理服务器（在本章后面描述）。（在 Firefox 中，选择 编辑 -> 首选项 -> 高级，然后单击 网络 选项卡，然后选择 设置。从

在弹出的“连接设置”窗口中，选择“手动代理配置”。然后为每个协议添加 Squid 服务器的计算机名称和默认端口 3128。你还可以勾选“对所有协议使用此代理服务器”选项，以便浏览器使用相同的代理来处理所有服务请求。

- 在客户端计算机上，尝试使用刚才配置的浏览器打开 Internet 上的任何网页。

如果网页未显示，请参阅“调试 Squid”部分了解如何修复此问题。

## 修改 Squid 配置文件

如果你想为 Squid 设置更复杂的访问权限，应从默认的`squid.conf`配置文件（前文已描述）开始。

首先，以 root 用户身份打开`/etc/squid/squid.conf`文件。你将看到大量描述该文件中可设置值的信息。配置 Squid 所需的大多数标签都用于设置缓存并为你的代理服务器提供主机访问。

> **提示：** 不要更改默认的`squid.conf`文件！如果你真的搞乱了你的 squid.conf 文件，可以通过将此文件的另一个副本重命名为 squid.conf 重新开始。如果你想确切回忆起目前所做更改，请在`/etc/squid`目录中输入以下命令：

```
# diff squid.conf squid.conf.default | less
```

这将显示你实际的`squid.conf`与起始版本之间的差异。

## 在 squid.conf 中配置访问控制

为了保护你的计算资源不被任何人使用，Squid 要求你定义哪些主机可以访问你的 HTTP（Web）服务。默认情况下，除本地主机外，所有主机均被拒绝访问 Squid HTTP 服务。使用`acl`标签，你可以创建访问列表。然后，使用`http_access`标签，你可以为你创建的访问列表授权访问 HTTP（Web）服务。

访问控制列表标签（`acl`）的形式为：

```
acl name type string
acl name type file
```

`name`是你要希望分配给列表的任何名称。`string`是文本字符串，而`file`是包含适用于特定 acl 类型的信息的文件。有效的 acl 类型包括`dst`、`src`、`dstdomain`、`srccdomain`、`url_path_pattern`、`url_pattern`、`time`、`port`、`proto`、`method`、`browser`和`user`。

默认情况下会设置多个访问控制列表。你可以使用这些分配的 acl 名称来为 HTTP 或 ICP 服务分配权限。你也可以创建自己的 acl 名称来为这些服务分配权限。以下是来自`/etc/squid/squid.conf`文件的默认 acl 名称，你可以使用或修改它们：
