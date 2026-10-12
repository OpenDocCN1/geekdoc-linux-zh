
上下文：服务器配置，虚拟主机

## 谨慎使用 `<Location>`

> 警告 请谨慎使用此功能强大的容器。不要用它来替代 `<Directory>` 容器：当多个 URI 指向文件系统中的同一位置时，客户端可能通过使用此此容器未指定的 URI 来绕过预期的访问控制。

## `<LocationMatch>` 将指令应用于由正则表达式指定的 URI。

`<LocationMatch regexp> ... </LocationMatch>`

其中 `regexp` 是匹配一个或多个 URI 的正则表达式。该容器的工作方式与 `<Location>` 相同，但它适用于任何匹配 `regexp` 的 URI。

上下文：服务器配置，虚拟主机

## `<VirtualHost>` 将指令应用于指定的虚拟主机。

`<VirtualHost addr[:port]> [addr[:port]] ... </VirtualHost>`

其中 `addr` 是虚拟主机的 IP 地址（或 FQDN，尽管不建议这样做，`*` 表示所有地址），而 `port` 是 Apache 为该虚拟主机监听的端口。此指令不控制 Apache 监听的地址和端口；请使用 `Listen` 指令（第 925 页）实现该目的。此容器包含 Apache 应用于虚拟主机的命令。欲需更多信息，请参阅第 936 页的 `NameVirtualHost` 和第 953 页的 `Virtual Hosts`。

上下文：服务器配置

## 指令 II：高级指令

本节讨论了您在获得一些 Apache 经验后可能想要使用的配置指令。

### 控制进程的指令

- `MaxClients` 指定子进程的最大数量。

  `MaxClients num`

  其中 `num` 是 Apache 一时运行的子进程（服务器）的最大数量，包括空闲进程和处理请求的进程。当达到 `num` 个进程且没有空闲进程时，Apache 会发出连接错误；它不会启动新的子进程。

  上下文：服务器配置
  默认值：256
  Fedora/RHEL: 256

- `MaxRequestsPerChild` 指定子进程可以服务的最大请求数。

  `MaxRequestsPerChild num`

  其中 `num` 是一个子进程（服务器）在其生命周期内可以服务的最大请求数。子进程处理完请求后，它将不再处理任何其他请求，并在处理完当前请求后销毁。Apache 可以启动另一个子进程来替换销毁的进程。额外的请求将由服务器池中的其他进程处理。

  将 `num` 设置为 0 则不对子进程可处理的请求数设置限制，`MinSpareServers` 的影响除外。通过限制进程的寿命，此指令可以防止内存泄漏消耗过多系统内存。然而，将 `MaxRequestsPerChild` 设置为过小的值会导致 Apache 不断创建新服务器，从而损害性能。

  上下文：服务器配置
  默认值：10000
  Fedora/RHEL: 4000

- `MaxSpareServers` 指定空闲进程的最大数量。

  `MaxSpareServers num`

  其中 `num` 是 Apache 保持运行以处理传入请求的空闲进程（服务器）的最大数量。不要将此数字设置得太高，因为每个进程都会消耗系统资源。

  上下文：服务器配置
  默认值：10
  Fedora/RHEL: 20

- `MinSpareServers` 指定空闲进程的最小数量。

  `MinSpareServers num`

  其中 `num` 是 Apache 保持运行以处理传入请求的空闲进程（服务器）的最小数量。更多的空闲进程占用更多的计算机资源；仅对繁忙站点增加此值。

  上下文：服务器配置
  默认值：5
  Fedora/RHEL: 5

## `NameVirtualHost`

指定基于名称（按主机名）的虚拟机的地址和端口。
`NameVirtualHost addr[:port]`

其中 `addr` 是 Apache 用于提供基于名称的虚拟服务的 IP 地址（或 FQDN，尽管不建议这样做），`port` 是 Apache 为该虚拟主机监听的端口。将 `addr` 指定为 `*`，可使服务器在所有接口上作为基于名称的虚拟主机处理请求。

此指令不控制 Apache 监听的地址和端口；请使用 `List` 指令（第 925 页）实现该目的。欲需更多信息，请参阅第 934 页的 `<VirtualHost>` 和第 953 页的 `Virtual Hosts`。

上下文：服务器配置
默认值：none
Fedora/RHEL: none

## `StartServers` 指定 Apache 启动时启动的子数量。

`StartServers num`

其中 `num` 是 Apache 启动时的子进程数量。此值仅在 Apache 启动时有意义；`MinSpareServers` 和 `MaxSpareServers` 控制的是运行时的空闲进程数量。

上下文：服务器配置
默认值：5
Fedora/RHEL: 8

## 网络指令

### `HostnameLookups`

指定 Apache 是否在日志中记录客户端的主机名或 IP 地址。

`HostnameLookups On | Off | Double`

`On`：通过反向解析（第 856 页）确定客户端的主机名，用于日志记录。

`Off`：记录客户端的 IP 地址。

`Double`：为了提供更高的安全性，对客户端进行反向解析（第 856 页）以确定其主机名，并执行正向 DNS 查询以验证 IP 地址。如果无法验证 IP 地址则拒绝访问。

上下文：服务器配置，虚拟主机，目录
默认值：Off
Fedora/RHEL: Off

提示 谨慎使用 `On` 和 `Double` ：在繁忙系统上可能会消耗大量资源。可以使用程序作为 `logresolve` 进行离线反向解析。

如果您离线执行主机解析，将面临名称可能更改的风险；您通常希望获得请求发生时的名称。为了减少这个问题，请在写入日志后尽快执行主机解析。

`Timeout` 指定 Apache 等待网络操作完成的时间。

`Timeout num`

其中 `num` 是 Apache 等待网络操作完成的秒数。您通常可以将其设置为较低的值；对于繁忙服务器来说，五分钟太长了。Apache 默认较低是因为代码中某些地方在发送数据时没有重置计时器。

上下文：服务器配置
默认值：300
Fedora/RHEL: 60

`UseCanonicalName` 指定服务器识别身份的方法。

`UseCanonicalName On | Off | DNS`

`On`：Apache 使用 `ServerName` 指令（第 928 页）的值作为其身份。
`Off`：Apache 使用传入请求的名称和端口作为其身份。
`DNS`：Apache 对传入请求的 IP 地址进行 DNS 反向解析（第 856 页），并使用结果作为其身份。很少使用。

当服务器具有多个名称并需要执行重定向时，此指令非常重要。Fedora/RHEL 将此指令设置为 `Off`，因为 `ServerName` 指令（第 928 页）被注释掉了。一旦您设置了 `ServerName`，请将 `UseCanonicalName` 改为 `On`。有关重定向和此指令的讨论，请参阅第 951 页。

上下文：服务器配置，虚拟主机，目录
默认值：Off
Fedora/RHEL: Off

# 日志指令

`ErrorLog` 指定 Apache 发送错误消息的位置。

```
ErrorLog filename | syslog[:facility]]
```

其中 `filename` 指定了相对于 `ServerRoot`（第 941 页）的文件名，Apache 将其向该文件发送错误消息。`syslog` 关键字指定 Apache 将错误发送到 `syslog`（第 623 页）；`facility` 指定使用哪个 `syslogd` 设施。默认设施为 `local`。

上下文：服务器配置，虚拟主机
默认值：logs/error_log
Fedora/RHEL：logs/error_log

`LogLevel` 指定 Apache 记录的错误消息级别。

```
LogLevel level
```

其中 `level` 指定 Apache 记录该级别及更高级别（更紧急）的错误。请从以下列表中选择，此列表按紧迫程度递减和详细程度递增的顺序在此处列出：

- `emerg` 系统不可用消息
- `alert` 需要立即采取行动的消息
- `crit` 关键状态消息
- `error` 错误状况消息
- `warn` 非致命性警告消息
- `notice` 正常但重要的消息
- `info` 运行消息和建议
- `debug` 用于查找和解决问题的消息

上下文：服务器配置，虚拟主机
默认值：warn
Fedora/RHEL：warn

# 控制内容的指令

`AddHandler` 在文件名扩展名与内置的 Apache 处理器之间创建映射。

```
AddHandler handler [extension] ...
```
