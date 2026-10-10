
Squid 中的缓存服务通过你 Linux 系统的 ICP 端口提供。除了 ICP 服务外，你还可以启用简单网络管理协议（SNMP）。SNMP 让你的计算机为网络上的 SNMP 代理提供统计和状态信息。SNMP 用于监控和维护网络资源。

> 警告：如果配置不当，SNMP 会带来潜在的安全风险。在 Squid 中配置 SNMP 时要小心。

可以使用 `-D` 选项启动 `squid` 守护进程 `/usr/sbin/squid`。配置位于 `/etc/squid/squid.conf`。关于 Squid 的更多信息，请参考 Squid 网页。

## 启动 squid 守护进程

安装 Squid 时，可以通过以下命令检查是否已安装：

```
# rpm -q squid
```

如果未安装 `squid`，可以使用 `yum` 安装它。要检查 `squid` 是否启用，请输入：

```
# chkconfig --list
```

如果你想让服务在启动时运行，请使用以下命令：

```
# chkconfig squid on
```

此时，`squid` 守护进程应该会在系统启动时自动启动。默认情况下，进程将带有 `-D` 选项运行。如果你想添加其他选项，请编辑 `/etc/sysconfig/squid`：

```
SQUID_OPTS="-D"
```

## 第16 章：连接互联网

你可以在引号内添加 `-D` 选项的任何选项。这些选项大部分用于调试：

- `-port`：替换用于默认端口（3128）的端口号。这对于临时尝试替代端口用。
- `-squidfile`：使用此指定备用的 `squid.conf` 文件（`/etc/squid/squid.conf` 之外）。将 `squidfile` 替换为备用文件名。这是尝试新 `squid.conf` 的一个良好级别。
- `-level`：将调试级别更改为 `level` 指定的数字。这也会导致调试消息发送到 `stderr`。
- `-X`：使用此选项检查 `squid.conf` 文件中的值设置是否正确。它会在解释 `squid.conf` 文件时开启完整调试。

你可以使用 `/etc/init.d/squid restart` 重启 `squid` 服务。当 `squid` 守护进程运行时，有几种方法可以运行 `squid` 命令来更改守护进程的工作方式，使用这些选项：

- `reconfigure`：让 Squid 再次读取其配置文件。
- `shutdown`：让 Squid 在等待当前连接退出后退出。
- `interrupt`：立即关闭 Squid，不关闭连接或日志文件。（仅在其他方法无效时使用此选项。）
- `kill`：立即杀死 Squid，不等待连接关闭。

## 使用简单的 squid.conf 文件

你可以使用 Squid 自带的 `/etc/squid/squid.conf` 文件开始。虽然文件包含注释列表，但文件中的实际设置是易于管理的。以下段落描述了默认 `squid.conf` 文件的内容：

```
http_port 3128
```

`http_port` 标签标识 Squid 监听 HTTP 客户端请求的端口。使用的普通端口（默认）是 3128。可选，你可以添加主机名（例如 `example.com:3128`）或 IP 地址（例如 `10.0.0.1:3128`）来限制传入请求为针对特定主机名或 IP 地址的请求。

### 722 第四部分：Fedora RHEL 网络与服务器设置

```
hierarchy_stoplist cgi-bin ?
```

`hierarchy_stoplist` 标签表示当 URL 中出现字符串字符串时，内容应该从原始服务器获取，而不是从缓存节点。在本例中，对字符串 `cgi-bin` 和问号字符 `?` 的请求都将重定向到源服务器。

```
acl QUERY urlpath_regex cgi-bin \\
cache deny QUERY
```

这两行可以用于对包含特定字符的 URL 进行缓存。这些行与上一行配合使用，不缓存包含相同字符串（`cgi-bin` 和 `?`）的 URL，因为这些内容总是从原始服务器请求。

```
acl apache rep_header Server ^Apache
acl all src 0.0.0.0/0.0.0
acl manager proto cache object
acl localhost src 127.0.0.1/255.255.255
```

`acl` 标签用于创建访问控制列表。上述代码中的第一行创建了一个访问控制列表，并将任何包含 `Server-Apache` 的响应头分配给 `acl`。之后，定义 `acl` 包含所有 IP 地址。下一行 `acl` 行将 `manager` `acl` 分配给 `cache_object` 协议。`localhost` 源被分配给 IP 地址 `127.0.0.1`。

```
access_log /var/log/squid/access.log squid
```

上一行标识了 `squid` `access.log` 文件的位置。顾如其名，该文件包含了关于对 Squid 服务器请求的消息。

Squid 包含了默认设置，用于规定缓存中不同类型的内容在多长时间内被认为是新鲜的。`squid.conf` 文件包含了以下 `refresh_pattern` 值：

```
refresh_pattern ^ftp 1440 20% 10080
refresh_pattern ^gopher 1440 0% 1440
refresh_pattern 0% 4320
```

在上述代码中，所有以 `*` 带有 `ftp` 或 `gopher` 开头的行都被设置为 1440 分钟后过期。对象在其生命周期内被视为新鲜的百分比在下一列（20%、0% 和 20%）。最后一列表示对象将刷新的最大分钟数。接下来的几个条目定义了如何处理特定对象以及如何分配对 HTTP 和 ICP 服务的访问。

```
acl SSL_ports port 443
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 # https
```

### 第 16 章：连接互联网 723

```
acl Safe_ports 70          # gopher
acl Safe_ports 210          # wais
acl Safe_ports 1025-65535    # unregistered
acl Safe_ports 280          # http-mgmt
acl Safe_ports 488          # gss-http
acl Safe_ports 591          # filemaker
acl Safe_ports 777          # multilling
acl CONNECT method CONNECT
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
http_reply access allow all
icp_access allow all
```

接下来的章节将详细详细描述这些设置，以及你可能想在 `squid.conf` 文件中设置的其他标签。默认情况下，没有客户端可以使用 Squid 代理服务器，因此你至少想要定义哪些计算机可以访问代理服务。

为了确保此简单的 Squid 配置能够正常工作，请遵循此步骤：

- 1. 在 Squid 服务器上，重启 `squid` 守护进程。使用 `/etc/init.d/squid restart` 实现此。（如果 Squid 未在运行，请使用 `start` 代替 `restart`。）
- 2. 在 Squid 服务器上，启动你的互联网连接（如果尚未启动的话）。
- 3. 在网络上的客户端计算机上，设置 Firefox（或其他 Web 浏览器）使用 Squid 服务器作为代理服务器（本章稍后会描述）。（在 Firefox 中，选择编辑 -> 选项 -> 高级并点击网络选项卡，然后选择设置。在弹出的连接窗口中，选择手动代理配置。为每个协议添加 Squid 服务器的计算机名和默认端口 3128。你也可以勾选“为所有协议使用代理服务器”，以便对浏览器的所有服务请求使用同一个代理。）
- 4. 在客户端计算机上，尝试使用你刚刚配置的浏览器打开互联网上的任何网页。

如果网页没有出现，请查看“调试 Squid”部分以了解如何解决问题。

## 修改 Squid 配置

如果你想为 Squid 设置一组更复杂的访问权限，你应该从默认的 `squid.conf` 配置文件（之前之前描述的）开始。

首先，打开 `/etc/squid/squid.conf` 文件（使用 `root` 用户身份）。你将看到许多描述你可以在文件中设置的值的信息。你配置 Squid 所需的大多数标签都用于设置缓存和提供对你代理服务器的访问。
