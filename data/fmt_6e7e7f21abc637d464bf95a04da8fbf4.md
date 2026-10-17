
一些与 Apache 相关的单独模块、脚本和其他服务，如 `perl`、`php`、`ssl` 和 `webalizer`，可能有单独的配置文件会吸引你。这些文件包含在 `/etc/httpd/conf.d/` 目录中。请参阅本章稍后的“配置模块和相关服务（`/etc/httpd/conf.d/*.conf`）”部分。

> **注意：** 关于 Apache 的更多信息可以在你自己的 Web 服务器上获取，通过 `http://localhost/manual/`（如果安装了 `httpd-manual` 包）。

### 配置 Web 服务器 (`httpd.conf`)

`httpd.conf` 文件是 Apache Web 服务器的主配置文件，包含涉及服务器通用操作的选项。默认文件名（`/etc/httpd/conf/httpd.conf`）可以通过 `httpd` 守护进程的 `-f filename` 命令行参数或 `ServerConfigFile` 指令来覆盖。以下部分列出了 `httpd.conf` 文件的内容，并描述如何使用该文件。

第一部分包含关于 `httpd.conf` 文件的注释：

```apache
# This is the main Apache server configuration file. It contains the
# configuration directives that give the server its instructions.
# See <URL:http://httpd.apache.org/docs/2.2/> for detailed information.
# In particular, see
# <URL:http://httpd.apache.org/docs/2.2/mod/directives.html>
# for a discussion of each configuration directive.
#
# Do NOT simply read the instructions in here without understanding
# what they do. They're here only as hints or reminders. If you are
# unsure consult the online docs. You have been warned.

.
.
.
```

该部分完全由注释组成。它基本上告诉了你此文件中的信息是如何分组的，以及 `httpd` 守护进程如何访问此文件。默认情况下，日志文件位于 `/var/log/httpd` 目录中。

#### 设置全局环境

在 `httpd.conf` 文件的“第 1 节：全局环境”中，你设置影响 Apache 服务器通用运行的指令。大多数全局指令都可以在特定的虚拟域中覆盖，如果你为多个域提供 Web 服务的话。以下是不同指令的作用：

```apache
### Section 1: Global Environment
#
# The directives in this section affect overall operation of Apache,
# such as the number of concurrent requests it can handle or where it
# can find its configuration files.
#
```

#### 揭示子组件

`ServerTokens` 指令可以让你阻止远程计算机查出你在 Apache 服务器上运行的子组件。如果你不介意暴露这些信息，可以注释掉此指令。为了防止暴露，`ServerTokens` 设置如下：

```apache
#
# Don't give away too much information about all the subcomponents
# we are running. Comment out this line if you don't mind remote sites
# finding out what major optional modules you are running
ServerTokens OS
```

将 `ServerTokens` 设置为 `ProductOnly` 将最小化潜在攻击者可能看到的连接信息。

#### 设置服务器根目录

`ServerRoot` 指令指定了包含配置文件、指向日志文件目录的链接以及指向模块目录的链接的目录。可以使用 `httpd` 的 `-d` 命令行参数指定替代的 `ServerRoot` 路径名。

```apache
ServerRoot "/etc/httpd"
```

#### 存储服务器的 PID 文件

Apache Web 服务器跟踪正在运行的服务器进程的 PID。你可以使用以下条目更改此文件的位置：

```apache
PidFile run/httpd.pid
```

Apache 使用 `PidFile` 来存储第一个（root 拥有的）主守护进程进程的 ID。此信息由 `/etc/init.d/httpd` 脚本在关闭服务器时使用，也由 `server-status` 处理程序使用（本章稍后描述）。

#### 配置超时值

你可以设置几个与超时相关的值。其中一些值在代码后的文本中进行了描述：

```apache
Timeout 120
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```

`Timeout` 指令确定 Apache 在接收数据包之间、在接收发送响应的确认之间，或在接收传入请求期间保持连接打开的秒数。如果发现在机器上有过多的打开的闲置连接，可以默认的两分钟（120 秒）减少。

`KeepAlive` 指令指示 Apache 在处理完请求后保持连接打开一段时间。这使来自同一客户端的后续请求能够更快地处理，因为不需要为每个请求创建新的连接。

`MaxKeepAliveRequests` 指令设置在一个打开的连接中可以处理的请求数量限制。默认值肯定是合理的，因为大多数连接会在达到 `MaxKeepAliveRequests` 之前命中 `KeepAliveTimeout`。

`KeepAliveTimeout` 指令指定在等待另一个请求期间保持连接打开的秒数。你可能希望增加默认值（15 秒）。拥有较长超时的原因可能是为了允许在同一连接上下载页面上的所有图像，或者考虑到客户端浏览你的平均页面并从中选择链接可能需要多长时间。你正在使用的 Web 应用程序也可能需要较长的持久连接。（当然，较长的 `KeepAliveTimeout` 会阻止每个服务器在此时间段内转向另一个客户端，因此你可能会发现需要添加更多的请求进程来考虑这一点。）

### 设置服务器进程数

为了高效运行，Web 服务器必须能够同时处理大量传入的内容请求。为了准备处理 Web 内容请求，Apache（在 Fedora 中的配置方式）会有多个服务器进程（`httpd` 守护进程）运行并监听服务请求。这些服务器进而可以将请求引导至多个线程以处理内容请求。

借助多处理模块（MPM）特性（在 Apache 2.0 中引入），为 Apache 增加了线程支持。在支持原生 POSIX 线程库的操作系统上（Fedora 即支持此类系统），线程允许 Apache 通过减少所需的进程槽位和服务器数量所需的内存来提高性能。与增加进程相比，增加线程消耗的资源更少。

对于低流量的 Web 服务器，您可能可以直接保留支持 MPM 特性的参数不变。您可能拥有足够处理传入请求的进程数量，但数量不会多到成为服务器的负担。然而，如果您的服务器需要持续提供大量内容，或者需要偶尔应对请求量的巨大峰值，请考虑调整 `httpd.conf` 文件中与 MPM 相关的参数。

如果您想更改任何与 MPM 相关的参数，以下是需要考虑的一些问题：

- **获取足够的 RAM** — 内存至关重要。每个活跃的进程和线程都会消耗一定数量的内存。如果活跃的进程和线程数量超过了您拥有的 RAM 容量，您的计算机将开始使用交换空间，性能会迅速下降。确保您的系统有足够的 RAM 来预期在 Apache Web 服务器上运行的最大服务器进程数和线程数。
- **针对最大负载进行配置** — Apache 能够根据需要创建新的服务器进程和线程。您并不需要在所有时刻保持最大数量的进程和线程可用。相反，您可以配置 Apache 可以根据服务器需求动态添加的服务器和线程的最大数量。
- **针对性能进行配置** — 当 Apache 不得不启动新线程（少量开销）、启动服务器进程（较多开销）或使用交换空间（最大开销）时，性能会下降。具体数值取决于服务器硬件、配置和负载，但这些相对值始终成立。在一个完美的世界里，您需要的服务器确切数量应该是默认运行的服务器数量，并保留少量备用以应对合理的峰值。如果响应速度至关重要，您可能会选择运行比实际需求更多的服务器，以便在出现峰值时不影响性能。
