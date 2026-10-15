
server-status 页面也可以执行自动更新，以提供对服务器的实时监控。如果指定 URL `http://localhost/server-status?refresh=40`，则浏览器显示的 server-status 页面将每隔 40 秒更新一次。这允许浏览器窗口持续监控 Web 服务器的活动。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_933_0.png)

图 21-4：Apache server-status 页面显示通用的 Apache 信息，并报告单个服务器进程的活动。

默认情况下，只生成基本状态信息。如果你想生成完整的状态信息，需要通过取消取消以下行的注释来开启 `ExtendedStatus` 指令：

```
# ExtendedStatus: controls whether Apache will generate "full" status
# information (ExtendedStatus On) or basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.
#nExtendedStatus On
```

# 第 21 章：设置 Web 服务器

## 对 server-info 和 server-status 的进一步保护

由于 server-info 和 server-status 页面都包含不应让网络上的任何人访问的隐私信息，因此有几种额外的方法可以保护这些信息。你可以将这些信息限制为本地主机；然而，在某些环境中这可能并不实际。

如果你必须允许其他机器或网络访问此类详细的配置信息，请仅允许必要的机器访问，并且最好只允许你本地网络上的机器。此外，请注意，如果落入别有用手中，server-info 和 server-status 页面显示的信息可能会你的整台机器的安全更容易受到破坏。

更改用于引用上述两个页面的 URL 可能会有益。这是“通过模糊实现安全”的一个示例，虽然不应依赖它，但它可以让未经授权的人获取有关你 Web 服务器的信息变得稍微困难（特别是当你无法将连接限制在本地网络时）。要实现这一点，只需更改 `Location` 指令中的文件名，如下行所示：

```
<Location /server.information.page>
```

以及：

```
<Location /server.status.page>
```

## 记录错误

错误日志包含服务器生成的这些，描述了各种错误情况。`http.conf` 文件中的 `ErrorLog` 和 `LogLevel` 指令（如配置服务器部分所述）可以修改文件名和记录的信息。默认日志为 `/etc/httpd/logs/error_log`（指向 `/var/log/httpd/error_log` 的链接）。以下是错误日志中的几行示例：

```
Mon 28 10:29:13 [notice] Apache/2.2.4 (Fedora)
  configured resuming normal operations
Mon 28 10:43:07 [error] client [127.0.0.1] client denied by
  server configuration: /var/www/html/server-status
Mon 28 10:06:42 [error] client [127.0.0.1] File
  does not exist; /var/www/html/logfile.html
Mon 28 10:12:28 [notice] received SIGTERM, shutting down
```

第一行表示服务器刚刚启动，无论 `Log` 指令如何都会被记录。第二行表示记录了一个错误，用于演示一个被拒绝的请求。第三行显示了一个错误，代表对不存在的文件的请求。第四行同样不受 `LogLevel` 指令影响，表示服务器正在关闭。还应定期监控错误日志，因为它可能包含可能需要修复的 CGI 脚本的错误消息。

## 记录访问

每个传入的 HTTP 请求都会在传输日志中生成条目（默认认为 `/etc/httpd/logs/access_log`，指向 `/var/log/httpd/access_log` 的链接）。统计软件包和日志文件分析程序使用此文件，因为手动读取它是一项枯燥的工作。（请参见第 14 章中关于 logwatch 机制的信息）。

日志的格式可以通过 `httpd.conf` 文件中的 `LogFormat` 和 `CustomLog` 指令进行更改，正如在“配置 Web 服务器 (`httpd.conf`)”部分定义的那样。如果你尝试访问 `http://localhost/`（“common”格式，见图 21-1），则以下行（在“common”格式下）将是：access_log:

```
127.0.0.1 - [28/Apr/2008:02:23:33 -0600] "GET /HTTP/1.1" 403 3931 -"Mozilla/5.0 (X11; Linux i6686; rv:7.3) Gecko/20040102 Firefox/0.10.1"
127.0.0.1 - [28/Apr/2008:02:23:34 -0600] "GET /icons/powered_by.gif HTTP/1.1" 200 2414 -"Mozilla/5.0 (X11; Linux i6686; rv:7.3) Gecko/20040102 Firefox/0.10.1"
127.0.0.1 - [28/Apr/2008:02:23:44 -0600] "GET /icons/powered_by_fedora.png HTTP/1.1" 200 2243 -"Mozilla/5.0 (X11; Linux i6686; rv:7.3) Gecko/20040102 Firefox/0.10.1"
```

Test Page 实际上是一个错误状态 (403)，表示 Apache 服务器正在运行，但尚未添加主页。接下来的两行分别显示 server-info 和 server-status 页面（如图 21-3 和 21-4 所示）在测试页面生成了以下事件：

```
127.0.0.1 - [26/Apr/2008:23:40:41 -0400] "GET /server-info HTTP/1.1" 200 42632
127.0.0.1 - [26/Apr/2008:23:41:49 -0400] "GET /server-status HTTP/1.1" 200 1504
```

拒绝访问 server-status 页面的尝试记录了以下行（注意 403 响应码）：

```
127.0.0.1 - [26/Apr/2008:23:43:07 -0400] "GET /server-status HTTP/1.1" 403 211
```

## 分析 Web 流量

`webanalyzer` 软件包可以获取 Apache 日志并为你的服务器生成使用报告。这些报告以 HTML 格式创建，因此你可以显示图形化信息。信息将以表格和图表形式提供。

要使用 `webanalyzer`，必须安装 `webanalyzer` 软件包（`yum webanalyzer`）。你可以运行带有 `/etc/webanalyzer.conf` 文件中没有值的选项的 `webanalyzer` 来获取所需的信息。作为替代方案，可以使用命令行选项来覆盖 `webanalyzer.conf` 中的设置。要使用默认值，只需运行：

```
webanalyzer
```

如果一切顺利，该命令将运行片刻并静默退出。根据 `/etc/webanalyzer.conf` 文件的信息，将读取 `/var/log/httpd/access_log` 文件，并将 `index.html` 文件复制到 `/var/www/html/usage/` 目录。你可以通过任何浏览器打开文件来查看输出。例如，你可以在位置框中输入：

```
http://localhost/usage
```

输出报告显示了 Webanalyzer 活动的 12 个月总结。在柱状图中，每个月的蓝色条代表 Web 站的点击次数，深蓝色条显示不同文件的数量，浅蓝色条显示打开的页面数量。右列还显示了访问人数和访问网站数。同时也显示了传输的数据量（单位为 KB）。图 21-5 显示了一个运行几个月的 Web 服务器的 `webanalyzer` 输出文件示例。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_936_0.png)

## 第四部分：Fedora 和 RHEL 网络与服务器设置

图表下的表格显示了每月活动的每日和每月总结。用户可以点击月份名称查看详细活动。

> 提示：由于 Webanalyzer 同时支持常用日志格式 `CLF` 和合并日志格式，它可以用于显示 Apache 产生之外的日志文件信息。例如，你可以显示你的 FTP 服务器或 Squid 的统计数据。
