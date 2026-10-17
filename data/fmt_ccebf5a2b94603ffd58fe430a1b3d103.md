
TransferLog `logs/access.log`

当参数为通往外部程序的管道时，日志信息将发送到该外部程序的标准输入 (`STDIN`)。

请注意，如果虚拟主机 `VirtualHost` 继承了主服务器的 `TransferLog`，则不会为其启动新程序。如果使用了程序，则它将在启动 `httpd` 的服务器用户下运行。如果服务器是由 `root` 启动的，则为 `root`。请确保该程序是安全的。

LogFormat `[nickname]`

此指令设置由 `TransferLog` 指令指定的默认日志文件格式。默认值值为 `"%h %l %u %r\" %s %b"`。如果您在指令行上为格式包含了一个昵称（`nickname`），则您可以在其他 `LogFormat` 和 `CustomLog` 指令中使用它，而无需重复整个格式字符串。定义了昵称的 `LogFormat` 指令不起作用——也就是说，它只定义了昵称，而不会实际应用该格式。

CustomLog `file-pipe-or-nickname`

与 `TransferLog` 指令类似，此指令允许您将日志信息发送到日志文件或外部程序。然而，与 `TransferLog` 指令不同，它允许您使用可以作为参数指定的自定义日志格式。

参数格式指定了日志文件中每一行的格式。该格式的可用选项与 `LogFormat` 指令的参数完全相同。如果格式包含任何空格（在几乎所有情况下都是如此），则应该用双引号括起来。

您可以使用 `LogFormat` 指令定义的格式昵称，而不是实际的格式字符串。

昵称仅适用于 Apache 1.3 或更高版本。此外，`TransferLog` 和 `CustomLog` 指令可以在每个服务器中使用多次，以导致每个请求都记录到多个文件中。

CookieLog `filename`

`CookieLog` 指令设置记录 cookie 的日志文件名。文件名相对于 `ServerRoot`。包含此指令仅是为了与已弃用的 `mod_cookies` 兼容；因此，不建议使用此指令。请改用用户跟踪模块（user-tracking module）的指令。本章稍后部分将讨论用户跟踪模块 `mod_usertrack`。

# 第 12 章：Web 服务

## 自定义服务器日志文件

尽管 CLF 满足了大多数日志需求，但有时能够自定义日志数据是很有用的。例如，您可能希望记录访问您网站的浏览器的类型，以便您的 Web 设计团队确定应该避免或使用什么类型的特定浏览器的 HTML。或者，您可能想知道哪些网站将访问者引导（即，引用）到了您的网站。所有这些内容在 Apache 中都可以轻松实现。默认日志模块 `mod_log_config` 支持自定义日志。

自定义格式通过模块的 `LogFormat` 和 `CustomLog` 指令设置。`LogFormat` 和 `CustomLog` 的格式参数是一个字符串。该字符串可以同时包含字面字符和特殊的 `%` 标识符。当字符串中使用字面值时，它们会被复制到每个请求的日志文件中。然而，`%` 标识符会被替换为相应的值。特殊的 `%` 标识符有：

- `%b`：发送的字节数，不包括 HTTP 头部
- `%f`：请求的文件名
- `%{variable}`：环境变量 `VARIABLE` 的内容
- `%h`：发出请求的远程主机
- `%{IncomingHeader %}`：`IncomingHeader` 的内容——即，发送到服务器的请求中的头部行(行)。末尾的 `i` 字符表示这是客户端（入站）头部。
- `%l`：如果启用了 `IdentityCheck` 指令且客户端机器运行了 `ident`，则这是由客户端报告的身份信息。
- `%{u}`：如果请求的 URL 需要成功的 HTTP 身份验证，则用户名是该标记的值。
- `%u`：请求路径
- `%v`：服务器或虚拟主机名称
- `%{OutgoingHeader %}`：`OutgoingHeader` 的内容——即回复中的头部行(行)。末尾的 `o` 字符表示这是服务器（出站）头部。
- `%p`：服务请求的端口
- `%P`：处理请求的子进程 ID
- `%r`：请求的第一行
- `%s`：服务器对请求返回的状态。注意，当请求被重定向时，此标识符的值仍为原始状态。如果你想存储重定向后的状态，请使用 `%{->`

## 第四部分：设置内网/互联网服务

- `%t`：请求时间。时间格式与 CLF 相同。
- `%{%t}`：按给定格式的时间（你可以查看 `strptime`）。
- `%U`：服务请求所需的时间（秒）
- `%U`：如果请求的 URL 需要成功的 HTTP 身份验证，则用户名是该标记的值。
- `%u`：请求路径
- `%v`：服务器或虚拟主机名称

可以在前面的规格中包含默认条件信息。条件可以是特定状态码的存在（或不存在）。例如，假设您想记录所有将用户引导至不存在页面的引用 URL。在这种情况下，服务器会产生 404 (未找到) 头部。为了记录这些引用 URL，您可以使用格式标识符：

```
%404 %Referer'
```

同样，为了记录导致异常状态的引用 URL，您可以使用：

```
%!200,304,302(%Referer)'
```

注意使用 `!` 字符表示服务器状态列表的缺失。同样，为了在 CLF 格式标识符的末尾包含额外信息，您可以扩展 CLF 格式，其定义字符串为：

```
%h %u %t \"%r\" %s %b
```

例如：

此规格记录 CLF 格式数据，并在每个日志目中添加客户端头部头部 `Referer` 和用户信息。

## 使用错误日志

如果不记录错误，您将无法确定问题所在以及错误发生在哪里。有趣的是，Apache 核心支持错误日志。`ErrorLog` 指令允许您记录 Apache 遇到的所有类型的错误。您可以指定一个文件名，或者使用 `syslog` 守护进程 (`syslogd`) 来记录所有错误。例如：

### 第12 章：Web 服务

`ErrorLog /logs/error_log`

在这里，Apache 将把错误消息写入 `/logs/error_log` 文件。如需记录日志，请使用 `syslog` 设施，使用：

`ErrorLog syslog`

使用 `LogLevel` 指令，你可以指定 Apache 应该发送到 `syslog` 的消息类型。例如：

```
ErrorLog syslog
LogLevel debug
```

在这里，Apache 被指令将调试消息发送到 `syslog`。如果你想通过 `syslog` 将调试消息存储在不同的文件中，你需要修改 `/etc/syslog.conf`。例如：

```
*.debug /var/log/debug
```

在 `/etc/syslog.conf` 中添加此行，重启 `syslogd` (`killall -HUP syslogd`)，Apache 将允许你将所有 Apache 调试消息存储到 `/var/log/debug` 文件中。请注意，你可以将 `LogLevel` 设置为以下任何设置之一：

- `emerg`: 紧急消息

如果你想在更新发生时查看 `syslog` 或任何日志文件的更新，可以使用 `tail` 工具并配合 `-f /path/to/log` 选项。

## 分析服务器日志文件

有很多第三方 Web 日志分析工具。大多数工具都要求日志文件采用 CLF 格式，因此请确保你的日志中具有 CLF 格式。以下是一些工具以及你可以在哪里找到它们：

- `WebTrends`: http://www.webtrends.com/
- `Usage`: http://www.bouteell.com/usage/
- `wwwstat`: http://www.ics.uci.edu/pub/websoft/wwwstat/
- `http-analyze`: http://www.netstore.de/Supply/http-analyze/
- `pwebstats`: http://www.inimelb.edu.au/pwebstats.html
- `WebStat Explorer`: http://www.webstat.com/
- `AccessWatch`: http://netpressure.com/accesswatch/

发现哪个适合你的最佳方法是尝试一下，或者至少访问他们的网站进行功能比较。我发现两个非常有用的工具是 `Usage` 和 `wwwstat`。`Usage` 是我最喜欢的商业日志分析应用程序。它是高度可配置的，并使用公司出名的 GD 库生成出色的图形化报告。我也喜欢用 Perl 编写的免费程序 `wwwstat`，因此你需要在运行它的系统上安装 Perl。

## 维护服务器日志文件

在访问率高或有很多虚拟域的 Apache站点上，日志文件会在极短时间内变得巨大，这很容易导致磁盘危机。当日志文件变得非常大时，你应该对其进行轮转。你有两种轮转日志的方法：你可以使用 Apache 自带的名为 `rotatelog` 的工具，也可以使用 `logrotate`。

### 使用 rotatelog

Apache 自带了一个名为 `rotatelog` 的支持工具。你可以如下方式使用该程序：

```
TransferLog "| /path/to/rotatlogs logfile rotation time in seconds"
```
