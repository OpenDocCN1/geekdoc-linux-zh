
你可以进一步指定保存在磁盘或内存中的对象的最小和最大大小。在磁盘上，使用 `maximum_object_size` 和 `minimum_object_size`。默认最大值为 4 KB。默认最小值设置为 0，表示没有最小值。对于内存，使用 `maximum_object_size_in_memory` 和 `minimum_object_size_in_memory`。

`cache_swap_low` 和 `cache_swap_high` 选项允许你设置替换缓存中对象的阈值。

要指定缓存对象的位置，使用 `cache_dir` 选项。在这里，你指定用于缓存的目录。

## 管理设置

你的 Squid 缓存管理员的电子邮件地址在 `cache_mgr` 选项中指定。

如果你以 root 用户身份运行 Squid，那么 Squid 会将用户和组 ID 从 `root` 更改为 `nobody`。组 ID 将更改为 `nogroup`。这是为了保护 root 用户访问权限。如果你以非 root 用户身份运行 Squid，Squid 将保留该原始用户作为其用户 ID。如果在以 root 用户身份运行 Squid 时，你想指定除了 `nobody` 之外的其他用户，你可以使用 `cache_effective_user` 更改用户 ID，并使用 `cache_effective_group` 更改组。

你还可以指定一个在错误消息中显示的特殊主机名。使用 `visible_hostname` 设置名称。

## 日志

Squid 维护几个详细记录访问、缓存性能和错误消息的日志。

- `access.log` 保存发送到代理的请求。
- `cache.log` 保存 Squid 服务器消息，如错误和启动消息。
- `store.log` 保存关于 Squid 缓存的信息，如添加或移除的对象。

你可以使用缓存管理器（`cachemgr.cgi`）来管理缓存并查看缓存管理器运行时的统计数据。要运行缓存管理器，请使用浏览器执行 `cachemgr.cgi` 脚本（此脚本应放置在 Web 服务器的 `cgi-bin` 目录中）。

## Web 服务器加速：反向代理缓存

虽然 Squid 缓存可以增强客户端对 Web 服务器的访问，但 Squid 也可以减少 Web 服务器的负载。被请求压垮的 Web 服务器可以将其可缓存页面迁移到作为某种替代站点的 Squid 代理服务器上，处理这些页面的请求。实际上，Web 服务器变得更快了。这种缓存被称为反向代理缓存，它关注的是服务器而不是客户端。反向代理缓存会拦截发往服务器的请求，并处理那些针对其缓存页面的请求。只有针对未缓存页面的请求才会被转发到原始 Web 服务器。

要配置反向代理缓存，请使用带有 `accel` 选项的 `http_port` 指令（对于 Squid 2.4 及更早版本，请使用 `httpd_accel` 指令）。要为加速器指定特定位置，请使用 `defaultsite`（这取代了 Squid 2.4 及更早版本中使用的 `httpd_accel_host`）。

```
http_port 3128

http_port 192.168.0.25:80 accel defaultsite=rabbit.mytrek.com
```

如果您的 Squid 代理服务器和 Web 服务器运行在同一台主机上，您需要指定 Web 服务器使用的端口。该端口不能与 Squid 使用的端口相同。使用带有 `port` 选项的 `cache_peer` 指令来指定服务器端口。然后使用带有 `originserver` 选项的 `cache_peer` 指令指定 Web 服务器的地址。在以下示例中，Web 服务器使用端口 80，而 Squid 使用端口 3128：

```
http_port 3128 # Squid 代理的端口

cache_peer port 80

cache_peer originserver localhost # Web 服务器的 IP 地址
```

在 Squid 2.6 中，透明缓存直接作为 `http_port` 选项 `transparent` 得到支持。

```
http_port 3218 transparent
```

要指定使用 host 指令（虚拟主机），请使用 `vhost` 选项。这取代了早期版本中使用的 `httpd_accel_uses_host_header` 指令。对于虚拟 IP 主机，请使用 `vport`。

```
http_port vhost
```
