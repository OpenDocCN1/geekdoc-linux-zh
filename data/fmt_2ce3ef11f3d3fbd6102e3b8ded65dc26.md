
在此示例中，`handsonhistory.com`域中的所有计算机都可以显示这些页面。你可以将`handsonhistory.com`更改为你选择的域名。

## 显示服务器信息

`server-info`处理器可以配置为显示 Web 服务器配置的详细摘要。`server-status`处理器可以配置为显示有关服务器进程的信息。服务器信息（`server-info`）页面包含服务器版本信息和各种通用配置参数，并按模块划分数据。每个加载的模块都会列出，并带有该模块支持的所有指令以及这些指令的当前值。

服务器信息通常非常详细，包含的信息比图 21-2 显示的多，图 21-2 仅显示每个模块的链接和通用设置部分。

img/176fafece2d30daee750bc07e89ee4_789_0.png

图 21-2：`server-info`页面显示服务器信息

## 显示服务器状态

`server-status`页面底部按进程 ID (`PID`) 列出每个服务器，并使用可能的值指示其状态。图 21-3 是该页面的示例。

img/176fafece2d30daee750bc07e89ee4_789_1.png

图 21-3：Apache 服务器状态页面显示通用 Apache 信息并报告单个服务器进程活动。

`server-status`页面还可以执行自动更新以提供更密切的监控。如果指定 URL `http://localhost/server-status?refresh=40`，浏览器中显示的`server-status`页面将每 40 秒更新一次。这允许一个浏览器窗口专门用于持续监控服务器的活动。

## `server-info`和`server-status`的进一步安全

由于`server-info`和`server-status`页面包含不应让网络上的任何人访问的隐私信息，因此有几种额外的方法来保护这些信息。你可以将这些信息仅限于本地主机；但在某些环境中，这可能并不实际。

如果你必须允许其他机器或网络访问此类详细的配置信息，请仅允许尽可能少的机器，并且只允许你本地网络上的机器。此外，请注意，如果落入别有用手中，`server-info`和`server-status`页面显示的信息可能会使整个网络安全更容易受到威胁。图 21-4 显示了向没有权限访问`server-status`页面的用户应显示的错误消息。

img/176fafece2d30daee750bc07e89ee4_790_0.png

图 21-4：拒绝`server-status`以及对外部网络主机的访问，甚至可能拒绝除本地以外的任何机器。

## 记录错误

第一行包含服务器生成的消息，描述了各种错误状况。虽然错误日志的格式无法自定义，但 `httpd.conf` 文件中的 `ErrorLog` 和 `LogLevel` 指令（如在“配置服务器”章节中所述）可以修改文件名和记录的信息量。默认文件为 `/etc/httpd/logs/error_log`（它是 `/var/log/httpd/error_log` 的链接）。下面显示了错误日志中的几行示例：

```
Wed Aug 23 10:29:13 2000 [notice] Apache/1.3.12 (Unix) (Red Hat/Linux)
configured - resuming normal operations
Wed Aug 23 10:43:07 2000 [error] [client 127.0.0.1] client denied by server configuration: /home/httpd/html/server-status
Sat Aug 26 10:06:42 2000 [error] [client 127.0.0.1] does not exist: /home/httpd/html/newfile.html
Sat Aug 26 01:12:28 2000 [notice] caught SIGTERM, shutting down
```

第一行表示服务器刚刚启动，无论 `LogLevel` 指令如何都会被记录。第二行表示一个记录的错误，用于演示被拒绝的请求（见图 21-4）。第三行显示了一个文件不存在的错误。第四行同样无论 `LogLevel` 指令如何都会记录，表示服务器正在关闭。应该定期监控错误日志，因为它还包含可能需要修复的 CGI 脚本错误消息。

## 记录传输

每个 HTTP 请求都会在传输日志中生成条目（默认路径 `/etc/httpd/logs/access_log`，它是 `/var/log/httpd/access_log` 的链接）。统计包和日志文件分析程序通常使用此文件，因为手动读取它是一项相当繁琐的任务。可以通过 `httpd.conf` 文件中的 `LogFormat` 和 `CustomLog` 指令修改传输日志（如“配置服务器”章节中所述）。如果你按照安装步骤（见图 21-1）尝试访问 `http://localhost/`，以下行（采用“common”格式）将被写入 `access_log`：

```
127.0.0.1 - [23/Aug/2000:23:32:28 -0400] GET /HTTP/1.0" 200 195
127.0.0.1 - [23/Aug/2000:23:32:36 -0400] GET /poweredby.gif HTTP/1.0" 200 1817
127.0.0.1 - [23/Aug/2000:23:32:36 -0400] GET /icons/apache_pb.gif HTTP/1.0" 200 236
```

## Red Hat Linux 可用的统计包

手动分析传输日志并无趣。已经编写了几个包来自动化此任务，其中一些在下文中进行了描述。这只是 Red Hat Linux 可用程序的一小部分采样：

- Analog 4.1 - 这是一个免费的日志分析器非常快且易于配置，并产生非常详细的输出（包括条形图和超链接）。更多信息可以在 http://www.stat.cam.ac.uk/-sretl/analog/ 找到。
- Webizer 1.3 - 另一个快速免费的日志分析程序，Webizer 具有超链接以及彩色图表和饼图。详情可以在 http://www.mrunix.net/webalizer/ 找到。
- Wuage 7.0 - 该统计程序的输出详细、图形化且极可配置。30 天试用版可以下载，但完整版价格在 $75（单服务器许可）到 $295（多服务器许可）之间。详情请访问 http://www.bouteill.com/usage/。

查看 `server-info` 和 `server-status` 页面（分别见图 21-2 和 21-3）分别生成了以下事件：

```
127.0.0.1 - [23/Aug/2000:23:40:21 -0400] GET /server-info/1.0* HTTP/1.0 200 32
127.0.0.1 - [23/Aug/2000:23:41:49 -0400] GET /server-status/1.0* HTTP/1.0 200 54
```

拒绝访问 `server-status` 页（见图 21-4）记录了以下行（注意 403 响应）：

```
127.0.0.1 - [23/Aug/2000:23:43:07 -0400] GET /server-status/1.0* HTTP/1.0 403 21
```
