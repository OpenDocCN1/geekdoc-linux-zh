
`Timeout` 指令决定了 Apache 在数据包之间保持连接打开的秒数。如果你发现机器上有大量的空闲连接，应该降低默认值（120 秒）。

`KeepAlive` 指令指示 Apache 在处理完请求后一段时间内保持连接打开。允许来自同一客户端的后续请求处理得更快，因为不需要为每个请求创建新连接。

`MaxAliveRequests` 为每个连接可以处理的请求数设置了限制。默认值是合理的，因为大多数连接在达到 `MaxAliveRequests` 之前就会达到 `KeepAliveTimeout`。

`KeepAliveTimeout` 指令指定了在等待同一客户端的下一个请求时保持连接打开的秒数。你可能需要增加默认值（15 秒）。

# 第 21 章：设置 Web 服务器

在此期间可能会移动到另一个客户端，因此你可能会发现需要添加更多的请求处理进程来考虑这种情况。

## 设置服务器进程数

为了高效运行，Web 服务器必须能够同时处理大量传入的内容请求。为了准备好 Web 内容请求，Apache（正如在 Fedora 中设置的那样）运行着多个服务器进程（`httpd` 守护进程）并监听服务请求。这些服务器反过来可以将请求返回给多个线程，以于服务内容请求。

通过多进程处理模块（MPM 特性，在 Apache 2.0 中引入），Apache 增加了对线程的支持。在支持 POSIX 线程库的操作系统上（Fedora 和 RHEL 4 均如此），线程允许 Apache 通过需要更少的进程槽和更少的内存来提高性能。添加线程消耗的资源比添加进程少。

对于低流量的 Web 服务器，你可能不需要去变动支持 MPM 特性的进程。你可能会有足够的进程来处理传入的请求，但又不会多到对你的服务器造成负担。然而，如果你的服务器需要持续地提供大量内容，或者偶尔响应大量的请求峰值，你应该考虑调整 `httpd.conf` 文件中的 MPM 相关参数。

如果你想更改任何 MPM 相关参数，这里有几个需要考虑的问题：

- **内存至关重要** —— 如果活动进程和线程的数量超过了你拥有的 RAM 数量，你的计算机将开始使用交换空间（swap space），性能将迅速下降。确保系统中有足够的 RAM 来处理你预计在 Apache Web 服务器上运行的最大服务器进程和线程。
- **针对最大负载进行配置** —— Apache 可以根据需要创建新的服务器进程和线程。你不需要始终可用最大数量的进程和线程。相反，你可以根据服务器需求配置 Apache 可以动态添加的最大服务器数和线程数。
- **针对性能进行配置** —— 当 Apache 必须启动新线程（较少）、启动服务器进程（较多）或使用交换空间（最多）时，性能会下降。在理想情况下，你需要的确切服务器数量应该是运行的默认数量，并留几个备用以处理合理的峰值。性能至关重要，你可能会选择运行比你需要的更多的服务器，以便在峰值出现时性能不受到损害。

当 Apache 启动时，它会启动固定数量 `httpd` 服务器进程（一个父进程和多个子 `httpd` 进程）来处理 Web 服务器的传入内容请求。定义可用 `httpd` 服务器进程数量的参数包括：

- 父 `httpd` 服务器应启动多少个子服务器进程 (`StartServers`)
- 保留的备用服务器进程最小数量 (`MinSpareServers`)
- 保留的备用服务器进程最大数量 (`MaxSpareServers`)
- 在服务器生命周期内 `MaxClients` 可以超过的最大值 (`ServerLimit`)
- 允许启动的最大服务器进程数 (`MaxClients`)
- 一个进程可以服务的最大请求数 (`MaxRequestsPerChild`)

定义每个 `http` 服务器进程可用线程数量的参数包括设置：

- 始终应可用的备用线程最小数量，超过后将创建更多线程 (`MinSpareThreads`)
- 备用线程的最大数量，超过后活动线程将删除回每个子进程的线程数 (`MaxSpareThreads`)
- 每个子进程始终可用的线程数 (`ThreadsPerChild`)

下面的代码示例了如何在 `httpd.conf` 文件中为 `prefork.c` 模块（管理服务器进程的非线程模块）和 `worker.c`（多线程、多进程 Web 服务器模块）设置 MPM 特定的参数。

```apache
## 服务器池大小调节 (MPM 特有)

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

Apache 启动一个由 `root` 拥有的主守护进程，并绑定到相应的端口，然后切换到非特权用户。随后将以相同的非特权用户（在本例中为 `apache` 用户）启动更多的服务器（等同于 `prefork.c` 中 `StartServers` 指令的值）。

Apache 尝试根据当前负载智能地启动和杀掉（`kill`）服务器。如果流量量减小且有太多的空闲服务器，某些将被杀掉（减少到 `MinSpareServers` 中指定的服务器数量）。同样，如果大量请求在短时间内到达，且等待新连接的服务器太少，则将启动更多服务器（最多达到 `MaxClients` 中指定的服务器数量）。

> 注意：正确获取 `MaxClients` 的值至关重要，它限制了同时活跃的客户端连接总数。如果 `MaxClients` 服务器正在使用中，将不再创建新服务器，对服务器的后续请求将失败。

使用上述值，当守护进程启动时，父进程和八个子进程运行并等待连接（由 `StartServers` 定义）。

### 绑定到特定地址

你可以使用 `Listen` 指令绑定特定的 IP 地址。`Listen` 指令可以在默认基础上添加：

```apache
# Listen: 允许你在默认值之外绑定特定的 IP 地址/或
# 端口。另见 <VirtualHost>
# 指令。
# 将此更改为监听特定的 IP 地址，
# 防止 Apache {到所有绑定地址 (0.0.0.0)
Listen 12.34.56.78:80
Listen 80
```

`Listen` 指令比 `BindAddress` 和 `Port` 指令更灵活。可以指定多个 `Listen` 命令，允许你指定多个 IP 地址/端口组合。它也可以用于仅指定 IP 地址（此时仍需要 `Port` 指令）或仅指定端口号。默认情况下，Apache 监听本地计算机所有接口上的端口 80（标准 http 服务）和端口 443（安全 https 服务），这正是浏览器期望在此处找到 Web 内容。

### 在 httpd.conf 中选择模块

在编译过程中，可以为单个 Apache 模块选择动态链接。除非 `LoadModule` 指令显式标识要加载的模块，否则 `httpd` 服务器进程不会将动态链接的模块加载到内存中。使用 `LoadModule` 指令（带有模块名和相对于 `ServerRoot` 的模块路径）加载多个模块的代码块显示了这些模块的部分列表：

```apache
# 动态共享对象 (DSO) 支持
# 示例:
# LoadModule foo_module modules/mod_foo.so
#
LoadModule access_module modules/mod_access.so
LoadModule auth_module modules/mod_auth.so
LoadModule auth_anon_module modules/mod_auth_anon.so
LoadModule auth_dbm_module modules/mod_auth_dbm.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule include_module modules/mod_include.so
LoadModule log_config_module modules/mod_log_config.so
LoadModule userdir_module modules/mod_userdir.so
```

```apache
LoadModule alias_module modules/mod_alias.so
LoadModule rewrite_module modules/mod_rewrite.so
```
