
## 存储服务器的 ScoreBoard 文件

在某些系统上，会创建 ScoreBoard 文件来存储内部服务器进程信息。Red Hat Linux 不需要使用 *ScoreBoardFile*，因为通常保存在该文件中的状态信息改为存储在内存中。

## 存储服务器的 PID 文件

Apache Web 服务器会跟踪正在运行的服务器进程的 PID。你可以使用下面描述的条目来更改此文件的位置：

```
#
# PidFile: The file in which the server should record its process
# identification number when it starts.
#
PidFile run/httpd.pid
```

Apache 使用 *PidFile* 来存储第一个（由 root 拥有）的 master daemon 进程的进程 ID。此信息在关闭服务器时由 */etc/init.d/httpd* 脚本使用，也由 server-status 处理程序使用（稍后描述）。

## 配置超时值

你可以设置多个与超时相关的数值。以下代码后的文本中描述了一些这些数值：

```
#
# Timeout: The number of seconds before receives and sends time out.
#
Timeout 300
#
#
# KeepAlive: Whether or not to allow persistent connections (more than
# one request per connection). Set to "Off" to deactivate.
#
KeepAlive Off
#
#
# MaxKeepAliveRequests: The maximum number of requests to allow
# during a persistent connection. Set to 0 to allow unlimited amount.
# We recommend you leave this number high, for maximum performance.
#
MaxKeepAliveRequests 100
#
#
# KeepAliveTimeout: Number of seconds to wait for the next request from
# the same client on the same connection.
#
KeepAliveTimeout 15
```

Timeout 指令决定了 Apache 在接收 PUT 或 POST HTTP 请求方法的数据包之间、在发送响应的确认之间，或在接收传入请求时保持连接打开的秒数。默认的五分钟（300 秒）如果发现机器上存在过多的打开的空闲连接，可以 certainly 降低。

KeepAlive 指令指示 Apache 在处理完请求后保持连接打开一段时间。这使得来自同一客户端的后续请求可以更快地处理，因为每个请求都不需要创建新的连接（很可能连接到不同的服务器进程）。

MaxKeepAliveRequests 指令设置了可以用一个打开的连接处理的请求数量的限制。默认值是合理的，因为大多数连接会在达到 MaxKeepAliveRequests 之前先达到 KeepAliveTimeout。

KeepAliveTimeout 指令指定在等待另一个请求时保持连接的秒数。你可能希望根据客户端浏览平均页面并从中选择链接所需的时间来增加默认值（15 秒）。

## 设置服务器进程数量

为了让 Apache 能够动态更改正在运行的服务器进程数量以满足服务器需求，设置了多个参数来指示：

- 应启动多少个服务器进程（StartServers）
- 保持空闲的服务器进程的最小数量（MinSpareServers）
- 保持空闲的服务器进程的最大数量（MaxSpareServers）
- 允许启动的服务器进程的最大数量（MaxClients）
- 一个进程可以服务的请求的最大数量（MaxRequestsPerChild）

在 Apache 2.0 中的多处理模块（MPM）功能下，可以设置最小和最大服务器选项以利用更多处理器和线程。随着负载增加，可用于处理它的进程数量会根据这些设置而增加。因为启动每个进程需要时间，所以备用服务器用于处理偶尔的负载峰值。

```
##
## Server-Pool Size Regulation (MPM specific)
##
<IfModule prefork.c>
StartServers		8
MinSpareServers	5
MaxSpareServers	20
MaxClients                150
MaxRequestsPerChild 1000
</IfModule>

<IfModule worker.c>
StartServers               2
MaxClients                150
MinSpareThreads           25
MaxSpareThreads           75
ThreadsPerChild           25
MaxRequestsPerChild       0
</IfModule>

<IfModule perchild.c>
NumServers                5
StartThreads              5
MinSpareThreads           5
MaxSpareThreads           10
MaxThreadsPerChild        20
MaxRequestsPerChild       0
</IfModule>
```

Apache 启动一个由 root 拥有的 master daemon 进程，该进程绑定到适当的 Port，然后切换到非特权用户。然后会以相同的非特权用户（本例中为 apache 用户）启动更多服务器（相当于 **StartServers** 指令的值）。

Apache 会根据当前负载智能地启动和终止服务器。如果流量减少并且空闲服务器过多，则会终止一些服务器（直到 **MinSpareServers** 中注明的服务器数量）。同样，如果在很短的时间内到达大量请求，并且等待新连接的服务器太少，则会启动更多服务器（直到 **MaxSpareServers** 中注明的服务器数量）。

使用上面指定的值，当守护进程启动时，八个服务器进程将运行，等待连接（由 **StartServers** 定义）。随着更多请求的到来，Apache 将确保至少有八个服务器准备好响应请求。当请求已满足且没有新的连接到来时，Apache 将开始终止进程，直到空闲 Web 服务器进程的数量低于 20。**StartServers** 的值应始终介于 **MinSpareServers** 和 **MaxSpareServers** 之间。

Apache 使用 **MaxClients** 指令限制同时运行的服务器进程的总数。默认值为 150，这应该足够高。然而，如果你发现经常有接近这么多服务器在运行，请记住第 150 个之后的任何连接都将被拒绝。在这种情况下，如果你的硬件足够强大（并且网络连接可以处理负载），你应该增加 **MaxClients** 的值。

为了最大程度地减少可能内存泄漏的影响（并保持服务器池“新鲜”），每个服务器进程处理的请求数量是有限制的（等于 `MaxRequestsPerChild` 的值）。在处理完 1000 个请求（上面指定的值）后，该进程将被终止。更准确地说，每个进程可以服务 1000 个 *连接*，因为所有 `KeepAlive` 请求（在遇到 `KeepAliveTimeout` 之前发生）都计算为一个请求。

在多处理器环境中，设置前面描述的线程值既可以限制服务器可以消耗的线程数量，也可以提供你允许用于处理服务器处理的线程数量。`MinSpareThreads` 和 `MaxSpareThreads` 控制未被使用的可用线程数量。如果可用线程低于 `MinSpareThreads`，则会添加更多线程。如果空闲线程超过 `MaxSpareThreads`，则会丢弃一些线程。

## 绑定到特定地址

你可以使用 `Listen` 指令绑定到特定的 IP 地址。`Listen` 指令可用于添加你已有的默认绑定：

```
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, in addition to the default. See also the <VirtualHost>
# directive.
#
# Change this to Listen on specific IP addresses as shown below to
# prevent Apache from glomming onto all bound IP addresses (0.0.0.0)
#Listen 12.34.56.78:80
Listen 80
```

`Listen` 指令比 `BindAddress` 和 `Port` 指令更灵活。可以指定多个 `Listen` 命令，使你能够指定多个 IP 地址/端口号组合。它也可以仅用于指定 IP 地址（在这种情况下仍需要 `Port` 指令）或仅端口号。默认情况下，Apache 在本地计算机的所有接口上监听端口 80（Web 浏览器期望在此找到 Web 内容的地方）。

## 包含模块特定的配置文件

以下行会导致 Apache 从 /etc/httpd/conf.d 目录加载配置文件。该目录包含与特定模块关联的配置文件。

```
#
# Load config files from the config directory "/etc/httpd/conf.d".
#
Include conf.d/*.conf
```

> **交叉引用：** 本章稍后“配置模块 (/etc/httpd/conf.d/*.conf)”部分描述了 conf.d 目录中可能引起你兴趣的一些配置文件。
