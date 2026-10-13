
在此示例中，`handsonhistory.com`域中的所有计算机都可以显示 `server-info` 和 `server-status` 页面。你可以将 `handsonhistory.com` 更改为 Apache 服务器托管的任何域名或主机。

# 显示服务器信息

服务器信息 (`server-info`) 页面包含服务器版本信息以及各种通用配置参数，并按模块将其余数据分开。每个加载的模块都会被列出，包含该模块支持的所有指令的信息，以及该模块中任何定义指令的当前值。

服务器信息通常非常详细，包含的信息比图 21-3 显示的得多，图 21-3 仅显示了每个模块部分的链接和通用服务器设置部分。

![](img/8aa80810fdd3df400bb7ee72b296baad_864_0.png)

图 21-3：`server-info` 页面显示服务器和模块信息。

# 显示服务器状态

`server-status` 页面的底部按进程 ID (`PID`) 列出每个服务器，并使用某些可能的值指示其状态。图 21-4 显示了此页面的示例。

`server-status` 页面还可以执行自动更新，以对服务器进行更密切的监控。如果指定 URL `http://localhost/server-status?refresh=40`，浏览器中显示的 `server-status` 页面将每 40 秒更新一次。这使得浏览器窗口可以完全用于持续监控 Web 服务器的活动。

![](img/8aa80810fdd3df400bb7ee72b296baad_865_0.png)

**图 21-4：** Apache 服务器状态页面显示通用 Apache 信息并报告单个服务器活动。

默认情况下，只生成基本状态信息。如果你想生成完整状态信息，你需要通过取消以下代码中的注释来启用 `ExtendedStatus` 指令：

```
# ExtendedStatus: 控制 Apache 在调用 "server-status"
# 时生成“完整”状态信息还是基本信息。默认是 Off。
```

# server-status 的进一步安全

由于 `server-info` 和 `server-status` 页面包含不应让任何人访问的信息，将其限制在本地网络可能是有益的。要实现这一点，只需更改以下行：

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from .localhost
</Location>
<Location /server-info>
  SetHandler server-info
  Order deny,allow
  Deny from all
  Allow from .localhost
</Location>
```

这是“模糊安全”的一种示例，不应依赖它，但可以增加未经授权获取获取服务器信息的难度。

# 记录错误

服务器生成的错误日志消息描述了各种错误状况。`httpd.conf` 中的 `ErrorLog` 和 `LogLevel` 指令可以修改文件名和记录的信息。默认文件是 `/etc/httpd/logs/error_log`（指向 `/var/log/httpd/error_log`）。以下是错误日志的几行示例：

```
[Thu Apr 28 10:29:13 2005] [notice] [client -] Apache/2.0.48 (Fedora) -- 恢复正常操作
[Thu Apr 28 10:43:07 2005] [error] [client_id] [client 127.0.0.1] 服务器拒绝访问:/var/www/html/server-status
[Thu Apr 28 10:06:42 2005] [error] [client_id] [client 127.0.0.1] 文件不存在：/var/www/html/newfile.html
[Thu Apr 28 10:12:28 2005] [notice] [client -] 捕捉到 SIGTERM，正在关闭
```

# 记录访问

每个传入的 HTTP 请求都会在传输日志中生成记录（默认位于 `/etc/httpd/logs/access_log`，指向 `/var/log/httpd/access_log`）。统计包和日志分析程序通常使用此文件，因为读取它是一项相当枯燥的任务。（参见第 14 章日志日志。）

传输格式可以通过 `httpd.conf` 文件中的 `LogFormat` 和 `CustomLog` 指令进行更改（如“配置 Web 服务器 (`httpd.conf`)”节所述）。如果你按照安装程序（图 21-1）尝试访问 `http://localhost/`，将以“common”格式写入 `access_log`：

```
127.0.0.1 - (28/Apr/2005:00:23:33 -0600) "GET / HTTP/1.1" 403 3931 "-Mozilla/5.0(X11; Ut; Linux 1686; rv:1.7.3) Gecko/20041002 Firefox/0.10.1"
127.0.0.1 - (28/Apr/2005:00:23:34 -0600) "GET /icons/apache_pb2.gif HTTP/1.1" 200
```

```
http://localhost/~Mozilla/5.0 (X11; U; Linux i686; rv:1.7.3)
Gecko/20041002 Firefox/0.0.1"
127.0.0.1 - - [28/Apr/2005:23:34-0600] "GET /icons/powered_by_fedora.png HTTP/1.1"
200 2243 - "http://localhost/"Mozilla/5.0 (X11; U; Linux i686; rv:1.7.3)
Gecko/20041002 Firefox/0.10.1"
```

Apache 测试页面是一个错误状态（403），表示 Apache 服务器正在运行，但服务器的管理员尚未添加主页。接下来两行分别显示了 Fedora Core 页面上显示的 Apache (`apache_pb2.gif`) 和 Fedora (`powered_by_fedora.png`) 图标。（RHEL 系统显示红色图标）。

查看 `server-info` 和 `server-status` 页面（分别如图 21-3 和 21-4 所示）生成了以下条目：

```
127.0.0.1 - [28/Apr/2005:23:40:41 -0400] "GET /server-info HTTP/1.1"
200 42632
127.0.0.1 - [28/Apr/2005:23:41:49 -0400] "GET /server-status HTTP/1.1"
200 15504
```

访问 `server-status` 页面的拒绝尝试记录了以下行（注意 403 服务器响应码）：

```
127.0.0.1 - [28/Apr/2005:23:43:07 -0400] "GET /server-status HTTP/1.1"
403 211
```

# 分析 Web 服务器流量

`webalizer` 软件包可以读取 Apache 日志文件并为服务器生成使用报告。这些报告以 HTML 格式创建，因此你可以以图形方式显示信息。信息以表格和图表的形式呈现。

要使用 `webalizer` 命令，必须安装 `webalizer` 软件包。你可以不带任何选项运行 `webalizer`，它将读取 `/etc/webalizer.conf` 文件中的值来获取所需信息。作为替代方案，你可以使用命令行选项来覆盖 `webalizer.conf` 文件中的设置。要使用默认设置，只需运行以下命令：

```
# webalizer
```

如果一切顺利，该命令将运行片刻并静默退出。由于读取了 `/etc/webalizer.conf` 文件中的信息以及 `/var/log/httpd/access_log` 文件，一个 `index.html` 文件会被复制到 `/var/www/html/usage/` 目录。你可以通过任何浏览器窗口打开该文件来查看输出。例如，你可以在位置框中输入以下内容：

```
http://localhost/~usage
```

输出报告显示了 Web 服务器 12 个月的活动总结。在图表中，每个月的绿色条形代表网站的点击次数，深蓝色条显示命中的不同文件数量，浅蓝色条显示打开的页面数量。右侧列还显示了访问次数和访问站点数量的数据。同时也显示了以 KB 计算的数据传输量。

# 第 21 章：设置 Web 服务器

图 21-5 显示了一个运行几个月的 Web 服务器的 `webalizer` 输出文件示例。

![](img/8aa80810fdd3df400bb7ee72b296baad_868_0.png)

图 21-5：`Webalizer` 以列和行的格式显示 Web 数据。

在图表下方，表格显示了每个月活动的每日和每月统计数据。用户可以点击站点名称查看详细活动情况。
