
如果 `HostnameLookups` 指令开启，每个传入连接都将生成一个 DNS 查找，以将客户端的 IP 地址转换为主机名。如果您的站点收到大量请求，服务器的响应时间可能会受到不利影响。除非您使用需要完全限定域名且无法自行执行查找的日志文件分析程序或统计软件包，否则应关闭 `HostnameLookups`。随 Apache 发行版安装的 `logresolve` 程序可以计划在非高峰时段通过执行主机名查找来编辑日志文件。

## 配置 HTTP 日志记录

您可以设置几个与 Apache 信息日志记录相关的值。当显示相对路径名时，将追加 `/etc/httpd` 目录（例如，`/etc/httpd/logs/error_log`）。如下例所示，您可以设置错误日志的位置、日志警告级别以及一些日志昵称：

```
#    ErrorLog: The location of the error log file.
#    If you do not specify an ErrorLog directive within a <VirtualHost>
#    container, error messages relating to that virtual host will be
#    logged here.  If you *do* define an error logfile for a <VirtualHost>
#    container, that host's errors will be logged there and not here.
#
ErrorLog logs/error_log

#    LogLevel: Control the number of messages logged to the error_log.
#    Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
# LogLevel warn

# The following directives define some format nicknames for use with
# a CustomLog directive (see below).
LogFormat "%h %l %u %t "%r" %>s %b "%{Referer}i""%{User-Agent}i""combined
LogFormat "%h %l %u %t "%r" %>s %b" common
LogFormat "%{Referer}i -> %U" referer
LogFormat "%{User-agent}i" agent

#
# Location and format of the access logfile (Common Logfile Format).
# If you do not define any access logfiles within a <VirtualHost>
# container, they will be logged here. Contrariwise, if you *do*
# define per-<VirtualHost> access logfiles, transactions will be
# logged therein and *not* in this file.
#
# CustomLog /var/log/httpd/access_log common
CustomLog logs/access_log combined

#
# If you would like to have agent and referer logfiles, uncomment the
# following directives.
#
#CustomLog /var/log/httpd/referer_log referer
#CustomLog /var/log/httpd/agent_log agent
CustomLog logs/agent_log agent

#
# If you prefer a single logfile with access, agent, and referer
# information
# (Combined Logfile Format) you can use the following directive.
#
#CustomLog /var/log/httpd/access_log combined
```

前面的几行处理服务器错误、客户端跟踪信息和传入请求的日志记录方式。`ErrorLog` 指令可以指定绝对路径或相对于 `ServerRoot` 的路径名（默认为 `/etc/httpd`），指示服务器应存储错误消息的位置。在这种情况下，指定的文件是 `logs/error_log`，它扩展为 `/etc/httpd/logs/error_log`（实际上是指向 `/var/log/httpd` 目录中 `error_log` 文件的链接）。

`LogLevel` 指令控制出现在错误日志中的消息的严重程度和数量。消息范围可以从特别详尽的 `debug` 日志级别到尤其是静默的 `emerg` 日志级别。使用 `debug` 级别时，每当读取配置文件、使用访问控制机制或活动服务器数量发生变化时，都会记录一条消息。使用 `emerg` 级别时，只有严重的系统级故障才会使服务器进入恐慌状态。

`LogLevel` 指令指定的级别表示将被记录的最轻微的消息——该严重级别及以上的所有消息都会被记录。例如，如果 `LogLevel` 设置为 `warn`，则错误日志将包含 `warn`、`error`、`crit`、`alert` 和 `emerg` 级别的消息。默认值 `warn` 是正常使用的良好选择（它只记录可能需要操作员干预的重要事件），但 `info` 和 `debug` 级别非常适合测试服务器配置或追踪错误的确切位置。

四个 `LogFormat` 行定义（以供后续使用）了四种日志文件格式：`combined`、`common`、`referer` 和 `agent`。`LogFormat` 指令中可用的令牌在表 21-5 中进行了描述。`LogFormat` 定义可以根据个人偏好进行修改，也可以根据需要创建其他自定义格式。

### 表 21-5：LogFormat 中可用的令牌

| 令牌 | 描述 |
|---|---|
| `%a` | 客户端机器的 IP 地址。 |
| `%b` | 发送给客户端的字节数（不包括头部信息）。 |
| `%(VAR)e` | 环境变量 `VAR` 的内容。 |
| `%f` | 请求 URL 引用的文件名。 |
| `%h` | 客户端机器的主机名。 |
| `%(Header)i` | HTTP 请求中指定头行的内容。 |
| `%l` | 如由 `identd` 守护进程报告（如果可用），发起请求的客户端机器上的用户。 |
| `%(Note)n` | 来自其他模块的消息 `Note` 的内容。 |
| `%(Header)o` | HTTP 响应中指定头行的内容。 |
| `%p` | 接收请求的端口号。 |
| `%P` | 处理请求的服务器进程的 PID。 |
| `%r` | 来自客户端的实际 HTTP 请求。 |
| `%s` | 请求生成的服务器响应代码。 |
| `%t` | 当前本地时间和日期。可以使用 `%(Format)t` 改变时间格式，其中 `Format` 在 `strftime(3)` 手册页中描述。 |
| `%T` | 满足客户端请求所需的秒数。 |
| `%u` | 如果访问控制规则要求用户名/密码认证，这代表客户端提供的用户名。 |
| `%U` | 客户端请求的 URL。 |
| `%v` | 服务器的主机名和域名（根据 DNS，Domain Name System）。 |
| `%V` | 根据 `ServerName` 指令，处理请求的服务器的主机名和域名。 |

`common` 格式包括客户端主机名或 IP 地址、由 `ident` 守护进程和服务器认证方法报告的用户名（如果适用）、请求发生时的本地时间、实际 HTTP 请求、服务器响应代码以及传输的字节数。这种格式是 Web 服务器（以及最近甚至 FTP 服务器）中事实上的标准。

为了便于连接追踪，`referer` 格式存储了链接到刚刚交付的文档的 URL（来自同一网站或外部服务器，相对于 *ServerRoot*）。例如，如果页面 `http://www.redhat.com/corp/about_us.html` 包含指向位于 `http://www.mybox.com/linuxguy/bio.html` 的主页的链接，当客户端访问该链接时，`www.mybox.com` 上的 `referer` 日志将如下所示：

```
http://www.redhat.com/corp/about_us.html -> /linuxguy/bio.html
```

此信息可用于确定每个客户端到达您网站的路径。

`agent` 格式存储每个传入连接的 *User-agent: HTTP* 头的内容。此字段通常指示浏览器名称和版本、语言以及运行浏览器的操作系统或架构。在运行 Red Hat 7 的 Pentium II 上，Netscape 将生成以下条目：
