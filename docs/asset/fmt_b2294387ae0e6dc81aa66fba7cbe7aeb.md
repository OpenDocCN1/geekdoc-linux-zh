
`cache_peer <hostname> <type> <proxy-port> <icp-port>` 这里，将代理项输入 "parent"，例如，或使用代理地址作为 `<hostname>`，输入名称和 ID，并在 `<type>` 输入 `parent`。对于 `<proxy-port>`，输入代理运营商为浏览器指定的端口号，通常为 8080。如果父代理的 ICP 端口未知且与供应商无关，将 `<icp-port>` 设置为 7 或 0。此外，在端口号之后指定 `default` 和 `no-query` 以严格禁止使用 ICP 协议。这样，Squid 对于供应商代理的行为就像普通浏览器一样。

`cache_mem 8 MB` 此条目定义了 Squid 可用于缓存的内存量。默认为 8 MB。

`cache_dir ufs /var/cache/squid/ 100 256` `cache_dir` 条目定义了存储所有对象在磁盘上的目录。数字位于末尾表示以 MB 为单位要使用的最大磁盘空间，以及第一、二级目录的数量。`ufs` 参数应保持不变。默认值是在 `/var/cache/squid` 目录下占用 100 MB 磁盘空间，并在其中创建 16 个子目录，每个子目录包含 256 个目录。在指定磁盘空间时，请留出足够的预留磁盘空间。这里取可用磁盘空间50%到80%之间的取值是最合理的。目录的最后两个数字应谨慎增加，因为目录过多也会导致性能问题。如果你有多个磁盘共享缓存，请输入几行 `cache_dir` 配置。

- `cache_log /var/log/squid/access.log` 日志消息路径
- `cache_log /var/log/squid/cache.log` 日志消息路径
- `cache_store_log /var/log/squid/store.log` 日志消息路径

这三个条目指定了 Squid 存储所有操作的路径。通常情况下，这里不做任何更改。如果 Squid 面临沉重的使用负担，将缓存和日志文件分布在多个磁盘上可能是有意义的。

- `emulate_httpd_log off` 如果该条目设置为 on，则获取可读的日志文件。某些评估程序无法解释此。
- `client_netmask 255.255.255.255` 通过此条目对日志文件中记录的 IP 地址进行掩码以隐藏客户端身份。如果你输入 255.255.255.0，IP 地址的最后一位将被设置为零。
- `ftp_user Squid@` 通过此设置 Squid 在进行匿名 FTP 登录时应使用的密码。然而，在这里指定一个有效的电子邮件地址是有意义的，因为某些 FTP 服务器会检查这些地址的有效性。
- `cache_mgr webmaster` 当 Squid 意外崩溃时，发送消息的电子邮件地址。默认值是 webmaster。
- `logfile_rotate 0` 如果你运行 `squid -k rotate`，Squid 可以保护日志文件。在此过程中文件将被枚举，在达到指定值后，该点最旧的文件将被覆盖。这里的值为 0，是因为在 SuSE Linux 中，日志文件的归档和删除是由配置文件 `/etc/logrotate/squid` 中的 cron 任务完成的。
- `append_domain <domain>` 通过 `append_domain`，在未提供域名时指定自动附加的域名。通常在此处输入你自己的域名，因此在浏览器中输入 www 即可访问自己的 Web 服务器。
- `forwarded_for_on` 如果你将条目设置为 off，Squid 将从 HTTP 请求中移除客户端的 IP 地址和系统名称。
- `negative_tl 5 minutes; negative_ttl 5 minutes` 你不需要更改这些值。但是，如果你有拨号连接，互联网有时可能无法访问。此时 Squid 会记录失败的请求并拒绝发布新请求，尽管互联网连接已经重新建立。在这种情况下，将分钟改为秒，然后在浏览器中点击重新加载（Reload），几秒钟后拨号过程应该就会重新启动。
- `never_direct allow <acl_name>` 为了防止 Squid 直接从互联网获取请求，请使用上述命令强制连接到另一个代理。这必须之前在 `cache_peer` 中输入过。如果指定的 `<acl_name>` 为所有访问控制列表（即 all），则强制所有请求直接转发到父代理。这可能是必要的，例如当你正在使用一个严格规定使用其代理或拒绝其防火墙访问互联网的供应商时。

# 访问控制选项

Squid 提供了一套控制代理访问的智能系统。通过实现 ACL，可以对其进行简单且全面的配置。这涉及一组按顺序处理的规则列表。ACL 必须在使用之前进行定义。某些默认 ACL（如 `all` 和 `localhost`）已经存在。在定义 ACL 后，对其进行实现，例如结合 `http_access` 使用使用。

- `acl <acl_name> <type> <data>` 定义一个 ACL 至少需要三个规范。名称 `<acl_name>` 可以任意选择。对于 `<type>`，请从 `/etc/squid/squid.conf` 文件中 `ACCESS CONTROLS` 部分的各种不同选项中选择。`<data>` 的规范取决于具体的 ACL 类型，也可以从文件中读取，例如通过主机名、IP 地址或 URL。以下是简单的示例：

```
acl mysurfers srcdomain .my-domain.com
acl teachers src 192.168.1.0/255.255.255.0
```

`acl students src 192.168.7.0-192.168.9.0/255.255.255.0`

`acl lunch time MTWHF 12:00-15:00`

- `http_access allow <acl_name>` `http_access` 定义了谁被允许使用代理以及可以在互联网上访问什么。为此，必须给出 ACL。`localhost` 和 `all` 在上面已经定义过，可以通过 `deny` 或 `allow` 拒绝或允许访问。可以创建一个包含任意数量 `http_access` 条目的列表，从上到下进行处理，并根据先发生的情况，相应的 URL 可能会被允许或拒绝访问。最后一个条目始终应该是 `http_access deny all`。在接下来的示例中，`localhost` 可以访问所有内容，而所有其他主机都被拒绝访问。

```
http_access allow localhost
http_access deny all
```

- 指向互联网的设备：`FW_DEV_EXT="eth1"`
- 指向内部网络的设备：`FW_DEV_INT="eth0"`

在被从不可信网络访问为互联网的防火墙上，设置端口和服务（参见 `/etc/exports`）。在例例中，仅向外部提供 Web 服务：

`FW_SERVICES_EXT_TCP="www"`

在从安全网络访问的防火墙上定义端口或服务（参见 `/etc/exports`），并同时包含 TCP 和 UDP 服务：

`FW_SERVICES_INT_TCP="domain 3128"`

`FW_SERVICES_INT_UDP="domain"`

这允许访问 Web 服务和 Squid（其默认端口为 3128）。

之前指定的 "domain" 服务代表 DNS。该服务通常被使用。如果不需要，只需简单地从上述条目中将其移除，并将以下选项设置为 no：

`FW_SERVICE_DNS="yes"`

最重要的选项是是第 15 个：

```
#
# 15.)
# 哪些对服务的访问应该重定向到防火墙机器
# 本地端口
# 这可以用于强制所有内部用户通过你的
# squid 代理上网，或者透明地将 Web 流量重定向到
# 安全 Web 服务器。
# 选择：留空或使用以下解释的重定向规则语法，
# 之间用空格分隔。
# 一个重定向规则由 1) 源 IP/网，
# 2) 目的 IP/网， 3) 原始目的端口
# 4) 重定向流量的本地端口，之间用冒号分隔：
# 例如 "10.0.0.0/8,0/0,3128 0/0,172.20.1.1,8080"
#
```

# 文件 56：Firewallkonfiguration 的第 15 选项

上面的注释显示了需要遵循的语法。首先，是访问代理防火墙的“内部网络”的 IP 地址和子掩码。其次，是这些客户端“发送”请求的 IP 地址和子掩码。对于 Web 浏览器，请指定网络 0/0，这是一个通配符，意味着“到任何地方”。之后，输入这些请求发送的“原始”端口，最后是所有这些请求被“重定向”的端口。Squid 支持比 HTTP 更多的协议，将来自其他端口的请求重定向到我们的代理，例如 FTP（端口 21）、HTTPS 或 SSL（端口 443）。示例使用了默认端口 3128。如果有更多网络或服务需要添加，只需在相应的条目中用单个空格分隔即可。

`FW_REDIRECT_TCP="192.168.0.0/16,0/80,3128 192.168.0.0/16,0,21328"`
