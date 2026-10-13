
squid 守护进程（`/usr/sbin/squid`）可以在系统启动时自动启动。设置好之后，Squid 的大部分配置都在 `/etc/squid/squid.conf` 文件中完成。示例 `squid.conf` 文件（`/etc/squid/squid.conf.default`）包含大量关于如何配置 Squid 的信息（该文件包含超过 1800 行注释、示例和默认设置）。

有关 Squid 代理服务器的更多信息，请参阅 Squid Web Proxy Cache 主页（`www.squid-cache.org`）。

## 启动 squid 守护进程

安装 Red Hat Linux 时，你有一个安装 Squid 的机会。如果你不确定 Squid 是否已设置好，有几种方法可以检查。首先，以 root 用户身份输入以下内容：

```
# ps x | grep squid
```

如果 squid 守护进程正在运行，你应该看到类似以下条目的内容：

```
774 ?        S      0:00 squid -D
```

如果你没有看到正在运行的 Squid 进程，则可能没有设置守护进程自动启动。要设置守护进程在启动时运行，请输入以下内容：

```
# chkconfig squid on
```

此时，当系统启动时，squid 守护进程应该会自动启动。默认情况下，squid 守护进程将使用 `-D` 选项运行。`-D` 选项使 Squid 能够在没有活动互联网连接的情况下启动。如果你想要为 squid 守护进程添加其他选项，你可以编辑该启动脚本。首先，制作一个副本（`cp /etc/init.d/squid /etc/init.d/squid.default`），然后编辑 `/etc/rc.d/init.d/squid` 脚本。查找类似以下内容的行：

```
SQUID_OPTS="-D"
```

你可以在引号内添加任何选项，包括 `-D` 选项。这些选项中的大多数对于调试 Squid 非常有用：

- `-a port#` — 用端口号 `port#` 替代默认端口号（3128），用于处理 HTTP 代理请求。这在临时测试备用端口时很有用。
- `-f squidfile` — 使用此选项指定替代的 `squid.conf` 文件（非 `/etc/squid/squid.conf`）。用替代的 `squid.conf` 文件名替换 `squidfile`。这是在替换旧文件之前尝试新 `squid.conf` 文件的好方法。
- `-d level` — 将调试级别更改为 `level` 指示的数字。这还会导致调试消息被发送到 `stderr`。
- `-x` — 使用此选项检查 `squid.conf` 文件中的值是否设置正确。在解释 `squid.conf` 文件时，它会启用完全调试。

通过输入 `/etc/init.d/squid restart`，你可以重启 Squid 服务。当 squid 守护进程正在运行时，有多种方式可以运行 `squid` 命令来改变守护进程的工作方式，使用以下选项：

- `squid -k reconfigure` — 使 Squid 重新读取其配置文件。
- `squid -k shutdown` — 使 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt` — 立即关闭 Squid，不等待连接关闭。
- `squid -k kill` — 立即终止 Squid，不关闭连接或日志文件。（仅当其他方法无效时使用此选项。）

在 squid 守护进程准备就绪后，你现在需要设置 `squid.conf` 配置文件。

## 使用简单的 squid.conf 文件

你可以使用随 squid 附带的 `/etc/squid/squid.conf` 文件来开始。虽然该文件包含大量注释，但其中的实际设置相当易于管理。以下段落描述了默认 `squid.conf` 文件中包含的行：

```
hierarchy_stoplist cgi-bin ?
```

`hierarchy_stoplist` 标签表示，当 URL 中出现某些字符串时，内容应从原始服务器获取，而不是从缓存对等点获取。在这个例子中，针对字符串 `cgi-bin` 和问号字符 `?` 的请求都会被转发到源服务器。

```
acl QUERY urlpath_regex cgi-bin \?
no_cache deny QUERY
```

上述两行可用于使包含特定字符的 URL 永远不被缓存。这些行与上一行配合使用，通过不缓存包含相同字符串（`cgi-bin` 和 `?`）的 URL，而这些字符串总是从原始服务器获取。

```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

`acl` 标签用于创建访问控制列表。上面的第一行创建了一个名为 "`all`" 的访问控制列表，包含所有 IP 地址。下一个 `acl` 行将 `manager` `acl` 分配给处理 `cache_object` 协议。`localhost` 源被分配给 IP 地址 `127.0.0.1`。

接下来的几个条目定义了特定端口的处理方式以及 HTTP 和 ICP 服务的访问权限分配。

```
acl SSL_ports port 443 563
acl Safe_ports port 80            # http
acl Safe_ports port 21            # ftp
acl Safe_ports port 443 563       # https, snews
acl Safe_ports port 70            # gopher
acl Safe_ports port 210           # wais
acl Safe_ports port 1025-65535    # unregistered ports
acl Safe_ports port 280           # http-mgmt
acl Safe_ports port 488           # gss-http
acl Safe_ports port 591           # filemaker
acl Safe_ports port 777           # multiing http
acl CONNECT method CONNECT
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
icp_access allow all
```

以下部分详细说明了这些设置，以及你可能希望在 `squid.conf` 文件中设置的其他标签。

为了确保这个简单的 Squid 配置正常工作，请遵循以下步骤：

1. 在 Squid 服务器上，重启 squid 守护进程。为此，要么重启计算机，要么输入 `/etc/init.d/squid restart`。（如果 Squid 未运行，请使用 `start` 代替 `restart`。）
2. 在 Squid 服务器上，启动你的互联网连接（如果尚未连接）。
3. 在网络中的客户端计算机上，设置 Netscape（或其他 Web 浏览器）使用 Squid 服务器作为代理服务器（在本章后面描述）。（在 Netscape 中，选择 编辑 → 首选项 → 高级 → 代理，然后选择 手动代理配置 → 查看，并为每个协议添加 Squid 服务器的计算机名称和默认端口 3128。）
4. 在客户端计算机上，尝试使用刚刚配置的浏览器打开互联网上的任何网页。

如果网页没有显示，请参阅调试 Squid 部分以获取解决此问题的建议。

## 修改 Squid 配置文件

如果你想要为 Squid 设置更复杂的访问权限集，你应该从默认的 `squid.conf` 配置文件（前面已描述）开始。

首先，以 root 用户身份打开 `/etc/squid/squid.conf` 文件。你会看到大量描述你可以在此文件中设置的值的信息。通常，配置 Squid 所需的大多数标签都用于设置缓存并为你的代理服务器提供主机访问权限。

> **提示**：不要修改 `squid.conf.default` 文件！如果你真的搞乱了你的 `squid.conf` 文件，你可以通过将此文件再次复制为 `squid.conf` 来重新开始。如果你想确切回顾到目前为止所做的更改，请在 `/etc/squid` 目录下输入以下内容：
>
> ```
> # diff squid.conf squid.conf.default | less
> ```
>
> 这将显示你的实际 `squid.conf` 和你开始时使用的版本之间的差异。

## 在 squid.conf 中配置访问控制
