
`combined` 格式将其他三种日志文件格式中的所有信息包含在一行中。这种格式适用于将所有与连接相关的日志条目存储在一个集中文件中。`combinedio` 格式默认被注释掉，可以通过移除 `#` 字符来启用，以记录实际接收（`%oi`）和发送（`%os`）的字节数，前提条件是加载了 `mod_logio` 模块。

`CustomLog` 指令将已定义的 `LogFormat` 格式之一分配给一个文件名（同样，指定为绝对路径名或相对于 `ServerRoot` 的路径名）。唯一的未注释定义将 `combined` 格式分配给 `/etc/httpd/logs/access_log` 文件。若要单独保留代理或引用源信息，请取消相应定义的注释。此外，您也可以选择注释掉 `CustomLog logs/access_log combined` 行，并改用 `common` 格式的定义。

## 添加签名

由 Apache 服务器生成的任何页面都可以在页面底部添加一行签名。服务器生成页面的示例包括目录列表、错误页面、状态页面或信息页面。`ServerSignature` 指令可以设置为 `On`、`Off` 或 `EMail`。以下是 `ServerSignature` 的默认显示方式：

```
# Optionally add a line containing the server version and virtual # host name to server-generated pages (error documents, FTP directory # listings, mod_status and mod_info output etc., but not CGI generated # documents). # Set to "EMail" to also include a mailto: link to the ServerAdmin. # Set to one of: On | Off | EMail # ServerSignature On
```

当 `ServerSignature` 设为 `On` 时，服务器生成的页面底部会出现类似下面的一行：

```
Apache/2.0.48 (Fedora) Server at toys.linuxtoxys.net Port 80
```

当 `ServerSignature` 设置为 `EMail` 时，会在签名行中添加指向 Web 页面管理电子邮件账户的链接（服务器名称变为链接）。如果该指令设置为 `Off`，则该行根本不会显示。在启用 SSL 或 webdav 的情况下，此信息也会出现在服务器签名中。

## 别名重定向内容

定义别名内容的方式有很多种。这包括 `Alias` 和 `ScriptAlias` 指令。以下是 `httpd.conf` 中的别名相关设置（已移除注释）：

```
# # Aliases: Add here as many aliases as you need (with no limit). The format is # Alias fakename realname # Alias /icons/ "/var/www/icons/" <Directory "/var/www/icons"> Options Indexes MultiViews FollowSymLinks AllowOverride None Order allow,deny
 Allow from all
</Directory>

# ScriptAlias: This controls which directories contain server scripts.
ScriptAlias "/cgi-bin/" "/var/www/cgi-bin/"
# "/var/www/cgi-bin/" should be changed to whatever your ScriptAliased
# CGI directory exists, if you have that configured.
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

`Alias` 指令指向一个文件系统位置（不一定在 `DocumentRoot` 内）。例如，如果在配置中包含以下行，对 `/bigjob` 中文档（http://www.mybox.com/bigjob/index.html）的请求将导致检索 `/home/newguy/proj/index.html`。

```
Alias /bigjob /home/newguy/proj
```

`icons` 别名允许访问 Apache 用于您的网站 Web 服务器的 `icons`。`icons` 目录可从 `/var/www` 目录访问。

`ScriptAlias` 指令执行相关功能，但它所别名的目录包含可执行代码（通常是 CGI 脚本）。其语法与 `Alias` 指令相同。每次使用 `ScriptAlias` 时都要特别注意。因为 `ScriptAlias` 定义了服务器上可从 Web 内容运行的脚本所在位置，所以应确保仅分配那些包含经过安全验证且不会在系统中打开安全漏洞的脚本的目录。

### 重定向旧内容请求

随着 Web 服务器上的内容变化，一些内容将变得过时，而其他内容可能会移动到文件系统中的不同位置或不同的服务器。使用 `Redirect` 指令，您可以将旧内容的请求重定向到新位置。

默认情况下，您的 Apache 服务器没有设置任何 `Redirect` 指令。然而，您可以取消以下示例的注释并根据您的需要进行定制：

```
# Redirect permanent /foo http://www.example.com/bar
```

`Redirect` 可用于指示客户端其寻找的文档已移至其他位置（同一服务器或外部位置），只需指出旧位置和新位置即可。如果之前的 `Redirect` 选项已生效，客户端尝试访问 `http://www.mybox.com/foo` 将被重定向到 `http://www.example.com/bar`。

除了使用 `permanent` 作为 `Redirect` 的服务（这将产生重定向状态 301）外，还可以使用 `temp`（重定向状态 302）、`seeother`（替代状态 303）或 `gone`（永久移除状态 401）。您还可以提供 300 到 399 之间的任何状态代码作为服务，这些代码代表不同的错误响应。（这些数字是 HTTP 状态代码。）

> **交叉参考：** HTTP 状态代码在 RFC 2616 中作为 HTTP 协议的一部分进行定义。请参考该文档，网址为 www.w3.org/Protocols/rfc2616/rfc2616.txt。

### 定义索引

让您的 Apache 服务器为不同类型的文件显示不同的图标是可行的。要使用此功能，`IndexOptions` 应设置为 `FancyIndexing`，并且应使用 `AddIconByEncoding`、`AddIconByType` 和 `AddIcon` 指令：
