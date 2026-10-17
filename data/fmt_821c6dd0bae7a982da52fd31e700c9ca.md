
# rpm -q squid

squid-2.6.STABLE16-1.fc8

# 第 16 章：连接网络 711

如果没有安装 squid，可以从随书提供的 DVD 进行安装，或者通过输入 `yum squid` 通过网络安装。接下来，你可以检查 squid 是否已配置为运行。要这样做，请输入以下命令：

```bash
# chconfig --list squid
squid 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```

如果 squid 服务在级别 3、4 和 5 是关闭的（如果默认所有级别都是关闭的），你可以将其设置为启动时自动启动。要设置 squid 守护进程启动时运行，请输入：

```bash
# chconfig squid
```

此时，squid 守护进程会在系统启动时自动启动。默认情况下，squid 守护进程将带有 `-D` 选项运行。`-D` 选项允许 Squid 在没有活动 Internet 连接的情况下启动。如果你想为 squid 守护进程添加其他选项，可以编辑 `/etc/sysconfig/squid` 配置文件。寻找类似下面的一行：

```bash
SQUID_OPTS="-D"
```

你可以在引号内添加任何与 `-D` 选项的选项。这些选项大部分对调试 Squid 非常有用：

- `-a port#` 替换 `port#`，该端口号将代替默认端口号（3128）来提供 HTTP 代理请求。这对于临时尝试替代端口有用。
- `-squidfile` 使用此选项指定备用的 `squid.conf` 文件（`/etc/squid/squid.conf` 之外）。将 `squidfile` 替换为替代 `squid.conf` 文件的文件名。这是替换旧文件之前尝试新 `squid.conf` 文件的好方法。
- `-d level` 将调试级别更改为 `level` 指示的数字。这将导致调试消息发送到 stderr。
- `-X` 使用此选项检查值是否正确位于你的 `squid.conf` 文件中。它会在解释 `squid.conf` 文件时运行完整调试。

你可以通过输入 `/etc/init.d/squid restart` 来重启 squid 服务。在 squid 守护进程运行时，有几种方法可以运行 squid 命令来更改守护进程的工作方式，即使用这些选项：

- `squid -k reconfigure` 导致 Squid 重新读取其配置文件。
- `squid -k shutdown` 导致 Squid 在短暂等待当前连接退出后退出。
- `squid -k interrupt` 立即关闭 Squid，而不等待连接关闭。

## 第四部分：Fedora 和 RHEL 网络和服务器设置

- `squid -k kill` — 立即杀死 Squid，不关闭连接或日志文件。（如果其他方法不起，请使用此选项。）

当 squid 守护进程准备好运行后，你需要设置 `squid.conf` 配置文件。

### 使用简单的 squid.conf 文件

你可以使用 Squid 随附的 `/etc/squid/squid.conf` 文件开始。尽管该文件包含许多注释，但该文件中的实际设置是非常容易管理的。接下来的段落描述了默认 `squid.conf` 文件的内容：

```
http_port 3128
```

`http_port` 标签标识 Squid 监听 HTTP 客户端请求的端口。使用的普通端口（默认值）是 3128。可选地，你可以添加主机名（例如 `example.com:3128`）或 IP 地址（如 `10.0.0.1:3128`），以限制允许的入请求为指向特定主机名或 IP 地址的请求。

```
hierarchy_stoplist cgi-bin ?
```

`hierarchy_stoplist` 标签表示，当 URL 中出现特定字符串时，应该从原始服务器获取内容，而不是从缓存节点获取。在本例中，对 `cgi-bin` 和问号 (`?`) 的请求都将转发到源服务器 server。

```
acl url_path_regex cgi-bin \
cache deny QUERY
```

```
acl apache req_header Server ^Apache
acl all src 0.0.0.0/0
acl manager proxy cache_object
acl localhost src 127.0.0.1/255.255.255.255
```

前面的两行可以用于使包含某些字符的 URL 永远不缓存。它们与上一行配合使用，不缓存包含相同字符串（`cgi-bin` 和 `?`）的 URL，因为这些内容总是从源服务器获取。

`acl` 标签用于创建访问控制列表。后续代码中的第一行创建一个名为 `apache` 的访问控制列表，并将任何包含 Server "Apache" 的响应标头分配给 `apache` acl。之后，定义的 `all` acl 包含所有 IP 地址。下一行 `acl` 将 `manager` acl 分配以处理 `cache_object` 协议。`localhost` 源被分配给 IP 地址 `127.0.0.1`。

```
access_log /var/log/squid/access.log squid
```

前面的行标识了 Squid 访问日志文件的位置。正如名称所示，此文件包含关于指向 Squid 服务器请求的消息。

# 第 16 章：连接网络 713

Squid 包含了关于如何考虑缓存中不同类型内容的默认设置。Squid 中包含以下值：

```
refresh_pattern ^/ 1440 20
refresh_pattern ^/g 1440 20
refresh_pattern -1 -1 1440 20
```

`refresh_pattern` 标签定义了对象被认为新鲜的时间。第一个数字是以秒为单位的最大年龄，第二个是以秒为单位的最小年龄，第三是以秒为单位的刷新间隔，第四个是触发刷新必须重新下载的文件百分比。

以下示例显示了如何使用刷新模式：

```
acl url_path_regex cgi-bin \
cache deny url_path_regex
```

这将防止对 `cgi-bin` 目录的任何被缓存。

```
acl apache req_header Server ^Apache
cache deny apache
```

这将防止任何来自 Apache 服务器的请求被缓存。

```
access allow src 0.0.0.0
access deny all
```

这将允许所有请求访问代理，但拒绝所有缓存。

```
access allow localhost
access bypass localhost
access deny all
```

这将允许本地主机使用代理并拒绝所有其他请求。

### 在 squid.conf 中配置访问控制

为了保护你的计算资源不被任何人使用，Squid 要求你定义哪些主机访问你的 HTTP 服务。默认情况下，除了本地主机外，所有主机都被访问 Squid 服务。通过 `acl` 标签，你可以创建访问列表。然后，通过 `http_access` 标签，你可以为访问列表授权访问 HTTP 服务。

访问控制列表 (`acl`) 的形式为：

```
acl name type string
acl name type file
```

`name` 是分配给列表的任何名称。`string` 是文本字符串，`file` 是适用于特定 `acl` 信息的文件。有效的 `acl` 类型包括 `dst`, `src`, `dstdomain`, `srcdomain`, `url_pattern`, `url_pattern`, `time`, `proto`, `method`, `browser` 和 `user`。

设置了几个访问控制列表。你可以使用这些分配的 `acl` 名称来为 HTTP 或 ICP 服务分配权限。你也可以创建自己的 `acl` 名称来分配

# 第 16 章：连接到互联网 715

服务。以下是来自 `/etc/squid/squid.conf` 的默认 `acl` 名称，你可以使用或更改它们：

```
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255
acl SSL ports port 443 563
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # vais
acl Safe_ports port 1025-65535 # unregistered
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
```
