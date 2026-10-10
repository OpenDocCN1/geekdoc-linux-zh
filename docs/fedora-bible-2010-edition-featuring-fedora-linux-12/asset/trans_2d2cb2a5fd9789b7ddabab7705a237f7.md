

| 参数 | 描述 |
| :--- | :--- |
| | *directive*（指令）。 |
| -f *file* | 将 *file* 用作 ServerConfigFile 指令，而不是默认的 /etc/httpd/conf/httpd.conf。 |
| -h | 显示可用的命令行参数列表。 |
| -l | 列出在编译时链接到可执行文件的模块。 |
| -L | 打印可用于配置文件的指令的详细列表，并附带简短描述及包含该指令的模块。 |
| -S | 列出虚拟主机的配置设置。 |
| -t | 对配置文件进行语法检查。结果将是：语法正确或错误通知；例如：/etc/httpd/conf/httpd.conf 第 118 行存在语法错误 |
| -v | 打印版本信息：Server version: Apache/2.2.13 (Unix) Server built: Aug 21 2009 10:14:11 |
| -V | 列出版本信息及编译期间定义的任何值：Server version: Apache/2.2.13 (Unix) Server built: Aug 21 2009 10:14:11 Server's Module Magic Number: 20051115:23 Architecture: 32-bit ....... Server compiled with.... -D APACHE_MPM_DIR="server/mpm/prefork" -D APR_HAS_SENDFILE -D APR_HAS_MMAP . . . -D SERVER_CONFIG_FILE="conf/httpd.conf" |
| -k *option* | 使用 -k 与 start、stop、restart、graceful 或 graceful-stop 选项结合，以更改当前 Web 服务器的状态。 |

## 监控服务器活动

Apache Web 服务器是那些有恶意企图、想要劫持计算机的人极具吸引力的目标。这通常是因为服务器被放置在公共互联网上以响应客户端请求。鉴于互联网的开放性，如果你未能正确保护你的 Web 服务器，你很可能会成为攻击的目标。

你可以使用许多技术来保护你的服务器（详见第 13 章），从 SELinux 到证书，再到控制脚本的运行方式。然而，这里介绍的是监控 Apache Web 服务器性能和安全性的一些技术。仔细监控你的服务器通常可以在攻击造成严重损害之前将其阻止。

> **注意：** 如果你密切关注你的服务器，通常可以在攻击发生之前将其阻止。使用这里展示的技术来提供服务器状态的高层视图，然后深入检查日志文件以确保一切正常。寻找异常的减速、磁盘填满、大量请求或发送到你的服务器的请求中的异常模式。有关系统安全的更多信息，请参见第 13 章。

Apache 提供了两种独特的内置方法来检查 Web 服务器的性能和状态。`server-status` 处理程序可以配置为显示关于服务器进程的信息。`server-info` 处理程序可以配置为显示 Web 服务器配置的详细摘要。你可以通过在 `/etc/httpd/conf/httpd.conf` 文件中添加以下行来激活这些服务：

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>

<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>
```

在此示例中，来自本地计算机的所有用户都可以显示 `server-info` 和 `server-status` 页面。你可以将 `127.0.0.1` 更改为任何你的 Apache 服务器所托管的域名或主机名。

> **提示：** 如果你希望用户能够在 URL 中输入 `localhost`，你需要同时添加 `localhost` 和 `127.0.0.1`。

### 显示服务器信息

服务器信息（`server-info`）页面包含服务器版本信息和各种通用配置参数，并按模块拆分其余数据。每个已加载的模块都会列出，包括关于该模块支持的所有指令的信息，以及来自该模块的任何已定义指令的当前值。

服务器信息通常相当详细，包含的信息比图 20-3 中显示的多得多，该图仅显示了指向每个模块部分以及通用“服务器设置”部分的链接。

### 显示服务器状态

server-status 页面的内容包括服务器的版本信息、当前时间、服务器最后启动的时间戳以及服务器的运行时间。该页面还详细说明了每个服务器进程的状态，从几种可能的状态中进行选择（等待连接、刚刚启动、读取请求、发送响应、在达到 KeepAliveTimeout 定义的秒数前等待读取请求、执行 DNS 查找、记录交易或优雅退出）。

server-status 页面的底部按进程 ID（PID）列出每个服务器，并指示其状态，使用相同的可能值。图 20-4 显示了此页面的一个示例。

server-status 页面还可以执行自动更新，以提供更紧密的服务器监控。如果指定 URL http://localhost/server-status?refresh=40，则浏览器中显示的 server-status 页面将每 40 秒更新一次。这使得浏览器窗口可以完全用于持续监控 Web 服务器的活动。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_827_0.png)

图 20-3：server-info 页面显示服务器和模块信息。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_828_0.png)

**图 20-4：** Apache server-status 页面显示通用的 Apache 信息，并报告单个服务器进程的活动。

默认情况下，只生成基本状态信息。如果你希望生成完整的状态信息，请通过取消注释以下代码中的最后一行来启用 `ExtendedStatus` 指令：

```
# ExtendedStatus: controls whether Apache will generate "full" status
# information (ExtendedStatus On) or basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.
#
#ExtendedStatus On
```

### 进一步保护 server-info 和 server-status

由于 `server-info` 和 `server-status` 页面都包含不应让网络上任何人都能访问的私有信息，因此有几种额外方法可以保护这些信息。你可以将该信息限制为仅本地主机；然而，在某些环境中这可能不切实际。

如果你必须允许其他机器或网络访问如此详细的配置信息，请只允许必要的机器数量，最好仅限于你本地网络上的那些机器。此外，要意识到，如果落入坏人之手，`server-info` 和 `server-status` 页面显示的信息会使得你整个机器的安全性更容易被破解。

更改用于引用上述两个页面的 URL 也可能有益。这是“隐蔽安全”的一个例子，不应依赖它，但可以稍微增加未授权个人获取你 Web 服务器配置信息的难度（特别是如果你无法将这些连接限制在本地网络内）。要实现这一点，只需更改 Location 指令中的文件名，如以下行所示：

```
<Location /server.information.page>
```

以及：

```
<Location /server.status.page>
```

#### 记录错误

错误日志包含由服务器生成的描述各种错误条件的消息。httpd.conf 文件中的 ErrorLog 和 LogLevel 指令（如“配置服务器”章节所述）可以修改文件名以及记录的信息量。默认文件是 /etc/httpd/logs/error_log（它是 /var/log/httpd/error_log 的链接）。以下是错误日志中的几行示例：

```
[Mon Nov 23 10:29:13 2009] [notice] Apache/2.2.13 (Unix)
configured -- resuming normal operations
[Mon Nov 23 10:43:07 2009] [error] [client 127.0.0.1] client denied by server configuration: /var/www/html/server-status
[Mon Nov 23 10:06:42 2009] [error] [client 127.0.0.1] File does not exist: /var/www/html/newfile.html
[Mon Nov 23 01:12:28 2009] [notice] caught SIGTERM, shutting down
```

第一行表示服务器刚刚启动，并且无论 LogLevel 指令如何，都会记录在案。第二行表示一个已记录的错误，用以演示被拒绝的请求。第三行显示一个错误，代表对一个不存在文件的请求。第四行，同样无论 LogLevel 指令如何都会记录，表示服务器正在关闭。错误日志也应该定期监控，因为它将包含可能需要修复的 CGI 脚本的错误消息。

#### 记录访问

每个传入的 HTTP 请求都会在传输日志（默认为 /etc/httpd/logs/access_log，它是 /var/log/httpd/access_log 的链接）中生成一条条目。统计包和日志文件分析程序通常使用此文件，因为手动阅读可能是一项相当繁琐的任务。（有关 logwatch 设施的更多信息，请参见第 13 章。）

传输日志的格式可以通过 httpd.conf 文件中的 LogFormat 和 CustomLog 指令进行更改，如“配置 Web 服务器 (httpd.conf)”章节所述。如果你在按照安装步骤（见图 20-1）之后尝试访问 http://localhost/，那么以下行（采用“common”格式）将被写入 access_log：

