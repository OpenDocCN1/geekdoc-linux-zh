
首先，`OpenLinux` 使用 Web 服务器处理所有文档，因此即使你不打算提供公共 Web 页面也会使用 Web 服务器。其次，`OpenLinux` 遵循了前述的使用 `Apache` 的最新趋势。也就是说，有一个程序始终运行并管理 Web 服务器的整体负载，根据流量负载以及你在 `httpd.conf` 中设置的其他参数，启动和停止 Web 服务器的其他副本来处理请求。

## `PORT` 80

网络端口是 Web 服务器期望请求到达的端口。80 端口是 Web 服务器的标准。

## 第 11 章：配置 `Apache` Web 服务器

如果你不使用 80 端口，则必须确保所有引用你网站的 URL 都包含正确的端口号。例如，如果你的端口是 8080，那么你的主页 URL 将如下：

```
http://www.myplace.org:8080/
```

如果你不是系统的 `root` 用户，或者想要一个公开性较低的 Web 服务器，通常会使用非标准端口。
此外，如果你使用编号小于 1023 的非标准端口（你可以一直到约 65,000），那么在启动 `httpd` 守护进程时必须以 `root` 用户身份登录。每个生成的副本都将使用 `httpd.conf` 中定义的用户 ID。

### `HostnameLookups`

`HostnameLookups` 指令（此处所示）决定了标准日志文件中存储什么类型的信息：

```
HostnameLookups on
```

你的 `Apache` Web 服务器处理的每个请求都记录在 `/etc/httpd/apache/logs/access.log` 中。在该文件中可以指定几种类型的信息。日志请求的一个标准部分是请求 Web 页面的人的地址。如果此指令关闭（`off`），则域名（`mydesk.bigorg.com`）被存储在日志文件中；如果开启，则存储 IP 地址。

使用域名（`OpenLinux` 的默认设置）会增加 Web 服务器的负载，但会让日志变得有用得多。（请查看第 13 章有关如何使用日志文件查看服务器统计数据的详情。）关闭此指令可以跳过为每个入站请求查找 IP 地址的步骤。

### 用户和组指令（`User` 和 `Group` 指令）

`User` 和 `Group` 指令定义了服务器以哪个用户和组运行，如下例：

```
User nobody
Group #-1
```

如果 `User` 后面列出的用户不是你登录的用户，那么在启动 Web 服务器时必须以 `root` 用户身份登录（`OpenLinux` 的自动启动会处理这一点）。Web 服务器启动后，它会自动切换到使用 `User` 和 `Group` 指令后列出的用户和组的安全访问权限。

`User` 和 `Group` 指令维护了你的 Web 服务器的安全。例如，假设一个用户发现了一个安全漏洞，允许该用户让 Web 服务器在你的系统上执行命令。如果 Web 服务器以 `nobody` 用户运行，那么运行的脚本将无法访问系统上的任何资源，因为 `nobody` 用户没有访问权限，因此恶意用户对安全漏洞造成的破坏很小。

出于安全原因，默认设置是 `nobody` —— 一个在安装期间专门为了此类目的创建的用户。`nobody` 用户没有主目录，且访问权限极少。这有助于保持你的 Web 服务器安全。但你必须确保你希望 Web 服务器发送给客户端的所有文档对所有人都是可读的，否则 `nobody` 以及随后的 Web 服务器将无法访问它们。

`OpenLinux` 遗留了未定义的组，以进一步增加安全性。`User` 指令和 `Group` 指令的值都可以在 `httpd.conf` 文件中以名称或用户/组 ID 数字的形式输入。取决于对你来说最方便。

![](img/e01f1106dd2902613fa0789c8baa7e6_311)

要设置任何文件的权限以便所有人读取，请使用 `chmod` 命令。

```
chmod +r
```

### `ServerAdmin`

`ServerAdmin` 指令提供接收任何问题的管理员的电子邮件地址。`OpenLinux` 的默认值是 `root`，但你应该将此值改为 `Webmaster`。

### `ServerRoot`

`ServerRoot` 指令指定存储服务器配置文件、错误日志和日志文件的目录，如下：

```
ServerRoot /etc/apache
```

### `BindAddress`

`BindAddress` 指令告诉 Web 服务器监听哪个 IP 地址或域名，用法如下：

```
#BindAddress *
```

`BindAddress` 指令在默认配置中被注释掉了，因为假设你提供一个 IP 地址和一个域名。

![](img/e01f1106dd2902613fa0789c8baa7e6_312_0)

`BindAddress` 指令允许你让一台物理计算机作为多个域名的 Web 服务器，例如 `abc.com`、`nbc.com` 和 `cbs.com`，都在同一台计算机上。

如果你在系统上使用多个域名，`ServerRoot` 和 `DocumentRoot` 定义了每个域名的存储位置。`BindAddress` 指令的值决定了 Web 服务器请求哪个域名或 IP 地址。

![](img/e01f1106dd2902613fa0789c8baa7e6_312_1)

### `ErrorLog`

`ErrorLog` 指令定义了错误日志文件的存储位置，如下：

```
ErrorLog /var/log/httpd/apache/error.log
```

假设错误日志存储在作为 `ServerRoot` 目录的子目录下。要更改这一点，请在此指令的值以斜杠（`/`）开头。如果你检查 `/etc/httpd/apache/logs` 和 `/var/log/httpd/apache/` 中的 inode（使用 `ls -li`），你会发现这些文件链接到同一个 inode ——它们是同一个文件的别名。这保持了兼容性。

![](img/e01f1106dd2902613fa0789c8baa7e6_312_2)

## `Linux` Web 服务器工具包

结合了 Web 服务器的组织方式和 `Linux` 错误日志位置的标准。错误日志文件，为 Web 服务器在尝试响应浏览器请求时遇到的每一个错误都记录了一行。例如，如果用户请求一个不存在的文件，系统将向请求文档的用户返回一个错误，并将该错误记录在错误日志文件中。错误日志文件记录了被请求的文件和生成的错误响应。

# 传输日志（`TransferLog`）

`TransferLog` 指令定义了传输日志文件的存储位置。与错误日志一样，除非此指令的值以正斜杠开头，否则传输日志被认为位于 `ServerRoot` 区域内。同样，这里的默认值以及 `/etc/httpd/apache/logs` 中的别名链接同时符合 `Apache` 的组织方式和 `Linux` 标准，如下：

```
TransferLog /var/log/httpd/apache/access_log
```

传输日志是一个文件，其中通过你的 Web 服务器响应浏览器请求发送的每个文件都占有一行。在繁忙的网站上，这个文件会迅速变得巨大。该文件也是统计访问量、检查谁访问了网站以及跟踪其他信息的统计程序的严格审查对象。在某种程度上，你可以确定此文件中存储了哪些信息。细节将在本章稍后提供。

以下是标准日志条目的示例：

```
trumpet.infision.com - [05/May/1997:06:13:03 -0600] GET /doc/prodlist.html HTTP/1.0 200 77
```

### 日志文件轮转（`Rotating Log Files`）

繁忙网站上的日志文件变得巨大并不需要长时间。但它们太重要了，不能直接丢弃。如果出现安全问题，你需要保存它们以便统计审查和研究。

编写一个脚本或命令每晚或每个周末运行，将现有日志文件移动到保存位置并启动新文件是非常简单的事。你可以将该脚本或命令名称放在 `at` 命令或 `/etc/crontab` 文件的“cron 任务”中，以便脚本每天或每周自动执行。

更多信息请参阅 `logrotate` 命令的手动页（从任何命令行提示符尝试 `man logrotate`）。

# 第 11 章：配置 `Apache` Web 服务器

# `PidFile`

`PidFile` 指令定义了 PID 文件的存储位置。程序的 PID 是进程 ID，是操作系统为系统上运行的每个程序生成的唯一数字。该指令用法如下：

```
PidFile /var/run/httpd.pid
```
