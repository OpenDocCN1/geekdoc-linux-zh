
```
Server version: Apache/1.3.4 (Unix)
Server built: Aug 10 1999 19:17:10
Server's Module Magic Number: 19990108:0
Server compiled with....
-D HAVE_MMAP
-D HAVE_SHMGET
-D USE_SHMGET_SCOREBOARD
-D USE_MMAP_FILES
-D USE_FLOCK_SERIALIZED_ACCEPT
-D HTTP_ROOT="/usr/local/apache"
-D SUXEC_BIN="/usr/local/apache/sbin/suexec"
-D DEFAULT_PIDLOG="logs/httpd.pid"
-D DEFAULT_SCOREBOARD="logs/apache/runtime_status"
-D DEFAULT_LOCKFILE="logs/accept.lock"
-D DEFAULT_XFERLOG="logs/access_log"
-D DEFAULT_ERRORLOG="logs/error_log"
-D TYPES_CONFIG_FILE="conf/types"
-D SERVER_CONFIG_FILE="conf/httpd.conf"
-D ACCESS_CONFIG_FILE="conf/access.conf"
-D RESOURCE_CONFIG_FILE="conf/misc.conf"
```

## 检查 Apache 是否启动

因为 Apache 将其进程 ID 写入 `/var/run/httpd.pid`，检查 Apache 是否正在运行的一种简单方法是查看该文件是否存在。使用 `cat` 命令查看文件。这里是一个显示 Apache 在进程 ID 7078 下运行的示例。

```
cat /var/run/httpd.pid
```

如果它没有运行，你的输出将是这样：

```
cat /var/run/httpd.pid: No such file or directory
```

这种方法并非万无一失；在系统崩溃后，Apache 退出但不删除其 `httpd.pid`。为了获得更准确的结果，请使用 `ps ax` 命令：

```
ps ax | grep [httpd]
```

内核版本为 2.2.9 的机器，使用 X11。这是我的机器，正在从我的 Web 服务器请求文件。如果我请求了一个不存在的文件，我会在访问日志中看到这些内容：

```
208.12.12.130 - [02/Aug/1999:12:06:39 -0700] "GET /badfile.html HTTP/1.0" 404 206
-" "Mozilla/4.61 Caldera fen (X11; Linux 2.2.9; i686)"
```

由于 `badfile.html` 不存在，Apache 返回了 404 错误，在当前上下文中这意味着该文件不存在（尽管通常该代码表示未找到）。它花费 206 字节来告诉我文件不存在。这些 `-` 表示没有引用的网页；我是手动输入 URL 的。这些内容也会记录在错误日志中：

```
http: [Mon Aug 2 12:06:39 1999] [error] [client 208.12.12.130] File does not
exist: /usr/lib-install/html/badfile.html
```

这一行没有给我太多细节，但它很好地提供了 Apache 尝试检索的文件在文件系统上的完整路径。由于这个原因，检查这个文件要容易得多。Apache 记录了两次失败的文件请求，因为大多数日志分析器不检查错误日志，只检查访问日志。

在寻找特定内容时，遍历整个日志文件可能是困难的。`grep` 命令将返回包含指定关键字的行。要查看来自 aol.com 的访问日志行，请尝试：

```
grep aol.com /var/log/http/apache/access_log
```

只显示包含 "aol.com" 文本的行。由于 America Online 是一个拨号服务，你可能仍然会有几百或上千行输出。要只显示输出的最后 10 行，可以将 `grep` 命令与管道符 (|) 以及 `tail` 命令结合：

```
grep aol.com /var/log/http/apache/access_log | tail
```

现在只显示最后 10 次 aol.com 的访问。如果你想搜索 aol 地址的最后一次访问，可以反序组合这些命令：

```
tail /var/log/http/apache/access_log | grep aol.com
```

`grep` 对这类 Apache 日志等文本文件有更多搜索功能。你可以通过输入 `man grep` 查看其帮助页，学习该命令的高级搜索功能。

![](img/9102b40bb114da6b158a518630807d57_134_0.png)

## 使用 lynx 进行故障排除

`lynx` Web 浏览器是一个快速且方便的浏览器，非常适合简单的网站故障排除。因为它是基于文本的，它不需要 X11 的开销。可以使用 `lynx` 强制对特定网站进行查询，然后你就可以检查 Apache 对该查询响应的访问和错误日志。可以在命令行中给 `lynx` 提供 URL，例如：

```
lynx http://localhost/
```

这会在文本屏幕上渲染 localhost Web 页面。如果你更想看源码，可以使用 `-source` 选项：

```
lynx -source http://localhost/
```

如果你不在乎查看 Web 页面而只想强制发送请求，请将输出重定向到 `/dev/null`：

```
lynx -source http://localhost/ > /dev/null
```

这会强制发送请求并丢弃输出。重定向输出时别忘记使用 `-source`，这样 `lynx` 在完成后就会退出。

# 适用于 Apache 的 Web 统计分析器

维护网站的一个重要部分是获取关于网站产生了多少流量、流量来自何处、接收到了哪些错误等的统计报告。Apache 没有附带任何统计程序，但我为此目的推荐了两个程序。第一个是 Analog，一个免费软件程序，它读取 Apache 日志文件并根据日志中的信息生成报告。另一个用于生成 Web 使用统计的更高级程序是 WebTrends，它是一个商业软件。（遗憾的是，他们没有为 Linux 日志文件分析器；他们只提供更贵的 Enterprise Reporting Server，它可以生成深度和细节详尽的实时报告。）

## 更多信息

关于 Apache Web 服务器的更多信息可以在互联网的多个地方找到。以下是我最喜欢的几个 URL：

| URL | 资源名称 |
| --- | --- |
| http://www.apache.org | Apache 软件基金会网站 |
| http://linuxkb.cheek.com/page.php?apache | Linux 知识库 |
| http://www.apache-ssl.com | Apache SSL 网站 |
| http://hohoo.ncsa.uiuc.edu/docs/tutorials/includes.html | 服务器端包含 |
| http://hohoo.ncsa.uiuc.edu/cgi/ | 通用网关接口 |

## 一个 MDA，一个 MTA

Caldera 已将 `procmail` 集成到向用户交付入站邮件的过程中。`procmail` 充入站邮件的过滤器。它可以执行许多整洁的操作，例如将邮件路由到不同的文件夹、向电子邮件发送自动回复、根据内容进行过滤，以及在邮件到达收件箱时执行程序。与 `procmail`（一种 MDA，即邮件投递代理）不同，`sendmail` 是 MTA（邮件传输代理）。因此，`sendmail` 将收到的入站邮件交给 `procmail` 进行投递。

## 其他 MTA 与 sendmail

Linux 常用使用 `sendmail` 以外的邮件传输代理。其他程序如 `smallmail` 和 `qmail` 是 `sendmail` 的直接替换方案。这些程序体积更小，更容易操作，尽管没有那么稳健或可配置性强。由于体积较小，支持者认为它们不容易受到安全漏洞的影响，而且邮件投递速度更快。

另一个 MTA `fetchmail` 并不是 `sendmail` 的替代品。`fetchmail` 用于通过 POP3 将邮件从一个服务器传输到另一个服务器，而不是通过 SMTP。当邮件服务器无法通过 SMTP 存储和转发技术访问时（即拥有邮件的服务器发起传输），这种方法非常有用。例如，许多小型工作组通过网络地址地址转换（Linux 术语称为 IP Masquerading）过程共享单个 IP 地址。位于此配置私有侧的邮件服务器将无法从公共互联网访问，也无法接收 SMTP 邮件连接。然而，该服务器可以发起 POP3 连接到拥有邮件的服务器，并在本地检索每条消息。
