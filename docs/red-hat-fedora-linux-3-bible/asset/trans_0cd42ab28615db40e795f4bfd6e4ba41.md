

changed。在使用 emerg 级别时，仅记录会导致服务器恐慌状态的关键系统级故障。

`LogLevel` 指令指定的级别表示将记录的最不严重的消息级别——该级别及以上严重程度的所有消息都会被记录。例如，如果将 `LogLevel` 设置为 warn，则错误日志将包含 warn、error、crit、alert 和 emerg 级别的消息。对于常规使用，warn 的默认值是一个不错的选择（它只会记录最终可能需要操作员干预的重大事件），但 info 和 debug 级别非常适合测试服务器配置或追踪错误的确切位置。

四个 `LogFormat` 行定义了（供稍后使用）四种日志文件格式：combined、common、referer 和 agent。`LogFormat` 指令中可用的令牌在表 21-5 中进行了描述。可以根据自己的个人偏好修改 `LogFormat` 定义，并可根据需要创建其他自定义格式。

### 表 21-5：`LogFormat` 中可用的令牌

| 令牌 | 描述 |
| :--- | :--- |
| $a | 客户端机器的 IP 地址。 |
| $b | 发送给客户端的字节数（不包括头部信息）。 |
| ${VAR}e | 环境变量 VAR 的内容。 |
| $f | 请求 URL 引用的文件名。 |
| $h | 客户端机器的主机名。 |
| ${Header}i | HTTP 请求中指定头部行的内容。 |
| $l | 由 ident 守护进程报告（如果可用），发起请求的客户端机器上的用户。 |
| ${Note}n | 来自不同模块的消息 Note 的内容。 |
| ${Header}o | HTTP 响应中指定头部行的内容。 |
| $p | 接收请求的端口号。 |
| $P | 处理请求的服务器进程的 PID。 |
| $r | 来自客户端的实际 HTTP 请求。 |
| $s | 由请求生成的服务器响应代码。 |
| $t | 当前本地日期和时间。时间格式可以使用 ${Format}t 进行更改，其中 Format 在 strftime(3) man 页面中有描述。 |
| $T | 满足客户端请求所需的秒数。 |
| $u | 如果访问控制规则要求用户名和密码身份验证，则代表客户端提供的用户名。 |
| $U | 客户端请求的 URL。 |
| %v | 根据域名系统 (DNS) 确定的服务器主机名和域名。 |
| %V | 根据 `ServerName` 指令确定的处理请求的服务器主机名和域名。 |

*common* 格式包括客户端主机名称或 IP 地址、由 ident 守护进程和服务器身份验证方法报告的用户名（如果适用）、发起请求的本地时间、实际 HTTP 请求、服务器响应代码以及传输的字节数。此格式是 Web 服务器（甚至后来 FTP 服务器）中事实上的标准。

为了进行连接跟踪，*referer* 格式存储了指向刚交付文档（相对于 *ServerRoot*）的 URL（来自同一站点或外部服务器）。例如，如果页面 *http://www.redhat.com/corp/about_us.html* 包含指向位于 *http://www.mybox.com/~linxguy/bio.html* 的您主页面的链接，当客户端访问该链接时，*www.mybox.com* 上的 referrer 日志看起来像这样：

```
http://www.redhat.com/corp/about_us.html -> /linxguy/bio.html
```

可以使用此信息来确定每个客户端到达您网站所采取的路径。

*agent* 格式存储每个传入连接的 User-agent: HTTP 头部内容。此字段通常指示浏览器名称和版本、语言以及运行浏览器的操作系统或架构。在运行 Fedora 的 Pentium II 上，Mozilla 将产生以下条目：

```
Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.6)
```

*combined* 格式将其他三种日志文件格式中的所有信息包含在一行中。此格式适用于将所有与连接相关的日志条目存储在一个集中文件中。

`CustomLog` 指令将已定义的 *LogFormat* 格式之一分配给一个文件名（同样，指定为绝对路径名称或相对于 *ServerRoot* 的路径名称）。唯一未注释的定义将 combined 格式分配给 */etc/httpd/logs/access_log* 文件。要单独保留 agent 或 referrer 信息，请取消相应定义的注释。此外，您也可以选择注释掉 *CustomLog logs/access_log* combined 行，改为使用 common 格式的定义。

## 添加签名

由 Apache 服务器生成的任何页面都可以在页面底部添加签名行。服务器生成的页面的示例包括目录列表、错误页面、状态页面或 info 页面。`ServerSignature` 指令可以设置为 `On`、`Off` 或 `EMail`。以下是 `ServerSignature` 的默认外观：

```
# Optionally add a line containing the server version and virtual
# host name to server-generated pages (error documents, FTP directory
# listings, mod_status and mod_info output etc., but not CGI generated
# documents)
# Set to "EMail" to also include a mailto: link to the ServerAdmin.
# Set to one of: On | Off | EMail
#
ServerSignature On
```

将 `ServerSignature` 设置为 `On` 时，此行将出现在服务器生成页面的底部：

```
Apache/2.0.48 (Fedora) Server at toys.linuxtoys.net Port 80
```

将 `ServerSignature` 设置为 `EMail` 时，签名行中将添加指向 Web 页面管理电子邮件帐户的链接（服务器名称变为链接）。如果指令设置为 `Off`，则此行根本不会出现。

## 别名重定位内容

定义别名内容有多种方式。这些包括 `Alias` 和 `ScriptAlias` 指令。以下是 `httpd.conf` 中的别名相关设置（已移除注释）：

```
# Aliases: Add here as many aliases as you need (with no limit). The
# format is
# Alias fakename realname
#
Alias /icons/ "/var/www/icons/"

<Directory "/var/www/icons">
    Options Indexes MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>

# ScriptAlias: This controls which directories contain server scripts.
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

# "/var/www/cgi-bin" should be changed to whatever your ScriptAliased
# CGI directory exists, if you have that configured.
#
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

Alias 指令指向一个文件系统位置（不一定在 DocumentRoot 内）。例如，如果存在以下行，对 /bigjob（http://www.mybox.com/bigjob/index.html）中文档的请求将导致获取 /home/newguy/proj/index.html。

```
Alias /bigjob /home/newguy/proj
```

icons 别名允许访问 Web 服务器网站使用的 Apache 图标。icons 目录可以从 /var/www 目录访问。

`ScriptAlias` 指令执行相关功能，但它所别名的目录包含可执行代码（很可能是 CGI 脚本）。语法与 `Alias` 指令相同。使用 `ScriptAlias` 时要特别注意。因为 `ScriptAlias` 定义了服务器 Web 内容中可运行脚本的位置，所以应确保仅分配包含受保护脚本且不会在系统中打开安全漏洞的目录。

## 重定向对旧内容的请求

随着 Web 服务器上的内容更改，一些内容将变得过时，而其他内容可能会移至文件系统中的其他位置或不同的服务器。使用 `Redirect` 指令，可以将对旧内容的请求重定向到新位置。

默认情况下，您的 Apache 服务器没有设置任何 `Redirect` 指令。但是，您可以取消以下示例的注释并根据需要定制：

```
# Redirect permanent /foo http://www.example.com/bar
```

Redirect 可用于指示客户端其寻找的文档已移至其他位置（同一服务器或外部位置），只需指示旧位置和新位置即可。如果前面的 Redirect 选项生效，客户端尝试访问 http://www.mybox.com/Foo 将被重定向到 http://www.example.com/bar。

除了使用 permanent 作为 Redirect 的服务（结果为 301 重定向状态）外，还可以使用 temp（302 重定向状态）、seeother（303 替换状态）或 gone（410 永久移除状态）。您还可以将 300 到 399 之间的任何状态代码作为服务，这些代码代表不同的错误响应。（这些数字是 HTTP 错误代码。）

