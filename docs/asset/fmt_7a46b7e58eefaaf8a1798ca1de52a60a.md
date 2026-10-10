
# 网络

## 错误日志配置

### `ErrorLog` 指令
- **功能**：指定错误日志文件的位置。
- **说明**：如果未在 `<VirtualHost>` 容器内指定 `ErrorLog` 指令，与该虚拟主机相关的错误消息将记录在此处。如果*确实*为 `<VirtualHost>` 容器定义了错误日志文件，该主机的错误将记录在那里，而不是这里。
- **默认值**：`logs/error_log`

### `LogLevel` 指令
- **功能**：控制记录到 `error_log` 的消息数量。
- **可能值**：`debug`, `info`, `notice`, `warn`, `error`, `crit`, `alert`, `emerg`。
- **默认值**：`warn`

## 日志格式定义

以下指令定义了用于配合 `CustomLog` 指令使用的格式别名（见下文）：

```
LogFormat "%h %l %u %t "%r" %>s %b" "%{Referer}i\"\"%{User-Agent}i\"\"" combined
LogFormat "%h %l %u %t "%r" %>s %b" common
LogFormat "%{Referer}i -> %I" referer
LogFormat "%{User-agent}i" agent.
```

### 访问日志配置
- **位置**：`logs/access_log`（默认格式为 `common`）。
- **说明**：如果你未在 `<VirtualHost>` 容器内定义任何访问日志文件，它们将记录在此处。相反，如果你*确实*定义了每个 `<VirtualHost>` 的访问日志文件，事务将记录在那里，而不是*不*在此文件中。

- **单独日志选项**：如果你希望拥有单独的 `agent` 和 `referer` 日志文件，请取消以下指令的注释：
```
#CustomLog logs/referer_log referer
#CustomLog logs/agent_log agent
```

- **组合日志选项**：对于包含访问、`agent` 和 `referrer` 信息的单个日志文件（组合日志文件格式），使用以下指令：
```
CustomLog logs/access_log combined
```

## 日志指令详解

### `ErrorLog` 与 `LogLevel` 说明
这些行处理服务器错误、客户端跟踪信息和传入请求是如何被记录的。
- `ErrorLog` 指令可以指定绝对路径名或相对于 `ServerRoot`（默认为 `/etc/httpd`）的路径名，它指示服务器应存储错误消息的位置。在这种情况下，指定的文件是 `logs/error_log`，它扩展为 `/etc/httpd/logs/error_log`（实际上，这是 `/var/log/httpd` 目录中 `error_log` 文件的符号链接）。
- `LogLevel` 指令控制错误日志中出现的消息严重性和数量。消息范围可以从特别冗长的 `debug` 日志级别到特别静默的 `emerg` 日志级别。
  - 对于 `debug`，每当配置文件被读取、使用访问控制机制或活动服务器数量发生变化时，都会记录一条消息。
  - 对于 `emerg`，只记录导致服务器恐慌状况的关键系统级故障。
- `LogLevel` 指令指定的级别表示将记录的最不严重的消息——该严重程度及以上的所有消息都会被记录。例如，如果 `LogLevel` 设置为 `warn`，错误日志将包含 `warn`、`error`、`crit`、`alert` 和 `emerg` 级别的消息。默认的 `warn` 值是正常使用的良好选择（它只记录最终可能需要操作员干预的重要事件），但 `info` 和 `debug` 非常适合测试服务器配置或追踪错误的准确位置。

### `LogFormat` 格式说明
四个 `LogFormat` 行定义了（供稍后使用）四种日志文件格式：`combined`, `common`, `referer` 和 `agent`。你还可以添加第五种格式，称为 `combined`。`LogFormat` 指令中可用的标记在表 20-5 中描述。`LogFormat` 定义可以根据你的个人偏好进行修改，并且可以根据需要创建其他自定义格式。

- **`common` 格式**：包括客户端的主机名或 IP 地址，由 ident 守护进程报告的用户名以及服务器的身份验证方法（如果适用），请求发生时的本地时间，实际的 HTTP 请求，服务器响应代码以及传输的字节数。此格式是 Web 服务器（最近甚至 FTP 服务器）的事实标准。
- **`referer` 格式**：为了连接跟踪目的，存储链接到刚刚提供的文档的 URL（来自同一站点或外部服务器）（相对于 `ServerRoot`）。例如，如果页面 `www.example.com/corp/about_us.html` 包含指向你位于 `www.mybox.com/linuxguy/bio.html` 的主页的链接，当客户端访问该链接时，`www.mybox.com` 上的 referer 日志将如下所示：
```
http://www.example.com/corp/about_us.html  -\> /linuxguy/bio.html
```
这些信息可用于确定每个客户端到达你网站的路径。

## 表 20-5：`LogFormat` 中可用的令牌

| 令牌 | 描述 |
| --- | --- |
| `%a` | 客户端机器的 IP 地址 |
| `%b` | 发送给客户端的字节数（不包括头部信息） |
| `%(VAR)e` | 环境变量 `VAR` 的内容 |
| `%f` | 请求的 URL 引用的文件名 |
| `%h` | 客户端机器的主机名 |
| `%(Header)i` | HTTP 请求中指定头行的内容 |
| `%l` | 由 `identd` 守护进程报告（如果可用），发起请求的客户端机器上的用户 |
| `%(Note)i` | 来自不同模块的消息 `Note` 的内容 |
| `%(Header)o` | HTTP 响应中指定头行的内容 |
| `%p` | 接收请求的端口号 |
| `%P` | 处理请求的服务器进程的 PID |
| `%r` | 客户端发出的实际 HTTP 请求 |
| `%s` | 请求生成的服务器响应代码 |
| `%t` | 当前的本地时间和日期。可以使用 `%(Format)t` 更改时间格式，其中 `Format` 在 `strftime(3)` 手册页中有所描述。 |
| `%T` | 满足客户端请求所需的秒数 |
| `%u` | 如果访问控制规则要求用户名和密码认证，这代表客户端提供的用户名。 |
| `%U` | 客户端请求的 URL |
| `%v` | 根据域名系统 (DNS) 确定的服务器主机名和域名 |
| `%V` | 根据 `ServerName` 指令确定的处理请求的服务器主机名和域名 |

**`Agent` 格式**存储每个传入连接的 `User-Agent` HTTP 头内容。此字段通常指示浏览器名称和版本、语言以及运行浏览器的操作系统或架构。在运行 CentOS 的 Pentium II 上，Mozilla 将生成以下条目：
```
Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.6)
```

## 日志记录策略

*`combined`* 格式将其他三种日志文件格式中的所有信息包含在一行中。这种格式适用于将所有连接相关的日志条目存储在一个集中文件中。默认被注释掉的 *`common`* 格式可以通过移除 `#` 字符来启用，以记录实际接收 (`%b`) 和发送 (`%o`) 的字节数，前提是已加载 `mod_logio` 模块。

`CustomLog` 指令将定义的某个 `LogFormat` 格式分配给一个文件名（同样，指定为绝对路径名或相对于 `ServerRoot` 的路径名）。唯一未注释的定义将 `combined` 格式分配给 `/etc/httpd/logs/access_log` 文件。若要单独保留 `agent` 或 `referer` 信息，请取消对定义的注释。此外，你还可以选择注释掉 `CustomLog logs/access_log combined` 行，并改用 `common` 格式的定义。

## 添加签名

Apache 服务器生成的任何页面都可以在页面底部添加一行签名。服务器生成页面的示例包括目录列表、错误页面、状态页面或信息页面。`ServerSignature` 指令可以设置为 `On`、`Off` 或 `Email`。以下是 `ServerSignature` 的默认外观：

```
###### Optionally add a line containing the server version and virtual
###### host name to server-generated pages (error documents, FTP directory
###### listings, mod_status and mod_info output etc., but not CGI generated
###### documents).
###### Set to "Email" to also include a mailto: link to the ServerAdmin.
# Set to one of:  On | Off | Email
#
ServerSignature On
```

- 当 `ServerSignature` 设为 `On` 时，类似于以下内容的一行将出现在服务器生成页面的底部：
*Apache/2.2.8 (CentOS) Server at zarkov.example.com Port 80*

- 当 `ServerSignature` 设为 `Email` 时，将在签名行中添加指向网页管理电子邮件账户的链接（服务器名称将变成链接）。如果指令设为 `Off`，则该行完全不会显示。启用 SSL 或 WebDAV 时，此信息也会出现在服务器签名中。通常，最好在面向互联网的服务器上尽可能少地透露信息（因此最好关闭这些指令）。

## 别名与重定位内容

有多种方式来定义别名内容。这些包括 `Alias` 和 `ScriptAlias` 指令。以下是 `httpd.conf` 中与别名相关的设置（已移除注释）：

```
#
###### Aliases: Add here as many aliases as you need (with no limit). The format is
###### Alias fakename realname
#
Alias /icons/ "/var/www/icons/"

<Directory "/var/www/icons/">
    Options Indexes MultiViews FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>

###### ScriptAlias: This controls which directories contain server scripts.
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

###### "/var/www/cgi-bin" should be changed to whatever your ScriptAlias
###### CGI directory exists, if you have that configured.
#
<Directory "/var/www/cgi-bin/">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

- `Alias` 指令指向文件系统位置（不一定在 `DocumentRoot` 内）。例如，如果存在以下一行，对 `/bigjob/www.mybox.com/bigjob/index.html` 中文档的请求将导致检索 `/home/newguy/proj/index.html`。
```
Alias /bigjob /home/newguy/proj
```

- `icons` 别名允许访问 Web 服务器为你的网站使用的 Apache 图标。`icons` 目录可以从 `/var/www` 目录访问。

- `ScriptAlias` 指令执行相关功能，但它所别名的目录包含可执行代码（很可能是 CGI 脚本）。其语法与 `Alias` 指令相同。使用 `ScriptAlias` 时要特别注意。因为 `ScriptAlias` 定义了服务器上可从 Web 内容运行的脚本所在位置，所以你应确保只分配那些包含安全且不会在你的系统中打开安全漏洞的脚本的目录。

## 重定向旧内容的请求

随着 Web 服务器上内容的变化，某些内容将变得过时，而其他内容可能会移动到文件系统中的其他位置或不同的服务器。使用 `Redirect` 指令，你可以将旧内容的请求重定向到新位置。

默认情况下，你的 Apache 服务器没有设置任何 `Redirect` 指令。但是，你可以取消注释以下示例并根据需要进行定制：

```
###### Redirect permanent /foo http://www.example.com/bar
```

`Redirect` 可以通过简单指示旧位置和新位置，用来指示客户端它们寻求的文档已移至其他地方（同一服务器或外部位置）。如果之前的 `Redirect` 选项处于活动状态，客户端尝试访问 `www.mybox.com/foo` 将被重定向到 `www.example.com/bar`。

除了使用 `permanent` 作为 `Redirect` 的服务（导致重定向状态 301）外，你还可以使用 `temp`（重定向状态 302）、`seeother`（替换状态 303）或 `gone`（永久移除状态 410，原文误写为 401）。你也可以提供 300 到 399 之间的任何状态代码作为服务，这代表不同的错误响应。（这些数字是 HTTP 状态代码。）

> HTTP 状态代码是 RFC 2616 中 HTTP 协议的一部分定义的。请参考 `www.w3.org/Protocols/rfc2616/rfc2616.txt` 上的该文档。

## 定义索引

你可以让 Apache 服务器为不同类型的文件显示不同的图标。要使用此功能，`IndexOptions` 应设置为 `FancyIndexing`；并且应使用 `AddIconByEncoding`、`AddIconByType` 和 `AddIcon` 指令：

```
###### Directives controlling display of server-generated directory listings.

###### FancyIndexing is if you want fancy directory indexing or standard.
###### VersionSort is whether files containing version numbers should be
###### compared in the natural way, so that 'apache-1.3.9.tar' is placed
###### before 'apache-1.3.12.tar'.
#
IndexOptions FancyIndexing VersionSort NameWidth=* HTMLTable

###### AddIcon* directives tell the server which icon to show for different
###### files or filename extensions. These are only displayed for
###### FancyIndexed directories.
#
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (IMG,/icons/image2.gif) image/*
AddIconByType (SND,/icons/sound2.gif) audio/*
AddIconByType (VID,/icons/movie.gif) video/*

AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/binhex.gif .hqx
AddIcon /icons/tar.gif .tar
AddIcon /icons/world2.gif .wrl .wr1 .gz .vrm .vrm .iv
AddIcon /icons/compressed.gif .Z .gz .tgz .gz .zip
AddIcon /icons/a.gif .ps .ai .eps
AddIcon /icons/layout.gif .html .shtml .htm .pdf
```
