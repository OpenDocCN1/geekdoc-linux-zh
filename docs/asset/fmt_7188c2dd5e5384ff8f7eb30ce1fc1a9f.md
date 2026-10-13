
如果管理员认为基础 HTTP 认证不够安全，他可能希望使用 MD5 摘要认证（Digest Authentication）。当使用 MD5 算法处理文件时，会生成一个 32 字符的数字指纹。产生两个具有相同指纹的消息在计算上是不可行的（概率约为 3.40e38 分之一之 1）。尽管 MD5 通常被用于验证文件完整性，但 Apache 内置了比基础 HTTP 认证更安全的替代方案。在使用 MD5 摘要认证时，用户名和密码的传输是加密的。

可以使用 `htdigest` 工具为受保护的 Web 目录添加 MD5 认证，以提供比基础 HTTP 认证更高水平的安全性。`htdigest` 的工作方式类似于 `htpasswd`。要为账户 `joeuser` 添加 MD5 支持，第一个管理员需要使用 `htdigest` 配合 `-c` 选项创建一个新的摘要数据库。

```
htdigest -c .htdigest "Joe User" joeuser
```

Joe User 输入了所谓的“域（realm）”。该域与在 `.htaccess` 文件中 `AuthName` 字段输入的内容相同。接下来，应该追加 `.htaccess` 配置。需要在 `:htdigest` 文件所在的位置添加 `AuthDigestFile` 字段：

```
AuthDigestFile=/home/joeuser/public_html/.htdigest
```

最后，需要更改 `.htaccess` 文件中的认证选项 `AuthType` 以使用基于摘要的认证。将如下：

`AuthType Basic`

更改为：

`AuthType Digest`

现在，将使用 MD5 摘要认证代替基础 HTTP 认证，Web 客户端与服务器之间的流量将通过加密。

# chroot Web 环境

管理员可能希望为 Web 目录设置一个 `chroot` 环境。如果管理员计划让用户上传并运行 CGI，这一点尤为重要。运行在 `chroot` 目录内部的服务器无法看到该目录树之外的任何内容。在 `chroot` 环境下，如果黑客成功攻入 `chroot` Web 服务器或 CGI，造成的损害将仅限于 `chroot` 目录树内的文件。由于这个原因，`chroot` 环境通常被称为“监狱（jail）”。

# 创建 chroot Web 环境

要创建 `chroot` 环境，管理员必须先创建一个所有 `chroot` 目录结构的用户，并为该目录结构创建一个组。然后，管理员必须创建 Web 服务器的根目录，并更改该目录的权限和所有者。如果 Web 服务器 `httpd` 将位于 `/cage` 目录，应执行以下命令：

```
# mkdir /cage
# chown -R cageowner:cagegroup /cage
# chmod -R 775 /cage
```

接下来，管理员必须以 `cageowner` 身份登录并在 `/cage` 下创建目录结构。使用 `chroot` 会切断与文件系统其余部分的通信；因此，必须将包含基础系统命令（`ls`, `mv`, `cp` 等）和至少一个 shell 的 `/bin` 目录复制到 `/cage` 目录。如果要运行 CGI，还必须将 Perl 及其支持库也复制到 `chroot` 目录。

最后，管理员需要使用 `chroot` 来欺骗 Web 服务器 `httpd`，让它认为 `/home/httpd` 是根目录。以下命令将以 root 身份执行：

```
# /usr/sbin/chroot /cage httpd
```

现在，将有一个功能性的 `chroot` 环境封装着 Web 服务器，在 Web 服务器安全性遭到破坏时保护系统的部分免受攻击。

# Squid

Squid 是一个免费、高性能的 HTTP 代理服务器，用于缓存互联网数据。它允许管理员在类 Unix 上提供高水平的互联网安全。Squid 可用于传递数据包，或用于过滤和控制互联网访问。Squid 是一个灵活的代理服务器，支持许多协议，如 FTP、Gopher、WAIS 和 SSL。然而，所有对 Squid 请求的响应必须是 HTTP 格式。

美国科学基金会（NSF）领导代码开发并为 Squid 项目提供所有资金。尽管 Squid 是在 Digital Unixget上开发的，但它设计用于运行在任何类 Unix 设备上。

# 代理服务器

代理被用作和互联网之间的内部防御。代理限制了对数据的访问，并隐藏了互联网服务器提供的信息的位置。代理服务器接收用户的互联网请求，并在传递给互联网服务器之前确定请求的有效性。Squid 然后缓存返回的数据，这使其与防火墙代理服务器区分开来。当第二次收到对相同数据的请求或接收到多个请求时，Squid 将提供数据的缓存副本，而不是检索它。

# Squid-cache

美国科学基金会（NSF）领导代码开发并为 Squid 项目提供所有资金。尽管 Squid 是在 Digital Unixget上开发的，但它设计用于运行在任何类 Unix 设备上。

# 代理服务器

代理被用用户和互联网之间的内部防御。代理限制了对数据的访问，并隐藏了互联网服务器提供的信息的位置。代理服务器接收来自用户的互联网请求，并在传递给互联网服务器之前确定请求的有效性。Squid 然后缓存返回的数据，这使其与防火墙代理区分开来。当第二次收到对相同数据的请求或接收到多个请求时，Squid 将提供数据的缓存副本，而不是检索它。

# 配置 Squid

美国科学基金会（NSF）领导代码开发并为 Squid 项目提供所有资金。尽管 Squid 是在 Digital Unix 上开发的，但它设计用于运行在任何类 Unix 设备上。

# 浏览器配置

Squid 默认拒绝所有浏览器，第一个配置步骤是允许浏览器连接。这在 `squid.conf` 文件的访问控制部分完成。接下来，每个网络主机上的浏览器必须配置为使用 Squid 进行互联网请求。

# 设置 HTTP 端口

Squid 默认在端口 3128 上接受 HTTP 请求。然而，80 是最常用的。使用 `http_port` 标签更改默认端口。

# 管理员邮箱

Squid 允许指定管理员的电子邮件。如果 Squid 崩溃，服务器管理员将收到电子邮件。使用 `cache_mgr` 标签指定管理员的邮箱地址。

## 访问控制

通过访问控制部分，管理员可以控制 Squid 响应的协议。该部分还允许管理员设置客户端可以使用协议、用户验证以及对等访问（缓存节点允许其他代理服务器与 Squid 通信）。以下是指定缓存对等和 HTTP 访问的访问控制部分示例：

```
#setting a cache peer
#the syntax for the cache peer access tag is
#cache_peer_access cache-host [allow/deny] [access-list-name]
cache_peer_access Megatron allow manager
cache_peer_access Megatron allow SSL_ports
#http access configuration:
http_access allow administrator localhost
http_access deny !Safe_ports
http_access allow CONNECT SSL_ports
http_access deny all
```

## 使用 Squid 实现安全

Squid 的内部安全通过 `squid.conf` 配置文件的访问控制部分进行操作。在这里，用户可以按域名、IP 地址和用户验证方法阻止访问。通过用户验证和互联网拦截，Squid 可以为服务器提供安全保护。然而，代理缓存服务器从不单独使用，而是与防火墙等其他安全软件配合使用。因此，大多数 Squid 的配置只需要最少量的内部实现。

## 防火墙访问控制

Squid 可以用于防火墙内部或外部。当 Squid 位于防火墙内部时，它被认为是一个信任主机，允许连接到服务器资源。用户请求从 Squid 传递到防火墙，响应从防火墙传回 Squid；它将防火墙视为代理服务器。在图 5.11 中，防火墙为 Squid 提供安全保护。然而，Squid 能够通过其访问控制功能为自己提供安全。

![](img/6942796f6e22033d0f94b498c190e5cc_206_0.png)

**图 5.11** 带有防火墙安全的 Squid。

## 第 5 章

| 主机 | 互联网服务器 | 三次握手协议 | 代理服务器 | 互联网 |
| :--- | :--- | :--- | :--- | :--- |

图 5.12 没有防火墙安全的 Squid。

当防火将将传递给代理服务器时，该特性被称为“交接”（hand-off）。如果防火墙不支持交接，内部客户端很难连接到外部世界。如果将 Squid 放在防火墙外部，用户请求将从防火侧传递到 Squid；此过程需要防火墙向 Squid 发送 HTTP 请求。如果防火墙不支持交接，请求将不会被传递。在图 5.12 中，防火墙没有为 Squid 提供安全。
