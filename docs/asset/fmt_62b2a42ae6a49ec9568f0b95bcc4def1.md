
# 838 第四部分：Red Hat Linux 网络和服务器设置

Apache 可以作为代理服务器、缓存服务器或两者的结合。
如果 `ProxyRequests` 设置为 `off`，服务器将仅缓存文件而不充当代理。
`CacheRoot`（指定用于存放缓存文件的目录）未定义，或者如果 `NoCache` 设置为 `*`，则不会执行任何缓存。代理和缓存服务默认都是关闭的（已注释掉）。

如果你开启了该功能，`CacheRoot` 应该存在于具有可用空间的文件系统上，以容纳缓存，缓存受 `CacheSize` 指令限制。然而，在文件系统缓存清理中，你有 20 到 40% 的额外空间可用来维持 `CacheSize`（以 KB 为单位），这仅按 `CacheInterval` 指令指定的定期发生。

`CacheMaxExpire` 指令表示文档在不检查原始文档是否有修改的情况下，在缓存中存在的最大小时数。
`CacheLastModifiedFactor` 适用于没有过期时间的文档，即使协议支持过期时间。要制定一个过期日期，将该因子（一个浮点数）乘以自文档上次修改以来的小时数。例如，如果文档在三天前修改过，且 `CacheLastModifiedFactor` 为 `0.25`，则文档将在 18 小时后从缓存中过期（只要该值仍为 `CacheMaxExpire` 的值）。

`CacheDefaultExpire` 指令（指定文档过期前的小时数）适用于通过不支持过期时间的协议接收到的文档。
`NoCache` 指令包含一个用空格分隔的 IP 地址、主机名或主机名中的关键词列表，这些文档不应被缓存。

如果让你在 `/etc/httpd/proxy` 中保留最多 24 小时，缓存服务器的行为如下：

- 缓存文件将在 `/etc/httpd/proxy` 中保留最多 24 小时，尽管服务器会每四小时执行一次垃圾回收（缓存清理），以确保缓存包含的数据少于 5K。
- 通过不支持过期时间的协议（例如，匿名 FTP）接收的文档将在一小时后过期，而没有过期时间的文档（即使协议支持过期时间，如 HTTP）将使用 `CacheLastModifiedFactor` 来确定文档何时从缓存中过期（这里是 1 小时，即 6 分钟）。
- 来自 `a_domain.com`、`another_domain.edu` 和 `joes.garage_sale.com` 域名的文档不会被缓存。

你可能希望允许更大的 `CacheSize`，并可能使用更短的 `CacheGcInterval`，但除此之外提供的值是合理的。记住，`CacheGcInterval` 的值可以是一个浮点数（例如，`1.25` 表示 75 分钟）。

## 配置虚拟主机

如果你有一台 Web 服务器计算机，但有多个想要通过这台计算机提供服务的域名，你可以将 Apache 设置为虚拟主机。通过虚拟主机，单个 IP 地址可以作为多个域名的访问点。

使用虚拟主机时，当请求从 Web 浏览器通过你计算机上的特定 IP 地址进入你的 Apache 服务器时，Apache 会检查请求的域名并显示与该域名关联的内容。作为支持虚拟主机的 Web 服务器的管理员，你必须确保为你的虚拟主机配置的所有内容都已设置（你必须定义 Web 内容位置、日志文件、管理员联系人等内容）。

虚拟主机通过 `VirtualHost` 标签定义。`/etc/http/conf/httpd.conf` 文件中与虚拟主机相关的信息见以下代码：

```
### 第 3 节：虚拟主机
```

## 启动和停止服务器

启动和停止 Apache 服务器的过程与许多服务器进程相同。安装 `apache` 包会创建 `/etc/init.d/httpd` 文件，你可以使用 `chkconfig` 在 `/etc/rc.d` 目录中创建适当的链接。

> **交叉引用：** 请参第 12 章，有关控制启动和停止守护进程及服务器的脚本内部机制的详细信息。

`/etc/init.d/httpd` 接受五个命令行参数之一。如果使用参数 `start` 调用，`httpd` 脚本将运行一个守护进程（由“root”所有），该进程将由 `apache` 用户（来自 `User` 和 `Group` 指令）生成其他守护进程（数量由 `StartServers` 指令指定）。这些进程负责响应传入的 HTTP 请求。如果使用 `stop` 作为命令行参数，服务器将关闭并终止所有 `httpd` 进程。

如果给出 `restart` 命令行参数，脚本将按顺序执行停止和启动程序。使用 `reload` 作为参数将发送挂起信号 -

| 参数 | 说明 |
|---|---|
| `-c 指令` | 读取配置文件并处理该指令。这可能会覆盖配置文件中对该指令的定义。 |
| `-C 指令` | 先处理该指令再读取配置文件。该指令可能会更改配置文件的评估，但也可能被配置文件中的另一个定义覆盖。 |
| `-d 目录` | 使用目录作为 `ServerRoot` 指令，指定模块、配置和日志文件目录的位置。 |
| `-D 参数` | 定义用于 `IfDefine` 指令中条件评估的参数。 |
| `-f 文件` | 使用文件作为 `ServerConfigFile` 指令，而不是使用默认的 `/etc/httpd/conf/httpd.conf`。 |
| `-h` | 显示可能的命令行参数列表。 |
| `-l` | 列出编译时链接到可执行文件中的模块： |
| `-L` | 打印可以在配置文件中使用的指令详细列表，并附带简短描述以及包含每个指令的模块。 |
| `-S` | 列出虚拟主机的配置设置。 |
| `-t` | 对配置文件进行语法检查。结果将是：Syntax OK 或（例如）：Syntax error on line 118 of /etc/httpd/conf/httpd.conf: |
| `-T` | 与 `-t` 相同，但不对 `DocumentRoot` 的值进行检查。 |

# 表 21-7（续）

| 参数 | 说明 |
| --- | --- |
| `-v` | 打印版本信息：Server version: Apache/1.3.12 (Unix) (Red Hat/Linux) Server built: Aug 7 2000 06:20:48 |
| `-V` | 列出版本信息以及编译期间定义的任何值：Server version: Apache/1.3.12 (Unix) (Red Hat/Linux) Server built: Apr 7 2000 06:20:48. Server's Module Magic Number: 19990320:7. Server compiled with.... -D EAPI -D HAVE_MMAP -D HAVE_SHMGET -D USE_SHMGET_SCOREBOARD -D USE_MMAP_FILES -D USE_FCNTL_SERIALIZED_ACCEPT -D HTTPD_ROOT="/usr" -D SUEEXEC_BIN="/usr/sbin/suexec" -D DEFAULT_PIDLOG="/var/httpd/httpd.pid" -D DEFAULT_SCOREBOARD="/var/httpd/httpd.scoreboard" -D DEFAULT_LOCKFILE="/var/httpd/httpd.lock" -D DEFAULT_XFERLOG="/var/log/httpd/access_log" -D DEFAULT_ERRORLOG="/var/log/httpd/error_log" -D TYPES_CONFIG_FILE="/etc/httpd/conf/mime.types" -D SERVER_CONFIG_FILE="/etc/conf/httpd.conf" -D ACCESS_CONFIG_FILE="/etc/conf/access.conf" -D RESOURCE_CONFIG_FILE="/etc/httpd/srm.conf" |
| `-X` | 仅启动单个主守护进程，不会产生其他 httpd 进程。这应该仅用于测试目的。 |

## 监控服务器活动

Apache 提供了两种独特的内置方法来检查 Web 服务器的性能。`server-status` 处理器可以配置为显示服务器进程的信息。`server-info` 处理器可以配置为显示 Web 服务器配置的详细摘要。你可以通过分别向 `/etc/httpd/conf/httpd.conf` 文件添加以下行来激活这些服务：

```
<Location /server-status>
  SetHandler server-status
  order deny,allow
  deny from all
  allow from handhistory.com
</Location>

<Location /server-info>
  SetHandler server-info
  order deny,allow
  deny from all
  allow from handhistory.com
</Location>
```

在此示例中，`handhistory.com` 域中的所有计算机都可以显示 `server-info` 和 `server-status` 页面。你可以将 `handhistory.com` 更改为 Apache 服务器托管的任何域名或主机名。

## 显示服务器信息

服务器信息（`server-info`）页面包含服务器版本信息以及各种通用配置参数，并按模块划分其余数据。每个加载的模块都会被列出，并包含该模块支持的所有指令的信息，以及该模块中定义的任何指令的当前值。

服务器信息通常非常详细，包含的信息比图 21-2 显示的多得多，图 21-2 仅显示了指向每个模块部分的链接和通用服务器设置（Server Settings）部分。

# 844 第四部分：红帽 Linux 网络和服务器设置

![](img/9fef5c8304e11e92fef0da9b18dad7b1_865_0.png)

图 21-2：`server-info` 页面显示服务器和模块信息。

## 显示服务器状态

`server-status` 页面的内容包括服务器的版本信息、服务器最后启动的时间戳以及服务器的运行时间。该页面还详细列出了每个服务器进程的状态，这些状态来自几种可能的状态（等待连接、正在启动、读取请求、发送响应、退出前等待读取请求）。

`server-status` 的底部列出了每个进程（PID）并指示其状态。图 21-3 是此示例![](img/9fef5c8304e11e92fef0da9b18dad71_865.1)

# Apache 状态

Server version: Apache/1.3.12 (Unix) (Red Hat/Linux)
Server built: Apr 7 2000 06:20:48
Current Time: Thu, Aug 15 10:53:25 2002
Uptime: 0:00:00
Requests currently processed: 3

# 第21 章：设置 Web 服务器

`server-status` 页面还可以自动更新服务器。如果你无法将连接限制在本地网络，可以使用 `KeepAlive` 参数指定服务器等待新请求的秒数。

默认只生成基本状态。如果你想生成完整状态，需要取消 `httpd.conf` 文件中 `ExtendedStatus` 行的注释：

```
# ExtendedStatus Off
ExtendedStatus On
```

启用 `ExtendedStatus` 后，`server-status` 页面提供更多详细的信息，包括关于客户端、处理请求以及服务器 CPU 使用的情况。

## server-status 安全

`server-status` 和 `server-info` 页面包含不应被任何人访问的敏感信息。将访问限制在本地网络是非常重要的。你可以像下面所示实现：

```
<Location /server-status>
  SetHandler server-status
  order deny,allow
  deny from all
  allow from localhost
</Location>

<Location /server-info>
  SetHandler server-info
  order deny,allow
  deny from all
  allow from localhost
</Location>
```

`server-status` 页面还可以用于监控服务器的状况。通过跟踪处理的请求和 CPU 使用情况，你可以判断服务器是否过载或是否需要扩展。

# 846 第四部分：红帽 Linux 网络和服务器设置

![](img/9fef5c8304e11e92fef0da9b18dad7b1_867_0.png)

图 21-4：外部网络访问 `server-status` 和 `server-info`。

## 记录错误

`ErrorLog` 包含服务器生成的描述各种错误状况的消息。`httpd.conf` 中的 `ErrorLog` 和 `LogLevel` 指令（在配置服务器部分描述）可以修改文件名和日志量。默认文件是 `/etc/logs/error_log`（它是 `/var/log/httpd/error_log` 的链接）。错误日志的几个示例所示：

```
[Thu Aug 15 10:29:13 2002] [notice] Apache/2.0.36 (Red Hat/Linux)
  configured -- resuming normal operations
[Thu Aug 15 10:43:07 2002] [error] [client 127.0.0.1] client denied by
server configuration: /var/www/html/server-status
[Thu Aug 15 10:06:42 2002] [error] [client 127.0.0.1] File
  does not exist: /var/www/html/newfile.html
[Thu Aug 14 01:12:28 2002] [notice] caught SIGTERM, shutting down
```

## 第21 章：设置 Web 服务器 847

第一行表示服务器刚刚启动，且无论 `LogLevel` 指令如何设置都会记录。第二行显示了一个记录的错误，用于演示被拒绝的请求（见图 21）。第三行显示了一个错误，代表对一个不存在的文件的请求。第四行同样不受 `LogLevel` 指令限制，它表示服务器正在关闭。应该定期监控错误日志，因为其中包含了可能需要修复的 CGI 脚本的错误信息。

## 记录传输

每个传入的 HTTP 请求都会在传输日志中生成一个条目（默认）。

传输日志的格式可以通过 `httpd.conf` 文件中的 `LogFormat` 和 `CustomLog` 指令进行更改（在“配置服务器”章节中描述）。如果你按照安装程序（见图 21-1）尝试访问 `http://localhost/`，以下几行（“common”格式）将被写入 `access_log`：

```
127.0.0.1 - - [15/Aug/2002:23:32:28 -0400] "GET /HTTP/1.1" 200 1945
127.0.0.1 - - [15/Aug/2002:23:32:36 -0400] "GET /powered_by.gif HTTP/1.1*" 200 1817
127.0.0.1 - - [15/Aug/2002:23:32:36 -0400] "GET /icons/apache_pb.gif HTTP/1.1*" 200 2326
```

查看 `server-info` 和 `server-status` 页面（分别图 21-2 和 21-3）会生成以下条目：
