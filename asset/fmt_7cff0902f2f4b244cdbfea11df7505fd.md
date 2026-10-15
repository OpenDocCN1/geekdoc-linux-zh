
# 或图像，你可能想改用 `"application/octet-stream"` 以替，

# 以防止浏览器尝试将二进制文件显示为文本。

```
```

`DefaultType` `text/plain`

```
```

通过使用 `mod_mime_magic` 模块，服务器可以查找提示信息来帮助确定文件类型。你必须确保将该模块添加到你的系统中才能使用它。以下是当模块可用时导致使用该模块的指令：

```
<IfModule mod_mime_magic.c>

  MIMEConfigFile share/magic

</IfModule>
```

## 设置主机名查找

在 Apache Web 服务器中，你可以让服务器为传入的客户端请求查找地址。开启 `HostnameLookups` 条目可以实现此功能：

```
# HostNameLookups: 记录客户端名称或仅记录其 IP 地址
# 例如   www.apache.org (on) 或 204.62.129.132 (off)。
# 默认关闭的，因为对于网络来说，如果人们必须
# 有意识地开启此功能会更好。
HostnameLookups Off
```

如果开启了 `HostnameLookups` 指令，每个传入的连接都会生成一个 DNS 查询，将客户端的 IP 地址转换为主机名。如果你的网站访问量很大，服务器的响应时间可能会受到不利影响。除非你使用需要完全限定域名且无法自行查找的日志分析程序或统计包，否则应关闭 `HostnameLookups`。随 Apache 分发版安装的 `resolve` 程序可以调度在非高峰时段执行查找并编辑日志文件。

## 配置 HTTP 日志

你可以设置多个与 Apache 信息日志相关的值。如下例所示，你可以设置错误日志的位置、日志警告级别以及一些日志别名：

```
# HostNameLookups: 记录客户端名称或仅记录其 IP 地址
# 例如  www.apache.org (on) 或 204.62.129.132 (off)。
# 默认关闭的，因为对于网络来说，如果人们必须
# 有意识地开启此功能会更好，因为启用它意味着
# 每个客户端请求将导致至少向名称服务器
# 发送一次查询请求。
HostnameLookups Off
```

```
# ErrorLog: 错误日志文件的位置。
# 如果你没有 <VirtualHost> 容器内指定 ErrorLog 指令，
# 与该虚拟主机相关的错误消息将记录
# 在处。如果你确实为 <VirtualHost> 容器定义了
# 错误日志文件，该主机的错误将记录在在那里，而不是在这里。
ErrorLog /var/log/httpd/error_log
```

```
# LogLevel: 控制记录到 error_log 中的消息数量。
# 可能的值包括：debug, info, notice, warn, error, crit,
# alert, emerg。
LogLevel warn
```

# 以下指令定义了一些用于 CustomLog 指令的
# 别名（见下文）。

```
LogFormat "%h %l %u %t \"%r %s \"%Referer\" \"%User-Agent\"" combined
LogFormat "%h %l %u %r" %s %b" common
LogFormat "%Referer -> %U" referer
LogFormat "%User-Agent>" agent
```

# 访问日志文件的位置和格式（通用日志文件格式）。
# 如果你没有在 <VirtualHost> 容器内定义任何
# 访问日志文件，与该虚拟主机相关的错误消息将
# 记录在这里。

```
CustomLog /var/log/httpd/access_log combined
```

# 访问日志文件的位置和格式（通用日志文件格式）。
# 如果你没有在 <VirtualHost> 容器内定义任何
# 访问日志文件，与该虚拟主机相关的错误消息将
# 记录在这里。

```
CustomLog /var/log/httpd/access_log common
```

# 访问日志文件的位置和格式（通用日志文件格式）。
# 如果你没有在 <VirtualHost> 容器内定义任何
# 访问日志文件，与该虚拟主机相关的错误消息将
# 记录在这里。

```
CustomLog /var/log/httpd/access_log referer
```

# 访问日志文件的位置和格式（通用日志文件格式）。
# 如果你没有在 <VirtualHost> 容器内定义任何
# 访问日志文件，与该虚拟主机相关的错误消息将
# 记录在这里。

```
CustomLog /var/log/httpd/access_log agent
```

等等，再次查看文本：
"以下指令定义了一些用于 `CustomLog` 指令的别名（见下文）。"
"四个 `LogFormat` 行定义了（供以后使用）四种日志文件类型：`combined`, `common`, `referer` 和 `agent`。`LogFormat` 中的可用令牌见表 21-5。`LogFormat` 可以根据你的喜好进行修改，并根据需要创建自定义格式。”

## 表 21-5 LogFormat 中的可用令牌

| 令牌 | 描述 |
| :--- | :--- |
| `%a` | 客户端的 IP 地址。 |
| `%b` | 发送到客户端的字节数（排除头部信息）。 |
| `%(VAR)e` | 环境变量 VAR 的内容。 |
| `%f` | 请求 URL 引用的文件名。 |
| `%h` | 客户端的主机名。 |
| `%(Header)i` | HTTP 请求中指定头部行的内容。 |
| `%l` | 由标识守护进程（如果可用），发起请求的客户端机器的用户。 |
| `%(Note)n` | 来自不同模块的消息内容。 |
| `%(Header)o` | HTTP 响应中指定头部行的内容。 |
| `%p` | 接收请求的端口号。 |
| `%P` | 处理请求的服务器进程 PID。 |
| `%r` | 来自客户端的实际 HTTP 请求。 |
| `%s` | 请求生成的服务器响应码。 |
| `%t` | 当前的本地时间和日期。时间格式可以使用 `%Format` 更改，Format 见 `strftime(3)` 手页。 |
| `%T` | 满足客户端请求所需的秒数。 |
| `%u` | 如果访问控制规则使用用户名/密码认证，这代表客户端提供的用户名。 |
| `%U` | 客户端请求的 URL。 |
| `%v` | 根据域名系统 (DNS) 的服务器的主机名和域名。 |
| `%V` | 根据 `ServerName` 指令处理请求的服务器的主机名和域名。 |

# 第 21 章 + 设置 Web 服务器 743

通用格式包括客户端主机名或 IP 地址、由 ident 守护进程报告的用户名以及服务器的身份验证方法（如果适用）、请求时的本地时间、实际的 HTTP 请求、服务器响应代码以及传输的字节数。这种格式是 Web 服务器（最近甚至包括 FTP 服务器）之间事实上的标准。

为了便于连接跟踪，引发生用格式（refer 格式）将存储链接到刚刚交付文档的 referer URL（来自同一站点或外部服务器）（相对于 `ServerRoot`）。例如，如果页面 `http://www.redhat.com/about_us.html` 包含一个指向您的小主页 `http://www.mybox.com/linuxguy/bio.html` 的链接，当客户端访问该链接时，`www.mybox.com` 上的 referer 日志将显示为：

```
http://www.redhat.com/about_us.html -> /linuxguy/bio.html
```

此信息可用于确定每个客户端通过何种路径到达您的站点。

代理 格式（agent 格式）将存储传入连接的 `User-agent:` HTTP 头部内容。该字段通常指示浏览器版本和名称、语言以及运行浏览器的操作系统或架构。在 Pentium II 的 Red Hat 7 上，Netscape 将产生以下条目：

```
Mozilla 4.51 [en] (X11; I; Linux 2.2.16-17 i686)
```

合并格式（combined format）将其他三种日志文件格式中的所有信息整合到一行中。这种格式适用于在一个集中文件中存储所有与连接相关的日志条目。

`CustomLog` 指令将定义的 `LogFormat` 格式之一分配给文件名（同样指定为绝对路径或相对于 `ServerRoot` 的路径）。上述未注释的定义将通用格式分配给文件 `/var/log/http/access_log`。如果您需要保留别名（alias）或 referer 信息，只需取消这些定义的注释。您也可以选择注释掉 `CustomLog /var/log/httpd/access_log` 这一行，并改用合并格式的定义。

## 为重定位内容别名

有多种方法定义别名内容，包括 `Alias` 指令和 `ScriptAlias` 指令：

```
