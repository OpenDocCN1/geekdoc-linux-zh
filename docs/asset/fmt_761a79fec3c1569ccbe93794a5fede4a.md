
| `ServerRoot` `/etc/httpd` | 定义 Apache 配置文件和日志文件的顶层目录 |

| `ServerTokens` `OS` | 定义服务器 HTTP 响应头的内容 |

| `StartServers` `8` | 定义 Apache 启动时创建的子服务器数量 |

| `Timeout` `120` | 定义 Apache 等待数据包发送和接收操作的最大秒数 |

表 23-1 中的某些项目需要额外的讨论。在指定日志文件或额外配置文件的名称时，除非它们以 `/` 开头，否则这些名称将附加到 `ServerRoot` 之后。例如，如果 `ServerRoot` `/etc/httpd` 且指定的日志文件为 `logs/mylog.log`，则完整名称为 `/etc/httpd/logs/mylog.log`，而 `/logs/mylog.log` 被解释为绝对路径。

对于大多数站点，表 23-1 中指令的默认值应显示 Fedora Core 和 RHEL 提供的默认 Apache 配置中的对应项，`LoadModule` 指令除外。为了节省空间和简化演示，注释已被移除。

```
ServerTokens OS
ServerRoot /etc/httpd
PidFile run/httpd.pid
Timeout 120
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
<IfModule prefork.c>
StartServers 8
MinSpareServers 5
MaxSpareServers 20
ServerLimit 256
MaxClients 256
MaxRequestsPerChild 4000
</IfModule>
```

**列表 23-1** Fedora Core 的全局配置指令。

```
<IfModule worker.c>
StartServers 2
MaxClients 150
MinSpareThreads 25
MaxSpareThreads 75
ThreadsPerChild 25
MaxRequestsPerChild 0
</IfModule>
Listen 80
Include conf.d/*.conf
```

**列表 23-1（续）**

23-1 中的内容不需要修改，但你可以考虑将 `MaxServers` 值设为 10，将 `StartServers` 值设为 5（这些指令的默认值）。然后，随着你开发服务器的使用模型，根据需要进行调整。同样，指定 `KeepAlive On` 会产生显著改进，消除了客户端与服务器之间建立新连接的开销。另一方面，如果开启了 KeepAlive 且在服务器上遇到性能问题，将 `KeepAliveTimeout` 减少到 5 通常比直接关闭 KeepAlive 更好。

`MinSpareServers` 和 `MaxServers` 指令使 Apache 能够自调节，根据 Web 服务器的使用情况增加或删除进程。当超过 `MaxClients` 尝试连接时，每个请求被放入队列（特别是 FIFO，先进先出队列），并在当前连接关闭时按接收顺序处理。然而，如果网站访问者等待太久，他们将发送另一个请求或完全断开。繁忙网站可能需要调整此值以适应大量流量。

`Listen 80` 指令表示服务器在 80 端口监听传入请求。因为 80 是默认端口，因此不需要指定，但这样显式设置端口会让配置更加透明。当使用 1024 以下的端口（特权端口）时，服务器必须由 root 启动。如果你愿意，可以配置 Apache 监听非特权端口（例如使用 `Listen 8080` 指令），在这种情况下服务器不需要由 root 用户和组运行。

子服务器如何创建以及何时创建取决于所使用的 MPM（多进程模块），这反过来影响 Apache 配置指令的行为。例如，`MaxClients` 只像无线程服务器描述的那样限制并发连接。在线程服务器中，MaxClients 限制数量

## 每个进程的并发连接线程数。大于此数的请求通常会被排队，而不是丢弃。同样，`ServerLimit` 指令指的是进程而非线程。在进程和线程之间共享限制将消除实现子服务器（subservers）的价值和意义。

服务器控制指令的影响取决于加载的是 prefork 还是 worker MPM。如果你将 prefork MPM 的设置与 Apache 1.x 的 worker 进程控制设置进行比较，你会发现其配置几乎是完全相同的。相比之下，worker MPM 需要完全不同的配置。例如，在 worker MPM 中，进程仅为两个服务器启动，但每个服务器可以拥有多达 25 个线程（`ThreadsPerChild`）。为了处理负载峰值，你可以增加子服务器的数量（`StartServers`）。对于 worker MPM，`MaxRequestsPerChild` 为 0，这意味着进程不会被杀死并重新创建。

## 配置默认服务器

Apache 有默认服务器或主服务器的概念，指的是响应任何由虚拟主机（也称为虚拟服务器）处理的 HTTP 请求的 `httpd` 服务器。目前暂不详述，虚拟服务器或虚拟主机是运行在与默认服务器同一台机器上的 `httpd` 进程，通过分配给虚拟主机的主机或 IP 地址与主服务器进行区分。尽管主服务器和虚拟服务器之间存在区别，但为主服务器定义的配置指令也适用于虚拟服务器，除非它们被覆盖。

> 交叉引用：下一节“配置虚拟服务器”将讨论针对虚拟服务器的配置指令，并对虚拟服务器进行通用讨论。

表 23-2 列出了用于配置默认服务器的指令以及每个指令的默认值（如适用）。

**表 23-2 默认服务器配置指令**

| 指令 | 描述 |

| :--- | :--- |

| `AccessFileName` `.htaccess` | 在请求文档的完整路径中列出一个或多个文件名，这些文件定义并控制对每个目录或子目录的访问，这些目录位于 `AccessFileName` 指定的文件（如果有）所在的顶级目录的同一级或更深层 |

| `AddCharset` `charset` | 将字符集 `charset` 添加到 Apache 支持的字符集列表中 |

| `AddDefaultCharset` `UTF-8` | 如果浏览器未请求或在 HTTP 请求头中未指定字符，则设置 Apache 的默认输出字符集 |

| `AddHandler` `handler` `mimetype` | 将处理器 `handler` 与 MIME 类型 `mimetype` 关联 |

| `AddIcon` `icon` `name` | 将图标映射为以 `name` 结尾的文件显示的图标；配合 `FancyIndexing` 指令使用 |

| `AddIconByEncoding` `icon` `mimeencoding` | 将图标与 MIME 编码 `mimeencoding` 的文件关联；配合 `FancyIndexing` 指令使用 |

| `AddIconByType` `icon` `mimetype` | 设置图标为显示 MIME 类型为 `mimetype` 的文件的图标；配合 `FancyIndexing` 指令 |

| `AddLanguage` `mimelang` `name` | 将 `name` 指定的文件扩展名映射到 MIME 语言 `mimelang`，覆盖之前对 `name` 的映射 |

| `AddOutputFilter` `output` `mimetype` | 将类型为 `output` 的服务器输出输出过滤器与 MIME 类型 `mimetype` 关联 |

| `AddType` `mimetype` `name` | 为以 `name` 结尾的文件添加指定的 `mimetype` 到从配置文件读取的 MIME 类型列表中 |

| `Alias` `urlpath` `dirpath` | 将相对于 `DocumentRoot` 指定的目录 `urlpath` 映射到文件系统 `dirpath`，允许 Apache 访问因所有内容必须在 `DocumentRoot` 下而原本无法访问的目录 |

| `CustomLog` `logs/access_log` `combined` | 定义 Apache 访问日志的名称以及记录到服务器请求时使用的格式 |

| `DefaultIcon` `/icons/unknown.gif` | 设置为无法确定 MIME 或内容类型的文件显示默认图标；配合 `FancyIndexing` 指令使用 |

| `DefaultType` `text/plain` | 当使用 `TypesConfig AddType` 指令无法确定请求文档的 MIME 类型时，定义默认 MIME 类型 |

| `<Directory dirname>` 指令 `</Directory>` | 界定一组适用于 `dirname` 及其子目录（如果有）的配置指令 |

| `DirectoryIndex` `filename` | 指定一个或多个文件名，当请求未指定特定文件或文档时，作为目录索引使用 |

| `DocumentRoot` `/var/www/html` | 设置提供所有请求文档的根目录；文档 URL（文件名）相对于 `DocumentRoot` 解释；另见 `UserDir` |

| `ErrorLog` `logs/error_log` | 定义 Apache 错误日志的名称，如果文件名不以 `/` 开头，则相对于 `ServerRoot` |

| `ForceLanguagePriority` | 使用在 `LanguagePriority` 中指定的值来返回一个有效结果。`Fallback` 从 `LanguagePriority` 中列出的选项中返回有效选择；`Prefer` 从客户端指定的接受语言中返回第一个匹配值 |

| `Group` `[#]apache` | 指定子服务器执行时使用的组名，或以 `#` 为前缀的 GID |

| `HeaderName` `HEADER.html` | 定义在目录列表顶部插入的内容 |

| `HostnameLookups` `Off` | 控制 Apache 是否对连接的主机执行 DNS 查询以便记录主机名 |

| `IndexIgnore` `filespec` | 定义目录索引器忽略的一个或多个文件模式 |

| `IndexOptions` `opts` | 设置控制 Apache 目录索引行为的选项 |

| `LanguagePriority` `spec` | 指定语言代码列表 `spec`，指示在内容协商期间应用语言代码的顺序 |

| `LogFormat` `str` `name` | 定义日志格式 `str name`，Apache 使用其记录消息 |

| `logLevel` `warn` | 控制 Apache 在错误日志中记录的信息量和详细程度 |

| `ReadmeName` `README.html` | 定义 `README.html` 为追加的文件内容 |

| `ScriptAlias` `urlpath` | 功能与 `Alias` 指令完全相同，指示 cgi 脚本 |

| `ServerAdmin` `root@localhost` | 定义显示给客户端的错误信息中的电子邮件地址

| `ServerName` | 指定服务器的替代名称（例如 `www.mydomain.com`），与实际的主机名不同 |

| `ServerSignature` `On` | 在生成的文档末尾附加 `ServerName` 和版本号 |

| `TypesConfig` `/etc/mime.types` | 设置 MIME 类型配置文件名（如果文件名不以 `/` 开头则相对于 `ServerRoot`），将文件扩展名映射到内容类型（另见 `AddType`） |

| `User` `[#apache` | 指定子服务时使用的用户名，或以 `#` 为前缀的 UID |

| `UserDir` `public_html` | 定义当客户端请求属于特定用户的文档时，使用的用户目录下的子目录 |

为了方便对表 23-2 中的指令进行进一步讨论，列表 23-2 显示了 Red Hat 默认 Apache 配置中的相应项目。该列表排除了注释以节省空间并简化讨论（省略号表示已删除的指令）。

# 配置 Web 服务器 529

```
DAVLockDB /var/lib/dav/lockdb

<IfModule>
ScriptAlias /cgi-bin/* /var/www/cgi-bin/*
<Directory /var/www/cgi-bin>
  AllowOverride None
  Options None
  Order allow, deny
  Allow from all
</Directory>
AddByEncoding(COMP, /icons/compressed.gif) x-compress x-gzip
AddIconByType (TXT, /icons/text.gif) text/*
AddIconByType (IMG, /icons/image2.gif) image/*
AddIconByType (SND, /icons/sound2.gif) audio/*
AddIconByType (VID, /icons/movie.gif) video/*
AddIcon /icons/binary.gif .bin .exe
..
AddIcon /icons/back.gif
AddIcon /icons/hand.right.gif README
AddIcon /icons/folder.gif ^DIRECTORY^
AddIcon /icons/blank.gif ^BLANKIKON^
DefaultIcon /icons/unknown.gif
ReadmeName README.html
HeaderName HEADER.txt
IndexOptions ?* ~ * HEADER RCS CVS *v ,t
AddLanguage ca .ca

AddLanguage zh-TW .zh-tw
LanguagePriority en cs ca da de lo eo es et fr he hr it ja ko lz nl nn
  no pl pt-BR ru sv zh-CN zh-TW
ForceLanguagePriority Fallback
AddDefaultCharset UTF-8
AddCharset ISO-8859-1 .iso8859-1 .latin
..
AddCharset shift_jis . .sjis
AddType application/x-compress .Z
AddType application/x-gzip .gz .tgz
AddHandler image-file map var
AddHandler type-map map var
AddType text/html .shtml
AddOutputFilter INCLUDES .shtml
Alias /error/* /var/www/error/*
<IfModule mod_negotiation.c>
<IfModule mod_include.c>
  <Directory */var/www/error*>
    AllowOverride None
    Options IncludeNoExec
    AddOutputFilter html
    AddHandler type-map var
    Order allow, deny
```

列表 23-2（续）

# 530 第23 章

Allow from all

LanguagePriority en de fr

ForceLanguagePriority Fallback

</Directory>

<IfModule>

</IfModule>

BrowserMatch "Mozilla/2" nokepalive downgrade-1.0 force-response-1.0

BrowserMatch "RealPlayer 4.0" force-response-1.0

BrowserMatch "Java/1.0" force-response-1.0

BrowserMatch "JDK/1.0" redirect-carefully

BrowserMatch "Microsoft Data Access Internet Publishing Provider redirect-carefully

BrowserMatch "*WebDrive" redirect-carefully

BrowserMatch "*WebDAVFS/1.[01]" redirect-carefully

BrowserMatch "*gnome-vfs" redirect-carefully

# 列表 23-2（续）

`User` 和 `Group` 指令表示子服务器由用户 `apache` 组所有，由于它们没有与 root 用户相同的权限，因此更安全。要在特权用户下运行子服务器，主服务器必须由 root 用户启动。为什么？只有具有 root 权限的进程才能更改 UID 和 GID 以维护 Linux 安全模型。

`ServerName` 指令定义了返回给客户端的名称，如果它与主机实际名称不同。例如，如果服务器的 DNS 名称是 `webbe.mydomain.com`，你可以指定 `ServerName` `www.mydomain.com`，以便服务器响应发送到 `http://www.mydomain.com/` 的请求。

`DocumentRoot` `/var/www/html` 将服务器目录设置为 `/var/www/html`，这意味着所有 URL 都在此目录下。例如，如果服务器名为 `www.example.com`，当客户端请求 `http://www.example.com/index.html` 时，服务器将返回文件 `/var/www/html/index.html`。

每个 `<Directory>` 块配置命名目录（或目录）及其子目录的访问信息。第一个块设置了所有目录的默认权限：

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

# 配置 Web 服务器 531
