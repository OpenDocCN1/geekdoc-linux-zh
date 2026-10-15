
# KeepAliveTimeout: 等待同一连接上同一客户端发送下一个请求的秒数。

`KeepAliveTimeout` 15

`Timeout` 指令规定了 Apache 在接收数据包之间、接收响应确认之间、或在接收传入请求期间保持连接打开的秒数。如果你发现服务器上存在过多的空闲连接，可以将默认的二分钟（120 秒）调低。

`KeepAlive` 指令指示 Apache 在处理完请求后保持连接一段时间。这使得来自同一客户端的请求可以被处理得更快，因为不需要为每个请求创建新连接。

`MaxKeepAliveRequests` 对一个打开的连接可以处理的请求数设置了限制。默认值显然是合理的，因为大多数连接在达到 `MaxKeepAliveRequests` 之前就会达到 `KeepAliveTimeout`。

`KeepAliveTimeout` 指令指定了在等待另一个请求时保持连接的秒数。你可能希望增加默认值（15 秒）。设置较长超时时间的可能是为了允许页面上的所有图像在同一个连接上下载，或者考虑到客户端浏览你的平均页面并从中选择一个链接可能需要的时间。你可能运行的 Web 应用程序也需要更长的持久连接。（当然，较长的 `KeepAliveTimeout` 会防止每个服务器在此期间段切换到另一个客户端，所以你可能会发现需要更多的请求处理进程来考虑这一点。）

## 设置服务器进程数

为了高效运行，Web 服务器必须能够同时处理大量入站的内容请求。为了准备处理 Web 内容请求，Apache（在 Fedora 中设置的）有多个正在运行并监听服务请求的服务器进程（`httpd` 守护进程）。这些服务器反可以将请求重定向到多个线程来处理内容请求。

通过多进程处理模块（MPM）功能（在 Apache 2.0 中引入），Apache 增加了线程支持。在支持原生 POSIX 线程库的操作系统上（Fedora 和 RHEL 都支持），线程允许 Apache 通过所需的服务器数量更少的进程槽和更少的内存来提高性能。添加线程比添加进程消耗更少的资源。

对于低流量的 Web 服务器，你可能有足够的进程来处理入站请求，但又多到至于不会成为服务器的负担。如果你的服务器需要持续提供大量内容，或者偶尔响应大量的请求激增，你应该考虑调整 `httpd.conf` 文件中 MPM 相关的参数。

如果你想更改任何 MPM 相关的参数，可能会遇到以下问题：

- `内存至关重要`：每个活动状态的进程和线程都会消耗一些内存。如果活动线程的数量超过了计算机的 RAM 数量，计算机将开始使用交换分区（`swap`），性能将会下降。
- `为最大负载进行配置`：Apache 能够根据需要创建新线程。确保有你预期的最大服务器数量所需的 RAM。
- `为性能进行配置`：Apache 必须启动新进程（更大的数量）。服务器的数量应该是默认值。
- `为激增进行配置`：你可能选择比需要的更多的服务器，以便。

当 Apache 启动时，它会启动一组 `httpd` 服务器进程（一个父进程和多个子进程）来处理内容的传入请求。定义 `httpd` 服务器进程可用性的参数包括：

- `StartServers`: 父 `httpd` 服务器启动的子进程数。
- `MinSpareServers`: 保持的最空闲服务器进程数。
- `MaxSpareServers`: 保持的最大空闲服务器进程数。
- `ServerLimit`: 在服务器生命周期内 `MaxClients` 的最大值。
- `MaxClients`: 允许启动的最大服务器进程数。
- `MaxRequestsPerChild`: 进程可以服务的最大请求数。

定义每个 `httpd` 服务器进程可用线程数的参数包括：

- `MinSpareThreads`: 应该始终保持的最少空闲线程数，超过后将创建更多。
- `MaxSpareThreads`: 最大空闲线程数，超过后将删除活动线程以恢复到子进程的线程数。
- `ThreadsPerChild`: 每个子进程可用的线程数。

下面的代码示例显示了 `httpd.conf` 文件中的 MPM 特定参数如何为 `prefork.c` 模块（管理服务器进程的非线程模块）和 `worker.c`（多线程、多进程 Web 服务器模块）工作。

```apache
##
服务器池大小调节（MPM 特有）
##
<IfModule prefork.c>
StartServers 8
MinSpareServers 5
MaxSpareServers 20
ServerLimit 256
MaxClients 256
MaxRequestsPerChild 4000
</IfModule>
```

```apache
<IfModule worker.c>
StartServers 2
MaxClients 150
MinSpareThreads 25
MaxSpareThreads 75
ThreadsPerChild 25
MaxRequestsPerChild 0
</IfModule>
```

Apache 启动一个 `root` 拥有的守护进程绑定到相应的端口，然后切换到非特权用户。更多的服务器（等同于值的

`prefork.c` 中的 `StartServers` 指令将以相同的非特权用户（在此情况下为 `apache` 用户）启动。

Apache 尝试根据当前负载智能地启动和杀毁服务器。如果流量减少且存在过多的空闲服务器，某些服务器将被杀死（减少到 `MinSpareServers` 中指定的服务器数量）。同样地，如果在短时间内收到大量请求，则会启动更多的服务器（最多达到 `MaxClients` 中注明的服务器数量）。

> 注意：正确设置 `MaxClients` 的值至关重要，因为它限制了此时可以激活的客户端连接总数。如果 `MaxClients` 数量的服务器在使用中，将不会再创建新的服务器，后续对服务器的请求将失败，直到某个连接被释放。

使用上述指定的值，当守护进程启动时，父进程和每个子服务器进程将运行并等待连接（由 `StartServers` 定义）。随着更多请求的到来，Apache 将确保至少有五个服务器进程准备就绪响应请求。当请求处理完毕且没有新连接到达时，Apache 将开始杀死进程，直到空闲 Web 服务器进程的数量低于 20。`StartServers` 的值应始终处于 `MinServers` 和 `MaxServers` 之间。

Apache 通过 `MaxClients` 指令限制并发线程的总数。默认值为 150，这应该足够高了。然而，如果你发现自己经常有许多线程在运行，请记住任何超过 150 的连接都将被拒绝。在这种情况下，如果你的硬件足够强大（且如果你的网络连接能够处理该负载），你应该增加 `MaxClients` 的值。

> 注意：你可以通过查看本章稍后描述的服务器 `server-status` 页面来查看 Apache 服务器进程的状态并感受服务器的活动。`ps -fu apache` 命令将向你显示 Apache 服务器进程（`httpd` 守护进程）是否正在运行。

为了最大限度地减少可能的内存泄漏的影响（并保持服务器池的“新鲜”），每个服务器进程处理的请求数量受到限制（等于 `MaxRequestsPerChild` 的值）。在处理完 4000 个请求（上述指定的值）后，该进程将被杀死。更准确地说，每个进程可以处理 4000 个连接，因为每个 `KeepAlive` 请求（在遇到 `KeepAliveTimeout` 之前发生）都仅计为一次请求。

在多处理器环境中，设置之前描述的线程值既可以限制服务器消耗的线程数，也可以限制你允许处理服务器处理的线程数。`MinSpareThreads` 和 `MaxThreads` 控制未使用的可用线程数。如果可用线程低于 `MinSpareThreads`，则会添加更多线程。如果线程超过 `MaxSpareThreads`，则某些线程会被丢弃。

## 第 21 章：设置 Web 服务器

### 绑定到特定地址

你可以使用 `Listen` 指令绑定 IP 地址。`Listen` 指令可用于向已有的默认绑定添加：

```
# Listen: 允许你除默认值之外绑定到特定的 IP 地址和/或
# 端口。另参见 <VirtualHost>
# 指令。
# 将此更改为如下所示在特定 IP 地址上监听，
# 防止 Apache 绑定到所有绑定的 IP 地址 (0.0.0.0)
#Listen 12.34.56.78:80
Listen 80
```
