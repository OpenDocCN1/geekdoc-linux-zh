
Port `80` 是 HTTP 流量的默认端口，因此 `http://www.apache.org:80/` 等于 `http://`。如果服务器运行在不同的端口，则必须在 URL 中指定端口号。Web 服务器运行在 `80` 端口，尽管它们可以接受任何已绑定到特定服务的端口（最高到 `65536`）的连接（请参 `/etc/services` 文件中的常用服务和协议及其使用的端口列表）。只有 `root` 可以运行在特权端口（`1024` 以下）上监听连接的程序。

## 设置电子邮件地址

如果您的服务器出现问题，您可以识别一个用户发送电子邮件的地址。这是通过 `ServerAdmin` 指令完成的：

```
# ServerAdmin: 您的地址，服务器出现问题时应向该地址
# 发送电子邮件。此地址出现在某些服务器生成的页面上，如
# 错误指令。例如：admin@your-domain.com
#
ServerAdmin you@your.domain.com
```

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值是 `root@localhost`。

## 设置服务器名称

如果您的服务器名称不是您确切注册的主机或域名，那么您应该在此处标识您的服务器名称。正如注释所指，`ServerName` 指令可以设置为除机器实际主机以外的值。然而，如果该服务器是公共互联网服务器，此其他名称在 DNS 中仍应指向您的机器。

## 设置规范名称

`CanonicalName` 指令提供了一种命名形式。当它设置为 `Off` 时，Apache 使用 `ServerName` 指令来创建 URL。当它被设置为 `On` 时，它使用 `CanonicalName` 指令。

```
# CanonicalName: 服务器的规范名称。如果将其设置为
# On，Apache 将使用此名称 own ServerName
# 指令来构造 URL。
#
CanonicalName Off
```

## 标识 HTTP 内容目录

有几个指令决定了 Web 内容的位置。Web 内容的主要位置通过 `DocumentRoot` 指令设置为 `/var/www/html`。

```
# DocumentRoot: 您提供文档的目录。默认情况下，
# 所有请求都来自该目录，符号链接和别名
# 可用于指向其他位置。
DocumentRoot "/var/www/html"
```

## 设置访问选项和覆盖

您为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认设置非常严格。以下是默认设置：

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

此段为 `Options` 和 `AllowOverride` 指令设置了一个默认权限块。`<Directory>` ... `</Directory>` 标签包含了应用于 `/` 目录（即根据 `DocumentRoot` 定义的 `/var/www/html`）的指令。

`Options FollowSymLinks` 指令指示服务器跟踪目录内的符号链接访问访问位置的内容。如果不显式指定，`/ `目录或其下方的任何目录都不会启用其他特殊功能。接下来，为您的 Web 服务器的根目录（`/var/www/html`）特别设置了以下访问选项。

```
<Directory "/var/www/html">
Options FollowSymLinks
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

如果您在该文件的早期部分更改了 `DocumentRoot` 的值，则您需要更改 `/var/www/html` 以匹配该值。为目录设置的 `Options` 是 `Indexes` 和 `FollowSymLinks`。这些以及其他特殊的服务器功能见表 21-2。`AllowOverride None` 指令指示服务器不要使用 `.htaccess` 文件。

## 第 21 章：设置 Web 服务器

`FileName` 无法覆盖任何特殊的访问功能。你可以将 `None` 替换为表 21-3 中描述的任何特殊访问功能。

> 注意：请记住，除非你特地启用了表 21-2 和 21-3 中描述的功能，否则该功能对你的服务器未启用（`Indexes` 和 `FollowSymLinks` 除外）。

### 表 21-2：Options 指令的特殊服务器功能

| 特性 | 说明 |
| --- | --- |
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将遍历符号链接。 |
| Includes | 允许服务器端包含。 |
| IncludesNOEXEC | 允许服务器端包含，但 `#exec` 元素除外。 |
| Indexes | 如果 `DirectoryIndex` 指令中指定的指定都不存在，则由 `mod_autoindex` 生成一个目录索引。 |
| MultiViews | 服务器允许根据用户浏览器的偏好进行内容协商。 |
| SymLinksIfOwnerMatch | 仅当目标的所有者与链接的所有者相同时，服务器才会遍历符号链接。 |
| None | 以上所有功能均未启用。 |
| All | 以上所有功能均启用，但 `MultiViews` 除外。必须显式启用。 |

### 表 21-3：AllowOverride 指令的特殊访问功能

| 特性 | 说明 |
| --- | --- |
| AuthConfig | 启用与身份验证相关的指令。 |
| FileInfo | 启用与 MIME 相关的指令。 |
| Indexes | 启用与目录索引相关的指令。 |
| Limit | 启用控制主机访问的指令。 |
| Options | 启用 `Options` 指令。 |
| None | 以上访问功能均无法覆盖。 |
| All | 以上访问功能均可以覆盖。 |

### 802 第 4 部分：Fedora 网络与服务器设置

## 在根目录下禁用索引

```bash
# 禁用根目录的自动索引，如果其他其他索引页，
# 则显示一个默认的欢迎页。
<LocationMatch "$/">
  Options -Indexes
  ErrorDocument 403 /error/noindex.html
</LocationMatch>
```

## 识别用户目录

如果你的服务器上有多个用户，并且你希望每个用户都能发布自己的 Web 内容，通常的做法是识别一个用户可以在其主目录中创建的目录名称，用以存储这些内容。当你确定了附加在用户名称主目录名后的名称时，该目录将用于响应针对该用户命名的服务器请求。该目录名称默认被设置为 `public_html`；但现在默认是关闭的。

要允许访问用户的个人页面，请在 `UserDir disable` 禁用行添加注释符号 `#`。然后删除 `UserDir public_html` 行前的 `#`，以便使用户能够通过 Web 服务器访问其个人的 `public_html` 目录。在移除多余的注释行后，以下文本显示了启用部分的内容：

```bash
# UserDir: 当接收到 -user 请求时，附加到用户
# 主目录的目录名称。
```

```bash
<ifModule mod_userdir.c>
# UserDir disable
UserDir public_html
</ifModule>
```

除了取消上例所示的 `UserDir public_html` 行的注释外，你还必须让用户的主目录和 `public_html` 目录对所有人都是可执行的，这样 `UserDir` 指令才能允许访问特定用户的 `public_html` 目录。例如，用户 `cjb` 可以输入以下命令使这些目录可访问。

```bash
$ chmod 711 /home/cjb
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```

为了让 `UserDir` 正常工作，还必须加载 `mod_userdir` 模块。

`UserDir` 有两种方式可以处理包含用户名的传入请求。一种可能的格式是识别各个用户公开访问目录的物理路径名。另一种可以指定请求重定向到的 URL。表 21-4 给出了一些示例，使用 `http://www.mybox.com/-cjb/proj/c004.html` 作为示例请求。

### 表 21-4：UserDir 路径和 URL 示例

| UserDir 指令 | 引用的路径或 URL |
| --- | --- |
| UserDir public_html | -cjb/public_html/proj/c004.html |
| UserDir /public/*/WWW | /public/cjb/WWW/proj/c004.html |
| UserDir /usr/local/web | /usr/local/web/cjb/proj/c004.html |
| UserDir http://www.mybox.com/users | http://www.mybox.com/users/cjb/proj/c004.html |
| UserDir http://www.mybox.com/* | http://www.mybox.com/-cjb/proj/c004.html |
| UserDir http://www.mybox.com/*/html | http://www.mybox.com/cjb/html/proj/j004.html |

`UserDir` 指令也可用于显式允许或拒绝特定用户的 `UserDir-to-path`。例如，包含以下行可以避免发布不应公开的数据：`UserDir disable root`

或者，使用以下行来禁用所有用户的翻译：

```bash
UserDir disable
UserDir enable cjb jsmith
```
