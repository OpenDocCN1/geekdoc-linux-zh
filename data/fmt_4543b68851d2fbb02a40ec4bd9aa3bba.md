
> 注意
列表 19.1 中的每个属性在下文中都得到了解释。然而，请注意某些属性通过将它们设置为空值默认被注释掉了。

`xinetd.conf` 默认集合中的前两个选项是 `enabled`（启用）和 `disabled`（禁用）。启用和禁用 xinetd 服务应该在 `/etc/xinetd.d/` 中的单独服务服务文件中完成，并将 `disable` 属性设置为 `yes` 或 `no`，如下一节“单独服务服务文件”所示。在 `xinetd.conf` 中使用 `enabled` 和 `disabled` 选项仅建议用于临时情况，如测试，或者你认为系统已被攻破并关闭所有不必要的服务。要使用其中一个或两个属性，请取消其中一个或两个的注释。

`enabled` 选项可以允许连接的服务。带有此选项的服务仍然需要在 `/etc/xinetd.d/` 中的单独服务文件中启用，方法是将 `disable` 属性设置为 `no` 并确保 `flags` 属性中没有列出 `DISABLE` 标记。如果没有设置 `disabled` 选项，则 `enabled` 列表中的 xinetd 服务被允许连接。

如果设置了 `disabled` 选项，只有 `enabled` 列表中的 xinetd 服务接受连接，除非它们也在 `disabled` 列表中。所有带有 `disabled` 选项列出的服务都不允许连接。

这两个属性都接受用空格分隔的服务 ID 列表。对于这两个选项，都必须使用服务 ID 而不是服务名称。在 `/etc/xinetd.d/` 中的单独服务文件中，`id` 属性将服务设置为唯一标识符。如果没有提供 ID，则 ID 默认为服务名称。大多数服务 ID 与服务相同。

名称，但在配合 `enabled` 和 `disabled` 属性使用时，请务必双检。

默认设置中的下一组属性控制日志。它们如下：

- `log_type`: 设置日志服务。如果设置为 `SYSLOG <facility>`，则使用指定的 syslog 设施。如果设置为 `FILE <file>`，则日志将写入指定的文件。
- `log_on_failure`: 设置日志服务。如果设置为 `SYSLOG <facility>`，则使用指定的 syslog 设施。如果设置为 `FILE <file>`，则日志将写入指定的文件。
- `log_on_success`: 设置当 xinetd 服务启动或其之一执行时记录的消息类型。请参阅 `xinetd.conf` 管理器以获取完整的值列表。在默认 `xinetd.conf` 设置下，会记录远程主机地址和进程 ID。

下一组属性设置了访问控制的默认值。详情请参阅本章的“允许 xinetd 连接”节。

接下来的三个属性是地址和网络默认值。`bind` 和 `mind` 属性已列出但默认被注释。这些属性的用法如下：

- `bind`: 要仅在特定接口上监听连接，请将此值设置为接口的 IP 地址。
- `mdns`: 设置为 `yes` 以启用 mdns 注册，该功能目前仅适用于 Mac OS。设置为 `no` 则禁用 mdns 注册。
- `ipv6`: 默认设置为 `yes` 或 `no` 以同时使用 IPv4 和 IPv6。

还列出了三个环境变量属性：

- `passenv`: 默认被注释。如果设置为环境变量列表，则在请求并允许连接时，这些值将传递给由 xinetd 启动的服务。如果设置为空值，则除 `env` 属性列出的变量外，不传递任何变量。
- `groups`: 如果设置为 `yes`，服务器将以服务器有效 UID 可访问的组身份运行。如果设置为 `no`，服务器将无法访问任何额外组。如果设置为组列表，则服务器将获得所列组的访问权限。
- `umask`: 为 xinetd 服务设置默认 umask。（umask 可以针对 `/etc/xinetd.d/` 下的单个服务文件中的单独服务进行设置。）

`xinetd.conf` 的最后一行使用了 `include` 属性。它告诉守护进程使用 `/etc/xinetd.d/` 目录中的单个服务文件。

## 单个 xinetd 服务文件

每个 xinetd 服务在 `/etc/xinetd.d/` 目录下都有一个配置文件。例如，列表 19.2 所示的 rsync 的 xinetd 配置文件 `/etc/xinetd.d/rsync`。

# The xinetd Super Server 383

# Listing 19.2 rsync 的 xinetd 配置文件

# default: off
# description: rsync 服务器是 ftp 服务器的良好补充，因为它 \
# 允许 crc 校验等功能。

```
service rsync

{

    disable = yes

    socket_type = stream

    wait = no

    user = root

    server = /usr/bin/rsync

    server_args = -daemon

    log_on_failure += USERID

}
```
