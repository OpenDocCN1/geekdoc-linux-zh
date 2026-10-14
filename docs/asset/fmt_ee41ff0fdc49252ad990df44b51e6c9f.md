
> 如果你从之前的版本更新，建议编辑新的 `/etc/squid.conf` 并仅对旧文件所作的更改进行应用。如果尝试实现旧的 `squid.conf`，可能会失效。

> **注意**

> 从 2.4 升级到 2.5

# `本地 DNS 服务器`

设置 `本地 DNS 服务器`（例如 `BIND`）是有意义的，即使它没有自己的代理。在 `/etc/resolv.conf` 中输入 `127.0.0.1` 以允许 `Squid` 运行。对于 `localhost`，应在文件中输入 DNS 端口。为了让 `Squid` 工作，应在文件中设置代理，通常为 8080。

在 `/etc/squid/squid.conf` 中的几乎所有的项都以 `#` 符号开头（注释掉）。

# 17.3.5 配置文件

在 `/etc/squid/squid.conf` 中的项定义 `Squid` 可用于缓存的内存量。默认值是 8 MB。

`cache_mem 8 MB` 此项定义了 `Squid` 可用于缓存的内存量。默认值是 8 MB。

所有设置在 `/etc/squid/squid.conf` 中。

# 通用配置选项（选择）

`http_port 3128` 这是 `Squid` 监听客户端请求的端口。默认端口是 3128，但 8080 也很常见。如果需要，可以用空格隔开多个端口号。

`cache_peer <hostname> <type> <proxy-port> <icp-port>` 在这里，例如输入使用你 ISP 的代理。作为 `<hostname>`，输入要使用的代理名称和 IP 地址；作为 `<type>`，输入 `parent`。对于 `<proxy-port>`，输入代理运营商设置的端口号，通常为 8080。将 `<icp-port>` 设置为 7，或者如果代理的 ICP 端口未知且与其使用无关。此外，在端口号之后指定 `default` 和 `no-query` 以禁止使用 ICP 协议。这样 `Squid` 在涉及代理方面的行为就像普通的浏览器一样。

`cache_dir ufs /var/cache/squid/100 16 256` `cache_dir` 定义了在磁盘上存储所有对象的目录。末尾的数字表示以 MB 为单位的最大磁盘空间以及一级、二级目录的数量。`ufs` 参数应保持不变。默认是在 `/var/cache/squid` 目录下占用 100 MB 磁盘空间，并在内部创建 16 个子目录，每个子目录再包含 256 个子目录。在指定使用的磁盘空间时，请留出足够的磁盘保留空间。值从最小到可用磁盘空间的百分之五十到八十之间最为合适。

...这里的意义。目录的最后两个数字增加时应保持谨慎，因为目录过多也会导致性能问题。如果你有多个共享缓存的磁盘，请输入几行 `cache_dir` 配置。

cache_access_log /var/log/squid/access.log

日志消息路径

cache_log /var/log/squid/cache.log

日志消息路径

cache_store_log /var/log/squid/store.log

日志消息路径

这三个条目指定了 `Squid` 记录所有操作的路径。通常情况下，这里不作任何更改。如果 `Squid` 承受着沉重的使用负载，将缓存和日志文件分布在几块磁盘上可能是有意义。

emulate_http_log_off 如果该项设置为 `on`，则获取可读的日志文件。然而，某些评估程序无法解释此设置。

client_netmask 255.255.255.255 通过此项，日志文件中的掩码 IP 地址将隐藏客户端的身份。如果你在这里输入 `255.255.255.0`，则此处 IP 地址的最后一位将设置为零。

ftp_user Squid@ 通过此项，指定 `Squid` 在匿名 FTP 登录时应使用的密码。如果未提供，在这里指定一个有效的电子邮件地址可能是有意义的，因为某些 FTP 服务器可以检查其有效性。

cache_mgr webmaster 如果 `Squid` 意外崩溃，`Squid` 向其发送消息的电子邮箱。默认值是 `webmaster`。

logfile_rotate 0 如果你运行 `-k rotate`，`Squid` 可以对日志文件进行轮转。在此过程中，文件会被编号，并在达到指定值后，最旧的文件将被覆盖。该值通常为 0，因为在 SUSE LINUX 中日志文件的归档和删除是由配置文件 `/etc/logrotate/squid` 中的定时任务（cronjob）完成的。

append_domain <domain> 通过 `append_domain`，在未提供域名时指定要自动追加的域名。通常情况下，在这里输入你自己的域名，在浏览器中输入 `www` 即可访问自己的 Web 服务器。

forwarded_for_on 如果你将该项设置为 `off`，`Squid` 将从 HTTP 请求中移除客户端的 IP 地址和系统名称。

# negative_tt_ttl 5 minutes; negative_dns_ttl 5 minutes

通常，你不需要更改这些值。然而，如果你有一个拨号连接，互联网有时可能无法访问。此时 `Squid` 会记录失败的请求并拒绝发布新请求，尽管互联网连接已经重新建立。在这种情况下，将分钟改为秒，然后在在浏览器中点击“重载（Reload）”后，几秒钟拨号过程应该会重新启动。

negative_direct allow <acl_name> 为了防止 `Squid` 直接从互联网获取请求，请使用上述命令强制连接到另一个代理服务器。这必须在之前已在 `cache_peer` 中输入。如果将所有内容指定为 `<acl_name>`，则强制将请求直接转发到父级代理。这可能是必要的，例如，当你正在使用一个严格规定必须使用其代理服务器或拒绝其防火墙直接访问互联网的提供商时。

# 访问控制选项（Options for Access Controls）

（此处标题）

`Squid` 提供了一个智能系统来控制对代理的访问。通过实现 ACLs（访问控制列表）可以实现这一点，ACLs 可以被轻松且全面地配置。这涉及到带有规则的列表，规则按顺序进行处理。ACL 必须在使用之前进行定义。一些默认的 ACL（如 `all` 和 `localhost`）已经存在。然而，仅仅定义 ACL 并不意味着它被实际应用。这只有在配合 `http_access` 规则时才会发生。

acl <acl_name> <type><data> 定义一个 ACL 至少需要三个规范。名称 `<acl_name>` 可以任意选择。对于 `<type>`，从多种不同的选项中选择，这些选项可以在 `/etc/squid/squid.conf` 文件的 `ACCESS CONTROLS` 部分中找到。`<data>` 的规范取决于具体的 ACL 类型，也可以从文件中读取，例如通过主机名、IP 地址或 URL。以下是一些示例：

```
acl mysurfers srcdomain .my-domain.com
acl teachers src 192.168.1.0/255.255.255.0
acl students src 192.168.7.0-192.168.9.0/255.255.255.0
acl lunch time MWTh 12:00-15:00
```

http_access allow <acl_name>_access 定义了谁被允许使用代理以及谁可以在互联网上访问什么。为了实现这一点，必须提供 ACL。上面已经定义的 `localhost` 和 `all`，可以通过 `deny` 或 `allow` 对其拒绝或允许。可以创建一个包含任意数量 `http_access` 条目的列表，从上到下进行处理，并根据哪个先发生，来决定对相应 URL 的允许或拒绝访问。最后一条条目始终应该是 `http_access deny all`。在接接的示例中，`localhost` 可以自由访问所有内容，而所有其他主机被完全拒绝访问。

```
http_access allow localhost
http_access deny all
```

在另一个示例中，使用这些规则，`teachers` 组始终访问互联网。`students` 组仅在周一至周五的午餐时间访问。

```
http_access allow localhost
http_access allow teachers
http_access allow students lunch
http_access deny all
```

为了可读性，`/etc/squid/squid.conf` 中的 `http_access` 条目应仅在指定位置。

## 17.3.6 透明代理（Transparent Proxy）

（此处标题）

代理的通常工作方式：代理拦截并回答浏览器的请求，因此浏览器接收请求的页面而无需知道它们在哪里。这一过程是透明的，因此得名。

### /etc/squid/squid.conf 中的配置选项

为了让透明代理运行，在 `/etc/squid/squid.conf` 中激活的选项为：

- httpd_accel_host virtual
