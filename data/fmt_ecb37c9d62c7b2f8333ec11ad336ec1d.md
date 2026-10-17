
```
#
# Server-pool size regulation. Rather than making you guess how many
# server processes you need, Apache dynamically adapts to the load it
# sees --- that is, it tries to maintain enough server processes to
# handle the current load, plus a few spare servers to handle transient
# load spikes (e.g., multiple simultaneous requests from a single
# Netscape browser).
#
# It does this by periodically checking how many servers are waiting
# for a request. If there are fewer than MinSpareServers, it creates
# a new spare. If there are more than MaxSpareServers, some of the
# spares die off. The default values are probably OK for most sites.
#
MinSpareServers 5
MaxSpareServers 20
#
# Number of servers to start initially --- should be a reasonable
# ballpark figure.
#
StartServers 8
#
# Limit on total number of servers running, i.e., limit on the number
# of clients who can simultaneously connect --- if this limit is ever
# reached, clients will be LOCKED OUT, so it should NOT BE SET TOO LOW.
# It is intended mainly as a brake to keep a runaway server from taking
# the system with it as it spirals down...
#
MaxClients 150
#
# MaxRequestsPerChild: the number of requests each child process is
# allowed to process before the child dies.  The child will exit so
# as to avoid problems after prolonged use when Apache (and maybe the
# libraries it uses) leak memory or other resources.  On most systems,
# this isn't really needed, but a few (such as Solaris) do have notable
# leaks in the libraries.  For these platforms, set to something like
# 10000 or so; a setting of 0 means unlimited.
#
# NOTE: This value does not include keepalive requests after initial
# request per connection.  For example, if a child process handles
# an initial request and 10 subsequent "keepalive" requests, it
# would only count as 1 request towards this limit.
#
MaxRequestsPerChild 1000
```

在独立模式下（源自 `ServerType` 指令），Apache 将启动一个由 root 拥有的主守护进程，该进程绑定到相应的 Port，然后切换到非特权 User。随后，将启动更多的服务器（等效于 `StartServers` 指令的值）作为相同的非特权 User（在这种情况下是 Apache 用户）。

Apache 尝试根据当前负载智能地启动和杀死服务器。如果流量减少且空闲服务器过多，一些服务器将被杀死（降至 `MinSpareServers` 中注明的服务器数量）。同样，如果大量请求在短时间内到达且等待新连接的服务器过少，将启动更多服务器（至多 `MaxSpareServers` 中注明的服务器数量）。

使用上面指定的值，当守护进程启动时，将运行 8 个服务器进程等待连接（由 `StartServers` 定义）。随着更多请求的到达，Apache

这将确保至少有 8 台服务器处于就绪状态以响应请求。当请求被满足且没有新连接到达时，Apache 将开始终止进程，直到空闲的 Web 服务器进程数量低于 20。`StartServers` 的值始终应介于 `MinSpareServers` 和 `MaxSpareServers` 之间。

Apache 使用 `MaxClients` 指令限制同时运行的服务器进程总数。默认值为 150，通常足够高。但是，如果您发现经常有大量（接近该数量）的服务器在运行，请记住，超过第 150 个的所有连接都将被拒绝。在这种情况下，如果您的硬件性能足够强大（并且您的网络连接能够处理该负载），您应该增加 `MaxClients` 的值。

为了最大程度地减少潜在内存泄漏的影响（并保持服务器池“新鲜”），每个服务器进程可处理的请求数量受到限制（等于 `MaxRequestsPerChild` 的值）。在处理完 1000 个请求（即上述指定值）后，该进程将被终止。更准确地说，每个进程可以服务 1000 个*连接*，因为所有的 `KeepAlive` 请求（在遇到 `KeepAliveTimeout` 之前发生的）都仅被计算为一个请求。

## 绑定到特定地址

您可以使用 `Listen` 指令绑定到特定的 IP 地址。`Listen` 指令可用于在现有默认绑定基础上添加：

```
# Listen: Allows you to bind Apache to specific IP addresses and/or
# ports, in addition to the default. See also the VirtualHost
# directive.
#
#Listen 3000
#Listen 12.34.56.78:80
#Listen 80
```

`Listen` 指令比 `BindAddress` 和 `Port` 指令更灵活。可以指定多个 `Listen` 命令，从而允许您指定多个 IP 地址/端口号组合。它也可以仅用于指定 IP 地址（此时仍需要 `Port` 指令）或仅指定端口号。默认情况下，Apache 监听本地计算机的 80 端口（这是 `/etc/services` 中列出的标准 www 端口）。

## 在虚拟地址上绑定

Apache 支持虚拟主机（virtual hosts）的概念。使用 `BindAddress` 条目，您可以告诉服务器应监听哪个 IP 地址或完全限定的互联网域名：

```
# BindAddress: You can support virtual hosts with this option. This
# option is used to tell the server which IP address to listen to. It
# can either contain "*", an IP address, or a fully qualified Internet
# domain name. See also the VirtualHost and Listen directive.
#BindAddress *
```

默认情况下，Web 服务器将监听为该机器配置的所有 IP 地址的指定端口（行为与上述行未取消注释时相同）。或者，`Listen` 指令（在本节稍后描述）可以提供对服务器使用的 IP 地址、完全限定域名和端口的更大控制权。`BindAddress` 指令只能使用一次。

## 在 httpd.conf 中选择模块

在编译过程中，可以选择特定的 Apache 模块进行动态链接。动态链接的模块不会加载到 httpd 服务器进程内存中，除非这些模块被 `LoadModule` 指令明确标识为需要加载。下面显示的代码块使用 `LoadModule` 指令，通过模块名称和模块路径（相对于 `ServerRoot`）选择加载到内存中的多个模块。以下文本显示了这些模块的部分列表：
