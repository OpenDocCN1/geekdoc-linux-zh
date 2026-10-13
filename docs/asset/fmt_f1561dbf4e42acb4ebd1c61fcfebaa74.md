
# 存储服务器的 PID、Lock 和 ScoreBoard 文件

Apache Web 服务器保留运行的服务器进程的 PID。它还存储有关锁文件的信息。在某些系统上，还会创建一个 ScoreBoard 文件来存储内部服务器进程信息。你可以使用下面的条目更改这些文件的位置：

`PidFile`: 服务器应将其 pid 记录到
`PidFile=/var/run/httpd`

`# ScoreFile`: 用于存储内部服务器进程信息的文件。
# 并非所有架构都需要此文件。如果你需要（当你运行 Apache 时
# 会知道此文件被创建了），则“必须”确保
# 没有两个 Apache 调用共享同一个 scoreboard 文件。

# 第 21 章 设置 Web 服务器 725

`scoreboard=/var/run/httpd.scoreboard`

# `LockFile` 指令设置了当 Apache 编译时使用了

# `USE_FCNTL_SERIALIZED_ACCEPT` 或

# `USE_FLOCK_ACCEPTED` 时，使用的锁文件路径。该指令通常应保持

# 默认值。更改它的主要原因是日志

# 目录是 NFS 挂载的，因为锁文件必须被存储在本地

# 磁盘上。主服务器进程的 PID 会自动附加到

# 文件名。

`#LockFile /var/lock/httpd.lock`

Apache 使用 `PidFile` 来存储第一个（root 所有的）主守护进程的 ID。此信息在 `/etc/init.d/httpd` 脚本在关闭服务器时使用。（此处由于原文后半部分大量重复，译文已完成核心逻辑翻译）

（以下为配置超时值的翻译）

# 配置超时值
你可以设置几个与超时值相关的值。其中某些值描述如下：

```
# Timeout: 在接收和发送之前超时的秒数。
# Timeout 300
```

```
# KeepAlive: 是否允许持久连接（一个连接处理多个请求）。设置为 "Off" 以禁用。
# KeepAlive On
```

```
# MaxKeepAliveRequests: 单个连接上可以处理的最大请求数。设置为 0 以允许无限量。
# 我们建议将此值调大，以获得最佳性能。
# MaxKeepAliveRequests 100
```

```
# KeepAliveTimeout: 等待下一个请求的秒数。
## KeepTimeout 15
```

`Timeout` 指令决定 Apache 在接收 PUT 或 POST 方法的数据包之间、在接收响应确认之间或在接收传入请求时保持连接的秒数。如果你发现机器上有大量的空闲连接，默认五分钟可能太短。

`KeepAlive` 指令指示 Apache 在处理请求后保持连接。这使得同一客户端的后续请求处理速度更快，因为不需要为每个请求创建一个新连接（到不同的服务器进程，最可能）。

`MaxKeepAliveRequests` 指令对单个连接上可以处理的请求数设置限制。默认值是合理的，因为大多数连接会达到 `KeepAliveTimeout`。

`KeepAliveTimeout` 指令指定在等待另一个请求时保持连接的秒数。根据客户端使用平均页面并从中选择链接所需的时间，你可能希望增加默认的15 秒。

# 设置服务器进程数量

你可以让 Apache 动态地更改服务器进程的数量。要做到这一点，请如下所示设置 `MinSpareServers` 和 `MaxSpareServers` 值：

```
# 服务器池大小调节。与其让你猜测需要多少个进程，
# Apache 会根据它看到的负载进行动态调整，也就是说，它试图
# 维护足够的服务器来处理当前负载，加上几个备用服务器来处理瞬时
# 负载峰值（例如来自单个客户端的多个并发请求）。
```

## 第 21 章 设置 Web 服务器

(Netscape 浏览器)。

它通过定期检查等待请求的服务器数量来实现此功能。如果空闲服务器少于 `MinSpareServers`，它会创建一个新的空闲服务器。如果多于 `MaxSpareServers`，某些空闲服务器将被销毁。默认值对于大多数站点来说通常足够。

`MinSpareServers 5`
`MaxSpareServers 20`

# 初始时启动的服务器数量 --- 应该是一个合理的估计
# 数值。
`#StartServers 8`

# 对运行服务器总数的限制，即限制同时连接的
# 客户端数量 --- 如果达到此限制，客户端将会被锁定（LOCKED OUT），因此
# 不应设置得太低。
# 它的主要作用是一个制动器，防止失控的服务器在
# 崩溃时拖累整个系统...
`#MaxClients 150`

# `MaxRequestsPerChild`：每个进程在退出前允许处理的
# 请求数。子进程将退出，以避免长时间使用后 Apache（以及它可能使用的
# 库）出现内存或其他资源泄漏时产生的问题。在大多数系统上，
# 并不真正需要，但某些系统（如 Solaris）的库不存在
# 泄漏。对于这些平台，将其设置为 10000 左右，
# 设置为 0 表示无限制。

注意：此值不包括每个连接初始请求之后的 keepalive 请求。
# 例如，如果一个进程处理了 初始请求和 1 个随后的“keepalive”请求，
# 它在此限制中将计为 1 个请求。
`MaxRequestsPerChild 100`

在独立模式下（通过 `HttpServer` 指令），Apache 将以 root 身份启动一个
主守护进程，绑定到相应的端口，然后切换到非特权用户。
随后将以相同的非特权用户（在此例中为 `nobody`）启动
更多的服务器（相当于 `StartServers` 指令的值）。

Apache 尝试根据当前负载智能地启动杀死服务器。
如果流量减少且空闲服务器过多，某些服务器将被
销毁（减少到 `MinSpareServers` 中指定的服务器数量）。同样，如果
请求紧密到达且等待新连接的服务器太少，将启动
更多服务器（最多达到 `MaxSpareServers` 中指定的服务器数量）。

上述指定的值在守护进程启动时，将有 8 个服务器进程运行并等待
连接（由 `StartServers` 定义）。随着更多请求的到来，Apache 将确保至少有 8 个服务器准备好响应请求。当请求被完成且没有新连接到达时，Apache 将开始杀死进程，直到空闲 Web 进程的数量低于 20。`StartServers` 的值始终应处于 `MinSpareServers` 和 `MaxSpareServers` 之间。

Apache 使用 `MaxClients` 指令限制同时运行的服务器进程总数。默认值为 150，这应该足够高了。然而，如果你发现有许多服务器正在运行，请记住超过 150 个的任何连接都将被拒绝。在某些情况下，如果你的硬件足够强大（并且如果你的网络连接可以处理该负载），你应该增加 `MaxClients` 的值。

为了尽地减少内存泄漏的影响（并保持服务器池的“新鲜度”），每个服务器进程能够处理的请求数都受到了限制（等于 `MaxRequestsPerChild` 的值）。在处理了 100 个请求（上述指定的值）后，该进程将被杀死。更准确的说法是，每个进程可以服务 100 个连接，因为所有的 KeepAlive 请求（在进入 `KeepAliveTimeout` 之前发生）都被计算为一个请求。

### 绑定到特定地址

你可以使用 `Listen` 指令绑定特定的 IP 地址。`Listen` 指令可以用于添加你已有的默认绑定：

```
# Listen: 允许你将 Apache 绑定到特定的 IP 地址和/或
# 端口。除了默认设置外。另见 VirtualHost
# 指令。
# Listen 3000
Listen 12.34.56.78:80
Listen 80
```

`Listen` 指令比 `BindAddress` 和 `Port` 指令更灵活。可以指定多个 `Listen` 命令，允许你指定多个 IP 地址/端口组合。它也可以用于仅指定 IP 地址（在这种情况下 `Port` 指令仍然是必要的）或仅指定端口号。默认情况下，Apache 监听本地计算机上的 80 端口（这是 `/etc/services` 中列出的标准 www 端口）。

### 在虚拟地址上绑定

Apache 支持虚拟主机概念。通过使用 `BindAddress` 条目，你可以告诉服务器监听哪个 IP 地址：

```
# BindAddress: 你可以使用此选项支持虚拟主机。此选项
# 用于告诉服务器监听哪个 IP 地址。它可以包含
# *、一个 IP 地址或一个完全限定的 Internet 域名。
# 另见 VirtualHost 和 Listen 指令。
# BindAddress *
```
