
# 配置 Web 服务器 (`httpd.conf`)

`httpd.conf` 文件是 Apache Web 服务器的主配置文件。它包含与服务器整体运行相关的选项。默认文件名（`/etc/httpd/conf/httpd.conf`）可以通过 `httpd` 守护进程的 `-f filename` 命令行参数或 `ServerConfigFile` 指令覆盖。以下各节列出了 `httpd.conf` 文件的内容，并描述了如何使用该文件。

第一节包含关于 `httpd.conf` 文件的注释：

```text
# This is the main Apache server configuration file.  It contains the
###### configuration directives that give the server its instructions.
###### See <URL:http://httpd.apache.org/docs/2.2/> for detailed information.
###### In particular, see
###### <URL:http://httpd.apache.org/docs/2.2/mod/directives.html>
###### for a discussion of each configuration directive.
#
###### Do NOT simply read the instructions in here without understanding
# what they do.  They're here only as hints or reminders.  If you are
# unsure consult the online docs.  You have been warned.
#
###### The configuration directives are grouped into three basic sections:
#
###### 1. Directives that control the operation of the Apache server
###### process as a whole (the 'global environment').
#
###### 2. Directives that define parameters of the main or default server,
###### which responds to requests that aren't handled by a virtual host.
###### These directives also provide default values for the settings
###### of all virtual hosts.
#
###### 3. Settings for virtual hosts, which allow Web requests to be sent
###### to different IP addresses or hostnames and have them handled by
###### the same Apache server process.
#
###### Configuration and logfile names: If the filenames you specify for
###### many of the directives below begin with "/' (or "drive:/" for
# Win32), the server will use that explicit path.  If the filenames do
###### *not* begin with "/", the value of ServerRoot is prepended -- so
###### "logs/foo.log" with ServerRoot set to "/usr/local/apache" will be
###### interpreted by the server as "/usr/local/apache/logs/foo.log".
#
```

这一部分完全由注释组成。它基本上告诉你信息在这个文件中是如何分组的，以及 `httpd` 守护程序如何访问此文件。默认情况下，日志文件位于 `/var/log/httpd` 目录中。

## 设置全局环境

在 `httpd.conf` 文件的“第 1 节：全局环境”中，你设置影响 Apache 服务器一般工作原理的指令。以下是不同指令的用途：

### 网络配置

#### 第 1 节：全局环境

```text
#
###### 此部分中的指令影响 Apache 的整体运行，
###### 例如它能处理多少个并发请求，或者它
###### 在哪里可以找到其配置文件。
#
```

### 隐藏子组件

`ServerTokens` 指令允许你防止远程计算机发现你在 Apache 服务器上运行的是哪些子组件。如果你不介意公开此信息，请注释掉该指令。为了防止信息泄露，`ServerTokens` 设置如下：

```text
#
###### 不要泄露关于我们所运行的所有子组件的过多信息。
###### 如果你不介意远程站点发现你正在运行哪些主要可选模块，
###### 请注释掉此行
ServerTokens OS
```

将 `ServerTokens` 设置为 `ProdctOnly` 可以最小化潜在的入侵者可能看到的连接信息。

### 设置服务器根目录

`ServerRoot` 指令指定了包含配置文件、指向日志文件目录的链接以及指向模块目录的链接的目录。可以使用 `httpd` 的 `-d` 命令行参数指定替代的 `ServerRoot` 路径名。

```text
###### ServerRoot: 服务器配置、错误和日志文件所在目录树的顶部。
#
###### 注意！如果你打算将此放在 NFS（或其他网络）挂载的
###### 文件系统上，请阅读 LockFile 文档（位于
###### <URL:http://httpd.apache.org/docs/2.2/mod/core.html#lockfile>）；
###### 这将为你省去很多麻烦。
#
###### 请勿在目录路径末尾添加斜杠。
#
ServerRoot "/etc/httpd"
```

### 存储服务器的 PID 文件

Apache Web 服务器会跟踪运行中的服务器进程的 PID。你可以使用以下条目更改此文件的位置：

```text
#
###### PidFile: 服务器启动时应记录其进程
###### 标识符的文件。
#
PidFile run/httpd.pid
```

Apache 使用 `PidFile` 存储第一个（root 所有的）主守护进程的过程 ID。此信息在关闭服务器时由 `/etc/init.d/httpd` 脚本使用，也由 `server-status` 处理器使用（稍后描述）。

### 配置超时值

你可以设置几个与超时相关的值。其中一些值在代码后的文本中有描述：

```text
#
###### Timeout: 接收和发送超时前的秒数。
#
Timeout 120

#
###### KeepAlive: 是否允许持久连接（每个连接
###### 多个请求）。设置为 "Off" 以禁用。
#
KeepAlive Off

#
###### MaxKeepAliveRequests: 在持久连接期间允许
###### 的最大请求数。设置为 0 以允许无限数量。
###### 我们建议你保留较高的数字，以获得最大性能。
#
MaxKeepAliveRequests 100

#
###### KeepAliveTimeout: 等待同一客户端在同一连接上的下一个
###### 请求的秒数。
#
KeepAliveTimeout 15
```

`Timeout` 指令确定 Apache 在接收数据包之间、在接收已发送响应的确认之间，或当接收传入请求时，保持连接打开的秒数。如果你发现机器上有过多的打开的空闲连接，可以降低默认的 2 分钟（120 秒）。

`KeepAlive` 指令指示 Apache 在处理完请求后保持连接打开一段时间。这使得来自同一客户端的后续请求能够更快地处理，因为不需要为每个请求创建新连接。这是首选的，这样你可以保持负载和连接数量较低。

`MaxKeepAliveRequests` 指令设置了一个打开连接可以处理的请求数量限制。默认值肯定是合理的，因为大多数连接会在达到 `MaxKeepAliveRequests` 之前触及 `KeepAliveTimeout`。

`KeepAliveTimeout` 指令指定在等待另一个请求时保持连接打开的秒数。你可能想要增加默认值（15 秒）。拥有较长超时的原因可能是为了允许页面上的所有图像在同一连接上下载，或者考虑到客户端浏览你的平均页面并从中选择一个链接可能需要多长时间。你正在使用的 Web 应用程序也可能需要更长的持久连接。（当然，较长的 `keepAliveTimeout` 会防止每个服务器在此期间继续处理其他客户端，因此你可能会发现需要添加更多的请求进程来应对这种情况。）

### 设置服务器进程数

为了高效运行，Web 服务器必须能够同时处理大量传入的内容请求。为了准备处理 Web 内容请求，Apache（在 CentOS 中的设置方式）有多个服务器进程（`httpd` 守护程序）正在运行并监听服务请求。这些服务器反过来可以将请求导向多个线程以服务内容请求。

通过多处理模块（MPM）特性（在 Apache 2.0 中引入），Apache 增加了对线程的支持。在支持原生 POSIX 线程库的操作系统上（CentOS 支持），线程使 Apache 能够通过减少进程槽位和所需服务器数量的内存来提高性能。添加线程比添加进程消耗的资源更少。

对于低流量的 Web 服务器，你可能可以保持支持 MPM 特性的参数不变。你很可能有足够的进程来处理传入请求，但不会多到成为你服务器的负担。然而，如果你的服务器需要持续提供大量内容，或者偶尔需要响应请求的大量激增，你应该考虑调整 `httpd.conf` 文件中的 MPM 相关参数。

如果你想更改任何 MPM 相关参数，这里有几个需要考虑的问题：

- **RAM 至关重要** — 每个活动的进程和线程都会消耗一定量的内存。如果活动进程和线程的数量超过你拥有的 RAM 量，你的计算机将开始使用交换空间，性能会迅速下降。确保你的系统有足够 RAM 来处理你预期在 Apache Web 服务器上运行的最大服务器进程和线程数量。
- **为最大负载配置** — Apache 能够根据需要创建新的服务器进程和线程。你不需要始终拥有最大数量的进程和线程。相反，你可以配置 Apache 可以随着服务器需求动态添加的最大服务器和线程数量。
- **为性能配置** — 当 Apache 必须启动新线程（少量）、启动服务器进程（较大量）或使用交换空间（最大量）时，性能会下降。在理想世界中，你需要的确切服务器数量应该是运行中的服务器默认数量，并留有一些备用以应对合理的峰值。如果响应至关重要，你可能会选择运行比所需更多的服务器，以便在峰值出现时性能不受影响。

Apache 启动时，它会启动一组 `httpd` 服务器进程（一个父进程和多个子 `httpd` 进程）来处理 Web 服务器的传入内容请求。定义可用 `httpd` 服务器进程数量的参数包括设置以下内容的参数：

- 父 `httpd` 服务器应该启动多少个子服务器进程（`StartServers`）
- 保留的空闲服务器进程的最小数量（`MinSpareServers`）
- 保留的空闲服务器进程的最大数量（`MaxSpareServers`）
- 在整个服务器生命周期中 `MaxClients` 的最大值（`ServerLimit`）
- 允许启动的最大服务器进程数（`MaxClients`）
- 一个进程可以服务的最大请求数（`MaxRequestsPerChild`）

定义每个 `httpd` 服务器进程可用线程数量的参数包括设置以下内容的参数：

- 之后将创建更多线程的、始终可用的备用线程的最小数量（`MinSpareThreads`）
- 之后将删除活动线程以回到每个子进程线程数的、备用线程的最大数量（`MaxSpareThreads`）
- 每个子进程始终可用的线程数（`ThreadsPerChild`）

以下代码示例显示了 `httpd.conf` 文件中 MPM 特定参数是如何为 `prefork.c` 模块（用于管理服务器进程的非线程化模块）和 `worker.c`（多线程、多进程 Web 服务器模块）设置的。

```apache
##
###### 服务器池大小调节（MPM 特定）
##
<IfModule prefork.c>
  StartServers         5
  MinSpareServers     5
  MaxSpareServers    20
  ServerLimit        256
  MaxClients         256
  MaxRequestsPerChild 4000
</IfModule>

<IfModule worker.c>
  StartServers         2
  MaxClients          150
  MinSpareThreads     25
  MaxSpareThreads     75
  ThreadsPerChild     25
  MaxRequestsPerChild  0
</IfModule>
```

Apache 启动一个由 root 拥有的主守护进程，该进程绑定到适当的端口，然后切换到非特权用户。随后，更多服务器（相当于 `prefork.c` 中 `Start-Servers` 指令的值）将作为相同的非特权用户启动（在此情况下为 `apache` 用户）。

### **第四部分** 网络

Apache 会根据当前的负载智能地启动和终止服务器。如果流量减少且空闲服务器过多，部分服务器会被终止（数量将降至 `MinSpareServers` 中指定的服务器数量）。同样，如果大量请求在短时间内到达，且等待新连接的服务器过少，系统将启动更多服务器（数量将增至 `MaxClients` 中指定的服务器数量）。

> **注意** 正确设置 `MaxClients` 的值至关重要，因为它限制了可以同时激活的客户端连接总数。如果使用中的 `MaxClients` 服务器数量达到上限，系统将不再创建新的服务器，后续的服务器请求将会失败，直到有空闲服务器释放出来。

使用上述指定的值，当守护进程启动时，父进程和八个子服务器进程将运行并等待连接（由 `StartServers` 定义）。随着更多请求的到来，Apache 将确保至少有五个服务器进程处于就绪状态以响应请求。当请求处理完毕且没有新连接到达时，Apache 将开始终止进程，直到空闲 Web 服务器进程数量低于 20。`StartServers` 的值应始终介于 `MinSpareServers` 和 `MaxSpareServers` 之间。

Apache 使用 `MaxClients` 指令限制同时运行的线程总数。默认值为 150，这通常已经足够高。但是，如果你发现经常有大量线程在运行（接近该数值），请记住超过第 150 个连接将会被拒绝。在这种情况下，如果你的硬件性能足够强大（并且你的网络连接能够承受该负载），你应该增加 `MaxClients` 的值。

> **注意** 通过查看本章稍后描述的服务器状态页面，你可以查看 Apache 服务器进程的状态并了解服务器的活动情况。`ps -fu apache` 命令将显示 Apache 服务器进程（`httpd` 守护进程）当前是否正在运行。

为了将可能的内存泄漏的影响降至最低（并保持服务器池的“新鲜度”），每个服务器进程可处理的请求数量是有限制的（等于 `MaxRequestsPerChild` 的值）。在处理完 4,000 个请求（上述指定的值）后，该进程将被终止。更准确的说法是，每个进程可以服务 4,000 个连接，因为所有 `KeepAlive` 请求（在遇到 `KeepAliveTimeout` 之前发生的）都只计算为一个请求。

在多处理器环境中，设置前面描述的线程值既可以限制服务器可消耗的线程数，也可以提供你允许用于处理服务器请求的尽可能多的线程。`MinSpareThreads` 和 `MaxSpareThreads` 控制当前未使用的可用线程数量。如果可用线程数量低于 `MinSpareThreads`，则会添加更多线程。如果空闲线程数量超过 `MaxSpareThreads`，则会丢弃部分线程。

### 绑定到特定地址

你可以使用 `Listen` 指令绑定到特定的 IP 地址。`Listen` 指令可用于添加到现有的默认绑定中：

```apache
###### Listen: Allows you to bind Apache to specific IP addresses and/or
###### ports, in addition to the default. See also the <VirtualHost>
###### directive.
#
###### Change this to Listen on specific IP addresses as shown below to
###### prevent Apache from glomming onto all bound IP addresses (0.0.0.0)
#Listen 12.34.56.78:80
Listen 80
```

`Listen` 指令比 `Bind` 指令更灵活。可以指定多个 `Listen` 命令，从而允许你指定多个 IP 地址/端口号的组合。它也可以仅用于指定 IP 地址或仅指定端口号。
