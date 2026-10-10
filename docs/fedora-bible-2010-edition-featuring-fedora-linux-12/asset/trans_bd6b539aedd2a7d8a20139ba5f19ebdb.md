
## 设置服务器进程数

为了高效运行，Web 服务器必须能够同时处理大量传入的内容请求。为了准备处理 Web 内容请求，Apache（在 Fedora 中的配置方式）会有多个服务器进程（httpd 守护进程）运行并监听服务请求。这些服务器进而可以将请求引导至多个线程以处理内容请求。

借助多处理模块（MPM）特性（在 Apache 2.0 中引入），为 Apache 增加了线程支持。在支持原生 POSIX 线程库的操作系统上（Fedora 即支持此类系统），线程允许 Apache 通过减少所需的进程槽位和服务器数量所需的内存来提高性能。与增加进程相比，增加线程消耗的资源更少。

对于低流量的 Web 服务器，您可能可以直接保留支持 MPM 特性的参数不变。您可能拥有足够处理传入请求的进程数量，但数量不会多到成为服务器的负担。然而，如果您的服务器需要持续提供大量内容，或者需要偶尔应对请求量的巨大峰值，请考虑调整 `httpd.conf` 文件中与 MPM 相关的参数。

如果您想更改任何与 MPM 相关的参数，以下是需要考虑的一些问题：

-   **获取足够的 RAM** — 内存至关重要。每个活跃的进程和线程都会消耗一定数量的内存。如果活跃的进程和线程数量超过了您拥有的 RAM 容量，您的计算机将开始使用交换空间，性能会迅速下降。确保您的系统有足够的 RAM 来预期在 Apache Web 服务器上运行的最大服务器进程数和线程数。
-   **针对最大负载进行配置** — Apache 能够根据需要创建新的服务器进程和线程。您并不需要在所有时刻保持最大数量的进程和线程可用。相反，您可以配置 Apache 可以根据服务器需求动态添加的服务器和线程的最大数量。
-   **针对性能进行配置** — 当 Apache 不得不启动新线程（少量开销）、启动服务器进程（较多开销）或使用交换空间（最大开销）时，性能会下降。具体数值取决于服务器硬件、配置和负载，但这些相对值始终成立。在一个完美的世界里，您需要的服务器确切数量应该是默认运行的服务器数量，并保留少量备用以应对合理的峰值。如果响应速度至关重要，您可能会选择运行比实际需求更多的服务器，以便在出现峰值时不影响性能。

当 Apache 启动时，它会启动一定数量的 httpd 服务器进程（一个父进程和多个子 httpd 进程）来处理传入的 Web 服务器内容请求。定义可用 httpd 服务器进程数量的参数包括那些设置以下内容的参数：

-   父 httpd 服务器应启动的子服务器进程数量（`StartServers`）
-   保持备用的空闲服务器进程的最小数量（`MinSpareServers`）
-   保持备用的空闲服务器进程的最大数量（`MaxSpareServers`）
-   允许启动的最大服务器进程数量（`MaxClients`）
-   在服务器生命周期内 `MaxClients` 可取的最大值（`ServerLimit`）
-   单个进程可处理的最大请求数（`MaxRequestsPerChild`）

定义每个 httpd 服务器进程中可用线程数量的参数包括那些设置以下内容的参数：

-   在创建更多线程之前，应始终可用的备用线程的最小数量（`MinSpareThreads`）
-   备用线程的最大数量，超过此数量后将删除活跃线程以恢复到每个子进程的线程数（`MaxSpareThreads`）
-   每个子进程始终可用的线程数量（`ThreadsPerChild`）

下面的代码示例展示了在 `httpd.conf` 文件中，`prefork.c` 模块（用于管理服务器进程的非线程模块）和 `worker.c`（多线程、多进程 Web 服务器模块）中 MPM 特定参数的设置方式。

```apache
<IfModule prefork.c>
StartServers		8
MinSpareServers	5
MaxSpareServers	20
ServerLimit	256
MaxClients	256
MaxRequestsPerChild 4000
</IfModule>

<IfModule worker.c>
StartServers		2
MaxClients		150
MinSpareThreads	25
MaxSpareThreads	75
ThreadsPerChild	25
MaxRequestsPerChild 0
</IfModule>
```

Apache 启动一个由 root 拥有的主守护进程，该进程绑定到相应的端口，然后切换到非特权用户。随后，将以相同的非特权用户（在本例中为 `apache` 用户）身份启动更多的服务器（相当于 `prefork.c` 中 `StartServers` 指令的值）。

Apache 试图根据当前负载智能地启动和终止服务器。如果流量减少且空闲服务器过多，部分服务器将被终止（减少至 MinSpareServers 中记录的服务器数量）。同样，如果大量请求在短时间内到来且等待新连接的服务器过少，将启动更多的服务器（增加至 MaxClients 中记录的服务器数量）。

> **注意：** 正确获取 MaxClients 的值至关重要，因为它限制了可同时处于活动状态的客户连接总数。如果所有 MaxClients 指定的服务器都在使用中，将不再创建新的服务器，并且对服务器的后续请求将失败，直到有服务器被释放。如果您从默认值增加 MaxClients，还需要增加 ServerLimit。

使用上述指定值，当守护进程启动时，父进程和八个子服务器进程将运行，等待连接（由 `StartServers` 定义）。随着更多请求的到来，Apache 将确保至少有五个服务器进程准备就绪以响应请求。当请求得到处理且没有新连接到来时，Apache 将开始终止进程，直到空闲的 Web 服务器进程数量低于 20。`StartServers` 的值始终应位于 `MinSpareServers` 和 `MaxSpareServers` 之间。

Apache 使用 MaxClients 指令限制同时线程的总数。默认值为 150，这应该足够了。但是，如果您发现经常有接近该数量的线程在运行，请记住任何超过第 150 个的连接都将被拒绝。在这种情况下，如果您的硬件足够强大（且您的网络连接能够处理该负载），您应该增加 MaxClients 的值。

> **注意：** 您可以通过查看本稍后章节中描述的服务器状态页面来查看 Apache 服务器进程的状态，并了解服务器的活动情况。`ps -fu apache` 命令可以显示当前是否正在运行 Apache 服务器进程（httpd 守护进程）。

为了最小化潜在内存泄漏的影响（并保持服务器池“新鲜”），每个服务器进程可处理的请求数量都有限制（等于 `MaxRequestsPerChild` 的值）。在处理了 4,000 个请求（前一个示例中指定的值）后，该进程将被终止。更准确的说法是，每个进程可以服务 4,000 个*连接*，因为所有 KeepAlive 请求（在 keep-alive 请求超时之前发生，如 KeepAliveTimeout 所指定）都被计算为一个请求。

在多处理器环境中，设置前面描述的线程值既可以限制服务器可消耗和提供的线程数量，也可以提供尽可能多的线程来处理服务器操作。MinSpareThreads 和 MaxSpareThreads 控制可用的未使用线程数量。如果可用线程低于 MinSpareThreads，则添加更多线程。如果备用线程超过 MaxSpareThreads，则丢弃部分线程。

## 绑定到特定地址

您可以使用 `Listen` 指令绑定到特定的 IP 地址。`Listen` 指令可用于添加您已有的默认绑定：

```apache
Listen 80
```

`Listen` 指令比 `BindAddress` 指令更灵活。可以指定多个 `Listen` 命令，使您能够指定多个 IP 地址/端口号组合。它们还可以用于仅指定 IP 地址或仅指定端口号。

默认情况下，Apache 在本地计算机的所有接口上监听端口 80（用于标准 http 服务）和端口 443（用于安全的 https 服务）（这是 Web 浏览器预期找到 Web 内容的地方）。仅在 `localhost:80` 上监听将限制访问仅给本地机器上的用户。由非特权用户运行的 Web 服务器通常绑定到端口 8080（只有 root 可以绑定到 1024 以下的端口）。如果您有多个网络接口卡，您可以限制 Apache 监听的接口（例如，您可以拥有一个仅面向公司局域网而未暴露到 Internet 接口的 Web 服务器）。

## 在 httpd.conf 中选择模块

在编译过程中，可以选择单独的 Apache 模块进行动态链接。动态链接的模块不会加载到 httpd 服务器进程的内存中，除非使用 `LoadModule` 指令明确标识要加载这些模块。接下来的代码块通过带有模块名和模块路径（相对于 `ServerRoot`，通常为 `/etc/httpd`）的 `LoadModule` 指令，选择将多个模块加载到内存中。以下代码显示了这些模块的部分列表：

```apache
# Dynamic Shared Object (DSO) Support
# Example:
# LoadModule foo_module modules/mod_foo.so
#
LoadModule auth_basic_module modules/mod_auth_basic.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule authn_file_module modules/mod_authn_file.so
...
LoadModule suexec_module modules/mod_suexec.so
LoadModule disk_cache_module modules/mod_disk_cache.so
LoadModule cgi_module modules/mod_cgi.so
```

Apache 模块通过 `LoadModule` 指令包含在活跃模块列表中。`ClearModuleList` 指令从当前活跃模块列表中删除所有条目。Fedora 上随 Apache 附带的每个标准模块都在表 20-1 中进行了描述。

如果某个模块包含不必要的功能，可以很容易地将其注释掉（从上述列表中移除）。事实上，注释掉未使用的模块是一种良好的安全实践。同样，您可能希望添加第三方模块的功能或特性（用于

