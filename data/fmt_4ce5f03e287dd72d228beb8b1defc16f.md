
## 需要构造自引用 URL 时

需要构造自引用 URL（指向响应服务器的 URL）时，它将使用 `ServerName` 和 `Port` 生成“规范”名称。如果此设置关闭，它将尽可能使用客户端提供的主机名。这也影响 CGI 脚本中的 `SERVER_NAME` 和 `SERVER_PORT`。

`UseCanonicalName On`

## TypesConfig

描述 `mime.types` 文件（或等效文件）位置。

`TypesConfig /etc/mime.types`

## DefaultType

当无法从文件名确定类型时，服务器将使用的默认 MIME 类型。如果你的服务器主要是文本或 HTML 文档，`text/plain` 是一个很好的值。如果大部分内容是二进制（如或图像），你可能希望使用 `application/octet-stream` 以防止浏览器将二进制文件显示为文本。

`DefaultType text/plain`

## mod_mime_magic

`mod_mime_magic` 模块允许服务器使用文件内容的提示来确定其类型。`MagicFile` 指令告诉模块定义所在的位置。

`mod_mime_magic` 不是默认服务器的一部分（你必须通过 `LoadModule` 自己添加它[参见“全局环境”部分的 DSO 段]，或者重新编译服务器并将 `mod_mime_magic` 包含在配置中），因此它被封装在 `<IfModule>` 容器中。这意味着只有当模块是服务器的一部分时，`MagicFile` 指令才会被处理。

```
<IfModule mod_mime_magic.c>
MIMagicFile /usr/share/magic
</IfModule>
```

## HostnameLookups

记录客户端的名称或仅其 IP 地址。例如 `www.apache.com` (开启) 或 `204.62.129.132` (关闭)。默认值为关闭，因为如果人们有意开启此功能，对网络更好，因为启用它意味着每个客户端请求都会导致至少一次查询请求到 `nameserver`。

关闭主机名查找：
`HostnameLookups Off`

## ErrorLog

错误日志文件的位置。如果你没有在 `<VirtualHost>` 容器内指定 `ErrorLog` 指令，则与该虚拟主机相关的错误信息将记录在此处。如果你“确实”为 `<VirtualHost>` 容器定义了错误日志文件，则该主机的错误将记录在其中而不是在此处。

`ErrorLog /var/log/httpd/error_log`

## LogLevel

控制记录在 `error_log` 中的消息数量。可选值包括：`debug`, `info`, `notice`, `warn`, `error`, `crit`, `alert`, `emerg`。

日志级别警告：
`LogLevel warn`

以下指令定义了一些格式别名，用于 `CustomLog` 指令（见下文）。

```
LogFormat "%h %l %u \%r\" %>s b \%{Referer}i\"%{User-Agent}i\" combined
LogFormat "%h %l %u \%r\" %>s b" common
LogFormat "%(Referer)i -> %U" referer
LogFormat "%(User-Agent)i" agent
```

## 访问日志

访问日志文件的位置和格式（通用日志格式）。如果你没有在一个 `<VirtualHost>` 容器内定义任何访问日志文件，它们将记录在此处。相反，如果你“确实”定义了 `<VirtualHost>` 访问日志，则事务将记录在其中而不在在此文件中。

`CustomLog /var/log/httpd/access_log common`

如果你想拥有 `agent`（代理者）和 `referer`（引用页）日志文件，请取消以下指令。

```
# #CustomLog /var/log/httpd/referer_log referer
#CustomLog /var/log/httpd/agent_log agent
```

如果你希望为访问、`agent` 和 `referer` 信息使用单一日志文件（组合日志格式），可以使用以下指令。

`# #CustomLog /var/log/httpd/access_log combined`

此外，在服务器生成的页面中（错误文档、FTP 目录列表、`mod_status` 和 `mod_info` 输出等，但不包括 CGI 生成的文档）添加包含包含服务器版本和虚拟主机名称的行。设置为 `Email` 也包含指向 `ServerAdmin` 的 `mailto:` 链接。设置为之一：`On` | `Off` | `EMail`

`ServerSignature On`

## Aliases

根据需要添加尽可能多的别名（无限制）。格式为 `Alias filename realise`。注意你在 ` ` 后面包含一个末尾斜杠 `/`，那么服务器将要求在 URL 中存在该路径。因此在示例中 `icons/` 没有设置别名，只有 `icons/`。

`Alias /icons/ "/var/www/icons/*`

```
<Directory /var/www/icons/
Options Indexes MultiViews
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

## ScriptAlias

这控制哪些目录包含服务器脚本。`ScriptAliases` 本质上与 `Aliases` 相同，只是真实目录中的文档被视为应用程序并在被请求时由服务器运行，而不是作为发送给客户端的文档。末尾 `/` 的相同规则适用于 `ScriptAlias` 指令同样适用于 `Alias`。

`#nScriptAlias /cgi-bin/ "/var/www/cgi-bin/"`

`/var/www/cgi-bin` 应该更改为你存在的 `ScriptAliased` 目录，如果你已经进行了配置。

```
<Directory /var/www/cgi-bin>
AllowOverride None
Options ExecCGI
Order allow,deny
Allow from all
</Directory>
```

## Redirect

允许你告诉客户端关于曾经存在于服务器命名空间中但已不再存在的文档。这允许你告诉客户端去哪里寻找重定向后的文档。

格式：`Redirect old-path new-path`

关于末尾 `/` 的规则适用于 `ScriptAlias` 指令同样适用于 `Alias`。

`#nScriptAlias /cgi-bin/ "/var/www/cgi-bin/"`

## 元数据信息

配置 Apache 741。

`#MetaSuffix .meta`

## 可自定义的错误响应

可自定义的错误响应（Apache 风格），这些有三种格式：

1. 纯文本
   `#ErrorDocument 500 '服务器发生了一个错误。`
   注意：`(*)` 标记将其标识为文本，它不会被输出。

2. 本地重定向
   `#ErrorDocument 404 /missing.html`
   将请求重定向到本地 URL `/missing.html`
   `#ErrorDocument 404 /cgi-bin/missing_handler.pl`
   注意：你可以使用服务器端包含将请求重定向到脚本或文档。

3. 外部重定向
   `#ErrorDocument 402 http://some.other_server.com/subscription_info.html`
   注意：与原始请求关联的许多环境变量将“不会”对脚本可用。

## HTTP 响应行为修改

以下指令修改了正常的 HTTP 响应行为。第一条指令禁用了 `Netscape 2.x` 以及伪造它的器的 `keepalive`。这些浏览器的实现存在已知问题。第二条指令用于 `Microsoft Internet Explorer 4.0b2`，它具有错误的 `HTTP/1.1` 实现，并且当用于 `301` 或 `302`（重定向）响应时，无法正确支持 `keepalive`。

```
BrowserMatch "Mozilla/2" nokealive
BrowserMatch "IE 4.0b2"; nokealive downgrade-1.0 force-response-1.0
```
