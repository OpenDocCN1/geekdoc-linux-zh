
典型的 `httpd.conf` 文件可能包含表 23.1 所列的指令。

#### 表 23.1 常见的 `httpd.conf` 指令

| 指令名称 | 描述 |
|---|---|
| `AddModule` | 指定 Apache 启动时要启用的预编译模块。该模块必须通过 `LoadModule` 指令加载，才能通过 AddModule 指令启用。`httpd.conf` 通常包含多条 AddModule 指令，默认的 `httpd.conf` 包含大量 AddModule 指令，用于启用 Apache 发行版附带的一组标准模块。本章后面的“Apache 模块”一节将对 Apache 模块进行更详细的讨论。 |
| `ClearModuleList` | 指定应清除 Apache 默认的已启用模块列表。这样，AddModule 指令就可以指定要启用的模块，而不是使用默认预加载的列表。 |
| `CustomLog` | 指定记录成功访问尝试的日志文件的位置。它还标识要写入的日志条目类型。值的格式为 `<Complete path of log file> <Entry type>`。该文件必须可由 Apache 守护进程运行所针对的用户写入；Apache 守护进程的用户和组通过 User 和 Group 指令指定。条目类型应为通过 LogFormat 指令指定的日志格式的别名。 |
| `ErrorLog` | 指定用于记录错误消息的文件位置。该文件应可由 Apache 守护进程运行所针对的用户写入；Apache 守护进程的用户和组通过 User 和 Group 指令指定。 |
| `Group` | 指定 Apache 守护进程运行所针对的组。这应为 `/etc/group` 文件中指定的有效 Linux 用户组。注意通过使用访问权限受限的组来限制 Apache 守护进程的访问权限。通常，Apache 守护进程在 nobody 组中运行。 |
| `HostNameLookups` | 指定当客户端连接时，Apache 是否应尝试使用 DNS 查找客户端的主机名。这允许 Apache 记录客户端的主机名而不是 IP 地址，但会带来相当大的开销，因为 DNS 查找可能非常耗时。此外，如果启用且连接失败，客户端连接可能会超时。可能的值为 `on` 或 `off`。 |
| `KeepAlive` | 指定当服务器以 ServerType 指令指定的独立模式运行时，是否应启用 Apache 的 KeepAlive 功能。启用后，Apache 会与客户端建立持久连接，从而提升性能，因为无需为每个页面请求创建新连接。可能的值为 on 或 off。默认值为 on，符合 HTTP 1.1 规范，即启用该功能。 |
| `KeepAliveTimeout` | 指定当服务器以 ServerType 指令指定的独立模式运行时，持久连接在多少空闲时间后关闭。时间以秒为单位，默认值 100 秒通常比较合适。 |
| `LoadModule` | 指定 Apache 启动时要加载的已编译模块。值的格式为 `<External module name> <compiled module object file>`。通常，Apache httpd.conf 文件包含大量在启动时加载的预先指定的模块。除非您要添加没有自动安装过程的第三方模块，否则无需更改此列表。 |
| `LogFormat` | 指定日志文件条目类型的格式。通常，httpd.conf 文件中会出现多条 LogFormat 指令。LogFormat 指令的值的格式为 `<Entry definition> <Entry alias>`。条目别名用于其他指令（如 CustomLog 指令）中，以指示要写入日志文件的日志条目类型。默认的 httpd.conf 文件通常包含四条 LogFormat 条目，别名分别为：combined、common、referer 和 agent。referer 和 agent 格式指定了随后用于 combined 和 common 日志格式的日志格式。common 日志格式定义了通用日志格式（Common Log Format），这是一种标准的 Web 服务器日志条目格式，也是 CustomLog 指令中使用的默认格式。combined 格式是 common 格式的一种替代，它在通用日志格式的基础上添加了 referer 和 agent 格式中指定的引用页和用户代理信息。 |
| `LogLevel` | 指定 Apache 应执行的错误日志记录级别。可能的级别有：emerg（记录所有紧急错误）、alert（记录警报条件）、critical（记录严重错误）、warn（记录所有警告）和 debug（记录服务器的几乎所有消息）。debug 错误级别对于确定服务器配置问题很有用，但会产生过多的磁盘写入活动，可能影响服务器性能。默认级别 warn 通常最适合正常服务器使用。 |
| `MaxClients` | 指定当服务器以 `ServerType` 指令指定的独立模式运行时，所支持的最大同时请求数。最大值为 256。需要仔细考虑此设置的值，尤其是在通过 `KeepAlive` 指令启用持久连接的情况下。如果启用了持久连接，并且您将最大客户端数设置得太小，则当新客户端连接时会出现连接资源争用。同时，随着开放连接数量的增加，您将面临性能损失，这在较小的 Web 服务器上可能非常显著。 |
| `MaxKeepAliveRequests` | 指定当服务器以 `ServerType` 指令指定的独立模式运行时，每个持久连接在必须关闭之前所能服务的最大请求数。这有助于防止客户端通过反复请求文档来维持永久的持久连接。对于大多数服务器，默认值 100 都能很好地工作。请记住，值为 0 实际上会禁用持久连接，即使 `KeepAlive` 设置为 on 也是如此。 |
| `MaxRequestsPerChild` | 指定当服务器以 `ServerType` 指令指定的独立模式运行时，每个子服务器进程处理的最大请求数。在独立模式下运行时，Apache 守护进程会启动一定数量的子进程来监听连接，并尽量保持最少数量的子进程等待新的传入连接。子进程处理完指定数量的请求后，将终止并被新的子进程替换。对于大多数服务器，默认值 30 都能很好地工作。 |
| `MaxSpareServers` | 指定当服务器以 `ServerType` 指令指定的独立模式运行时，任意时刻等待传入连接的最大子服务器数。在独立模式下运行时，Apache 守护进程会启动一定数量的子进程来监听连接，并尽量保持最少数量的子进程等待新的传入连接。子进程处理完指定数量的请求后，将终止并被新的子进程替换。在繁忙的服务器上，此值会对服务器性能产生显著影响。随着备用服务器数量的增加，您可以快速响应更多传入连接。但这意味着资源被分配给等待中的服务器进程，实际上您允许在 `MaxClients` 指令指定的限制内发生更多同时连接。 |

#### 表23.1：Apache指令

| 指令名称 | 描述 |
|---|---|
| `MinSpareServers` | 指定当服务器以ServerType指令指定的独立模式运行时，在任何时刻等待传入连接的最小自服务器数量。在独立模式下运行时，Apache守护进程会启动多个子进程来监听连接，并努力保持最小数量的子进程可用于等待新的传入连接。子进程在服务完指定数量的请求后会消亡，并由新的子进程替换。在繁忙的服务器上，该值会对服务器性能产生显著影响。随着备用服务器数量的增加，您可以快速响应更多传入连接。这意味着资源被分配给等待的服务器进程，并且您实际上允许在MaxClients指令指定的限制范围内发生更多数量的并发连接。您不应将此值设置得太高，因为这会不必要地浪费资源。Apache将根据当前系统负载，在MinSpareServers和MaxSpareServers指定的最小值和最大值之间调整备用服务器的数量。如果将此值设置得太高，Apache将无法根据负载需求按需减少备用服务器的数量。 |
| `PidFile` | 指定当服务器以ServerType指令指定的独立模式运行时，用于存储主Apache服务器守护进程的进程ID的文件名。 |
| `Port` | 指定当服务器以ServerType指令指定的独立模式运行时，Apache服务器将监听传入连接的端口。HTTP传入连接的默认端口是80。除非您想在非标准端口上运行服务器，否则不要更改此值。 |
| `ServerAdmin` | 指定服务器管理员的电子邮件地址，该地址显示在Apache向用户显示的默认错误消息中。 |
| `ServerName` | 指定您的Web服务器的默认主机名。该名称应具有指向运行Apache的服务器的有效DNS条目。 |
| `ServerRoot` | 指定保存Apache配置、错误和日志文件的顶级目录。如果您从源代码归档安装Apache，则此目录很可能是`/usr/local/apache/`。 |
| `ServerType` | 指定您希望将Apache作为独立进程运行，还是通过标准inetd机制调用Apache。可能的值是standalone和inetd。有关选择standalone或inetd操作的问题将在后面的“选择独立运行还是通过inetd运行Apache”一节中讨论。 |
| `StartServers` | 指定当服务器以ServerType指令指定的独立模式运行时，Apache将启动的等待传入连接的初始子服务器数量。在独立模式下运行时，Apache守护进程会启动多个子进程来监听连接，并努力保持最小数量的子进程可用于等待新的传入连接。您可以将其保持为默认值，因为Apache将根据当前系统负载，在`MinSpareServers`和`MaxSpareServers`指定的最小值和最大值之间调整备用服务器的数量。 |
| `Timeout` | 指定Apache服务器在放弃之前等待客户端响应的时间（以秒为单位）。默认值300对大多数服务器都很适用。 |
| `UseCanonicalNames` | 指定Apache是否应使用`ServerName`和`Port`指令中指定的服务器和端口，或使用客户端在文档请求中指定的服务器名称和端口，来构建自引用链接的URL。自引用链接是相对于当前文档指定的链接类型。当设置为on时，启用该功能，并使用指令中指定的服务器和端口。当设置为off时，禁用该功能，并使用客户端请求中指定的值。 |
| `User` | 指定Apache守护进程运行的用户。这应该是在`/etc/passwd`文件中指定的有效Linux用户组。您需要注意通过使用具有有限访问权限的用户来限制Apache守护进程的访问权限。通常，Apache守护进程以nobody身份运行。不要允许Apache以root用户身份运行，因为这可能会使交互式Web服务器功能（如CGI-BIN脚本）的用户以root用户身份访问您的系统，尤其是当CGI-BIN脚本编写不佳时。 |

#### 选择独立运行还是通过inetd运行Apache

Apache守护进程可以以独立模式运行，也可以通过`inetd`守护进程运行：

- 在独立模式下，Apache始终运行多个子Apache进程来处理传入请求。这些进程会持续一段时间，然后消亡并由新的子进程替换。
- 通过inetd运行时，不运行任何Apache进程。相反，inetd监听传入的Web连接，当有连接建立时，它会启动一个新的Apache进程。

模式的选择由`httpd.conf`文件中的`ServerType`指令定义。（请参阅表23.1。）

#### 配置Apache以通过`inetd`运行

如果您选择通过inetd运行Apache，如前面“选择独立运行还是通过inetd运行Apache”一节所述，则必须在`/etc/inetd.conf`文件中为Apache创建适当的条目。inetd的使用将在第13章“Linux网络配置和TCP/IP”中详细讨论。

对于Apache，请将以下条目添加到inetd.conf文件中：
```
