
要在系统启动时自动启动 Squid，你可以通过以下命令将其添加到 init 进程中

`insserv squid`

### 理解 Squid 配置

Squid 的配置文件 (`/etc/squid.conf`) 在文件内有详尽的注释，并有完整的文档说明。

此文件中仅需调整少数条目即可配置基础的代理服务器功能；大多数参数可以保留默认值。如果未提供其他值，或者该条目以注释符号开头，则将使用默认值。

` s quid.conf` 文件中的配置选项也称为“标签（tag）”。以下是最重要的标签列表：

- 网络标签（Network Tags）
- 缓存大小标签（Cache Size Tags）
- 日志文件与缓存目录标签（Log Files and Cache Directories Tags）
- 调优标签（Fine-Tuning Tags）
- 超时标签（Time-Out Tags）
- 管理标签（Administrative Tags）
- 错误标签（Error Tags）

## 网络标签

你可以设置以下标签：

- `http_port`。Squid 等待请求的端口默认设置为 3128。通常会设置另一个端口，例如 8080。

如果你在具有外部和内部网络接口的网关上运行 Squid，也可以以 `ip_address:port` 的形式指定 Squid 应该监听的 IP 地址。这样你就可以确保代理服务器只能从内部网络访问。

## 缓存大小标签

你可以设置以下标签：

- `cache_mem`。此参数决定了 Squid 使用多少物理 RAM 来缓存数据（最常用的响应）。除了 RAM 缓存外，Squid 还会使用硬盘进行缓存。

Squid 的实际内存占用取决于磁盘上缓存的大小。根据经验，Squid 每对于 1 GB 的总磁盘缓存空间大约使用 10 MB 的 RAM，加上 `cache_mem` 中指定的数量，再加上另外 10-20 MB。建议 Squid 服务器至少拥有此两倍的物理内存。

- `cache_swap_low`, `cache_swap_high`。这指的是预留用于缓存文件的磁盘空间（参见 `cache_dir` 标签）。

这两个值定义了理想阈值。当磁盘上文件占用的空间超过低值（`cache_swap_low`）时，Squid 开始从磁盘中删除文件；如果尽管如此达到了第二个值（`cache_swap_high`），文件将以更激进的方式被删除。默认值 90/95 适用于大多数场景。

- `maximum_object_size`。大于此值的对象（文件）将不会缓存在磁盘上。默认值为 4096 (4 MB)。

- `minimum_object_size`。小于此值的对象（文件）将完全不被缓存。默认值为 0 (0 KB)。

- `maximum_object_size_in_memory`。大于此值的对象（文件）将不会缓存在 RAM 缓存中。此值应保持足够大，以便频繁请求的对象可以存储在 RAM 缓存中。

- `ipcache_size`, `ipcache_low`, `ipcache_high`。Squid 会缓存域名解析。这些参数决定了缓存多少个 IP 地址（`ipcache_size`）、Squid 何时开始从缓存中移除 IP 地址（`ipcache_low`），以及何时以更激进的方式执行删除（`ipcache_high`）。后两个是百分比，默认值分别为 90 和 95。

## 日志文件与缓存目录标签

你可以设置以下标签：

- `cache_dir`。此标签决定了 Squid 在何处以及如何在大硬盘上缓存数据。

该标签使用以下格式

```
cache_dir storage_format dir size L1-dirs L2-options
```

- `storage_format`。决定 Squid 使用何种方法在硬盘上存储数据。默认是 `ufs`，这是传统的 Squid 存储方法。其他可能的方法（如 `aufs`）直接记录在 Squid 配置文件中。

- `dir`。决定 Squid 存储其缓存文件的目录。在默认配置中，Squid 使用 `/var/cache/squid`。

- `size`。`size` 参数设置缓存的大小。默认情况下，Squid 使用 `/var/cache/squid`。

- `L1-dir`。默认值是 100。

- `L2-dir`。Squid 接收到连接的。。默认值是 256。

- `options`。Squid 存储方法的选项。在在 中。默认情况下 `cache_dir` 的配置如下

```
cache_dir ufs /var/cache/squid 100000 90 95
```

- `cache_access_log`。决定 Squid 在何处存储访问日志文件。默认位置是 `/var/log/squid/access.log`。

- `cache_log`。定义 Squid 在何处存储缓存日志。此文件用于记录 Squid 的特定信息。默认位置是 `/var/log/squid/cache.log`。

- `store_log`。定义存储存储的日志文件。此文件用于记录 Squid 的特定信息。默认位置是 `/var/log/squid/store.log`。

## 调优标签

你可以选择以下标签：

- `request_header_max`。决定 Squid 接受的最大头部大小。默认值是 10 KB。

- `request_body_max`。限制可以在正文中发送的数据。默认值为 0 MB。

- `quick_swap_min`, `quick_swap_high`, `quick_swap_pct`。Squid 可以配置以限制传输。这些变量设置如下：
  - `quick_swap_min`。（单位为 KB）如果小于给定值，传输将继续。默认值是 16 KB。
  - `quick_swap_high`。（单位为 KB）如果大于给定值，传输将终止。默认值是 16 KB。
  - `quick_swap_pct`。（百分比）如果已经传输了指定的百分比，传输将继续。默认值是 95%。

- `negative_ttl`。当 Squid 尝试获取客户端请求的数据，但得到负响应（如 404 Not Found），该响应将缓存指定的时间。你需要指定一个值和一个时间单位（如秒、分钟或小时）。默认值为 5 分钟。

- `positive_dns_ttl`。Squid 缓存 DNS 响应。此标签决定了成功的 DNS 请求存储多久。默认值为 6 小时。

- `negative_dns_ttl`。此选项指定了负（失败）DNS 请求的缓存时间。默认值为 1 分钟。

## 错误标签 (Error Tags)

你可以设置以下标签：

- `err_html_text`。定义了向客户端显示的错误消息中应包含的文本。你可以使用 HTML 对文本进行格式化。为了确保显示这些文本，必须在 `/usr/share/squid/errors` 下的错误文件中希望出现该文本的地方包含变量 `%L`。
- `error_directory`。错误页的所在目录。默认值为 `/usr/share/squid/errors`。可以在 `/usr/share/doc/packages/squid/` 的相应目录下找到模板文件。

![](img/ebd0b66532100449f2a48e48fa2ec8ce_274_0.png)

权威的 Squid 文档是配置文件 `/etc/squid/squid.conf`。可以在 http://wiki.squid-cache.org/ 找到更多文档。在 http://wiki.visolve.com 你可以找到过旧版本 2.4 的文档，以及下一个主要版本 Squid 3.0 的文档，在写作时（即 2006 年），该版本处于早期测试阶段。

SLES 10 包含的 Squid 版本是 2.5。

## 控制 Squid 的访问 (Control Access to Squid)

在最简单的设置中，任何可以访问代理监听的网络接口的人都可以使用 Squid 代理访问网站。然而，Squid 也可以用于控制对网站的访问。

Squid 提供了强大的访问管理功能，允许你根据以下参数允许或拒绝对代理的访问，并控制由谁访问哪些网站：

- 客户端或 Web 服务器的 IP/网络地址
- 星期和时间
- 内容类型 (Content Type)
- 传输协议 (Transfer Protocol)

Squid 的访问管理基于 `squid.conf` 文件中的两种不同标签类型：

- `acl` (访问控制列表)。定义与传入 HTTP 请求匹配的条件。
- `http_access`。当指定的 `acl` 条件匹配时，决定允许还是拒绝访问。

假设你的 `squid.conf` 文件中有以下几行：

```
acl src 0.0.0.0/0.0.0.0

acl allowed_clients src 10.0.0.0/0

http_access allow allowed_clients

http_access deny all
```
