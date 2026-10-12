
squid 守护进程（`/usr/sbin/squid`）可以在系统启动时自动启动。设置完成后，Squid 大部分配置都在 `/etc/squid/squid.conf` 文件中完成。squid.conf 文件包含大量关于如何配置 Squid 的信息（该文件包含超过 3200 行注释和示例，尽管只有 32 行活动设置）。

有关 Squid 代理服务器的更多信息，请参阅 Squid Web Proxy Cache 主页（www.squid-cache.org）。

## 启动 squid 守护进程

安装 Red Hat Linux 时，您有机会安装 Squid（squid 软件包）。如果不确定 Squid 是否已设置，有几种方法可以检查。首先，以 root 用户身份输入以下内容：

```
# ps x | grep squid
```

如果 squid 守护进程正在运行，您应该会看到类似以下内容的条目：

```
774 ? S 0:00 squid -D
```

如果看不到 Squid 进程正在运行，守护进程可能未设置为自动启动。要设置守护进程在启动时启动，请输入以下内容：

```
# chkconfig squid on
```

此时，squid 守护进程应在系统启动时自动启动。默认情况下，squid 守护进程将使用 -D 选项运行。-D 选项使 Squid 在没有活动 Internet 连接的情况下启动。如果您想为 squid 守护进程添加其他选项，可以编辑 `/etc/sysconfig/squid` 配置文件。查找类似以下的行：

```
SQUID_OPTS="-D"
```

您可以在引号之间添加任何选项以及 -D 选项。这些选项中的大多数对于调试 Squid 很有用：

- **-a port#** — 用 port# 替换为将用于处理 HTTP 代理请求的端口号，而不是默认端口号（3128）。这对于临时尝试替代端口很有用。
- **-f squidfile** — 使用此选项指定替代的 `squid.conf` 文件（而不是 `/etc/squid/squid.conf`）。将 *squidfile* 替换为替代 `squid.conf` 文件的名称。这是在替换旧文件之前尝试新 `squid.conf` 文件的好方法。
- **-d level** — 将调试级别更改为 *level* 指示的数字。这也会导致调试消息发送到 *stderr*。
- **-X** — 使用此选项检查 **squid.conf** 文件中的值是否设置正确。它在解释 **squid.conf** 文件时会打开完整调试。

您可以通过输入 /etc/init.d/squid restart 来重启 Squid 服务。在 squid 守护进程运行时，您可以使用以下选项以几种方式运行 squid 命令来更改守护进程的工作方式：

- **squid -k reconfigure** — 导致 Squid 再次读取其配置文件。
- **squid -k shutdown** — 导致 Squid 在等待当前连接退出后退出。
- **squid -k interrupt** — 立即关闭 Squid，而不等待连接关闭。
- **squid -k kill** — 立即杀死 Squid，而不关闭连接或日志文件。（仅在其他方法不起作用时使用此选项。）

squid 守护进程准备好运行后，您需要设置 **squid.conf** 配置文件。

## 使用简单的 squid.conf 文件

您可以使用随 squid 提供的 /etc/squid/squid.conf 文件开始使用。尽管该文件包含大量注释，但其中的实际设置相当易于管理。以下段落描述了默认 squid.conf 文件的内容：

```
hierarchy_stoplist cgi-bin ?
```

**hierarchy_stoplist** 标签表示当 URL 中出现某些字符字符串时，内容应从原始服务器获取，而不是从缓存对等体获取。在此示例中，对字符串 cgi-bin 和问号字符（？）的请求都转发到源服务器。

```
acl QUERY urlpath_regex cgi-bin \/?
no_cache deny QUERY
```

前两行可用于使包含某些字符的 URL 永不被缓存。它们与前一行一起工作，不缓存包含相同字符串（cgi-bin 和 ？）的 URL，而这些 URL 总是从原始服务器获取。

```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

**acl** 标签用于创建访问控制列表。上面的第一行创建了一个名为“all”的访问控制列表，其中包含所有 IP 地址。下一个 **acl** 行将 manager **acl** 分配为处理 **cache_object** 协议。**localhost** 源被分配给 IP 地址 127.0.0.1。

接下来几项定义了如何处理特定端口以及如何分配 HTTP 和 ICP 服务的访问权限。

```
acl SSL_ports port 443 563
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
acl Safe_ports port 777 # multiling http
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

以下部分更详细地描述了这些设置，以及您可能想要在 squid.conf 文件中设置的其它标签。默认情况下，没有客户端可以使用 squid 代理服务器，因此您至少需要定义哪些计算机可以访问代理服务。

要确保此简单 Squid 配置正常工作，请按照以下步骤操作：

- 1. 在 Squid 服务器上，重启 squid 守护进程。为此，可以重新启动或输入 /etc/init.d/squid restart。（如果 Squid 未运行，请使用 start 而不是 restart。）
- 2. 在 Squid 服务器上，启动您的 Internet 连接（如果尚未启动）。
- 3. 在网络上的客户端计算机上，设置 Mozilla（或其他 Web 浏览器）以使用 Squid 服务器作为代理服务器（本章后面描述）。（在 Mozilla 中，选择 Edit → Preferences → Advanced → Proxies，然后选择 Manual proxy configuration 并添加 Squid 服务器的计算机名称以及默认端口 3128 到每个协议。）
- 4. 在客户端计算机上，尝试使用您刚配置的浏览器打开 Internet 上的任何网页。

如果网页未出现，请参阅 Squid 调试部分，了解如何修复问题。

## 修改 Squid 配置文件

如果您想为 Squid 设置更复杂的访问权限集，应从默认的 squid.conf 配置文件（前面已描述）开始。

首先，以 root 用户身份打开 `/etc/squid/squid.conf` 文件。您将看到大量描述可在该文件中设置的值的信息。您需要配置 Squid 的大多数标签用于设置缓存并为代理服务器提供主机访问。

> **TIP:** 不要更改 *squid.conf.default* 文件！如果您真的搞乱了 *squid.conf* 文件，您可以通过复制此文件到 *squid.conf* 来重新开始。如果您想准确回忆迄今为止所做的更改，请从 `/etc/squid` 目录输入以下内容：
> 
> ```
> # diff squid.conf squid.conf.default | less
> ```
> 
> 这将显示您实际的 *squid.conf* 与您开始时的版本之间的差异。

## 在 squid.conf 中配置访问控制

为保护计算资源不被任何人使用，Squid 要求您定义哪些主机计算机可以访问您的 HTTP（Web）服务。默认情况下，除本地主机外，所有主机均被拒绝访问 Squid HTTP 服务。使用 `acl` 标签，您可以创建访问列表。然后，使用 `http_access` 标签，您可以为创建的访问列表授权对 HTTP（Web）服务的访问。

访问控制列表标签（`acl`）的形式为：

```
acl name type string
acl name type file
```

名称是您想要分配给列表的任何名称。`string` 是文本字符串，`file` 是适用于特定 `type` 的 `acl` 的信息文件。有效的 `acl` 类型包括 `dst`、`src`、`dstdomain`、`srccdomain`、`url_path_pattern`、`url_pattern`、`time`、`port`、`proto`、`method`、`browser` 和 `user`。

默认情况下设置了多个访问控制列表。您可以使用这些分配的 `acl` 名称为 HTTP 或 ICP 服务分配权限。您也可以创建自己的 `acl` 名称分配给这些服务。以下是来自 `/etc/squid/squid.conf` 文件的默认 `acl` 名称，您可以使用或更改：

```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl SSL_ports port 443 563
acl Safe_ports port 80		# http
acl Safe_ports port 21		# ftp
acl Safe_ports port 443 563	# https, snews
acl Safe_ports port 70		# gopher
acl Safe_ports port 210		# wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280		# http-mgmt
acl Safe_ports port 488		# gss-http
acl Safe_ports port 591		# filemaker
acl Safe_ports port 777		# multiling http
acl CONNECT method CONNECT
```
