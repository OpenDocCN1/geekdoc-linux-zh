
## `ServerAdmin` 指令

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值为 `root@localhost`。

## 设置服务器名称

如果你的服务器名称不是确切的注册主机名或域名，你应该在此处指定你的服务器名称。正如注释所述，`ServerName` 指令可以设置为除机器实际主机名以外的值。但是，如果服务器要作为公共互联网服务器，该其他名称仍应在 DNS 中指向该机器。通常，**www** 只是机器真实名称的别名（例如，机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName juicebox.linuxtoys.net
```

如果你没有输入有效的服务器名称，Apache 会尝试使用你的主机名作为 `ServerName`。建议在此处显式输入 `ServerName`。

## 设置规范名称

使用 `UseCanonicalName` 指令创建自引用 URL，如下所示：

```
# UseCanonicalName: 确定 Apache 如何构造自引用
# URL 以及 SERVER_NAME 和 SERVER_PORT 变量。
# 当设置为 "Off" 时，Apache 将使用客户端提供的
# 主机名和端口。当设置为 "On" 时，Apache 将使用
# ServerName 指令的值。
#
UseCanonicalName Off
```

`UseCanonicalName` 指令提供了一致性的命名方式。当设置为 **On** 时，Apache 使用 `ServerName` 和 `Port` 指令创建引用同一机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 为 **Off** 时，URL 由客户端指定的任何内容组成（例如，如果客户端在同一域名内，URL 可以是 `http://al.linuxtoys.net/docs/` 或 `http://al/docs/`）。

这可能存在问题，特别是在访问控制规则要求用户名和密码验证时：如果客户端已获得主机 `al.linuxtoys.net` 的验证，但链接将其发送到 `www.linuxtoys.net`（物理上是同一台机器），客户端将被提示再次输入用户名和密码。建议将 `UseCanonicalName` 设置为 **On**。在前述情况下，无需重复验证，因为对同一服务器的任何引用始终会被解释为 `www.linuxtoys.net`。

## 标识 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。主要 Web 内容位置由 `DocumentRoot` 指令设置为 `/var/www/html`。（注意，此位置自 Red Hat Linux 7 之前的版本起已更改。以前的位置在 /home/http。）

```
# DocumentRoot: 你将从该目录提供文档。
# 默认情况下，所有请求都来自该目录，但
# 可以使用符号链接和别名指向其他位置。
DocumentRoot "/var/www/html"
```

## 设置访问选项和覆盖

你可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认值相当严格。以下是默认设置：

```
<Directory />
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

此部分为 *Options* 和 *AllowOverride* 指令设置了一组默认的权限块。`<Directory />…</Directory>` 标签包围了应用于 / 目录（默认为 /var/www/html，由 *DocumentRoot* 定义）的指令。

*Options FollowSymLinks* 指令指示服务器该目录内的符号链接可以被跟踪，以允许位于计算机其他位置的内容。如果没有在后续明确指定，/ 目录或其下的任何目录中的其他特殊服务器功能都将处于非活动状态。接下来，为你的 Web 服务器根目录（/var/www/html）具体设置了以下访问选项。（为了清晰起见，我去掉了这里的注释。）

```
<Directory "/var/www/html">
  Options Indexes FollowSymLinks
  AllowOverride None
  Order allow,deny
  Allow from all
</Directory>
```

如果你在此文件中较早的位置更改了 *DocumentRoot* 的值，你需要将 /var/www/html 更改为与那个值匹配。该目录设置的 *Options* 为 *Indexes* 和 *FollowSymLinks*。这些以及其他特殊服务器功能在表 21-2 中有描述。*AllowOverride None* 指令指示服务器 .htaccess 文件（或 *AccessFileName* 的值）不能覆盖任何特殊访问功能。你可以用表 21-3 中描述的任何特殊访问功能替换 *None*。

> 注意：请记住，除非你明确启用了表 21-2 和 21-3 中描述的功能，否则该功能在你的服务器上未启用（*Indexes* 和 *FollowSymLinks* 除外）。

| 功能 | 描述 |
|---|---|
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将遍历符号链接。 |
| Includes | 允许服务器端包含。 |
| IncludesNOEXEC | 允许服务器端包含，但除外 #exec 元素。 |
| Indexes | 如果 DirectoryIndex 指令指定的文件都不存在，mod_autoindex 将生成目录索引。 |
| MultiViews | 服务器允许基于用户浏览器的偏好（如首选语言、字符集和媒体类型）进行内容协商。 |
| SymLinksIfOwnerMatch | 仅当目标的所有者与链接的所有者相同时，服务器才遍历符号链接。 |
| None | 上述功能均未启用。 |
| All | 启用上述所有功能，但 MultiViews 除外。必须显式启用。 |

| 功能 | 描述 |
|---|---|
| AuthConfig | 启用与身份验证相关的指令（AuthName, AuthType, AuthUserFile, AuthGroupFile, Require 等）。 |
| FileInfo | 启用与 MIME 相关的指令（AddType, AddEncoding, AddLanguage, LanguagePriority 等）。 |
| Indexes | 启用与目录索引相关的指令（FancyIndexing, DirectoryIndex, IndexIgnore, HeaderName, AccessFileName, AddIcon, AddDescription 等）。 |
| Limit | 启用控制主机访问的指令（Allow, Deny 和 Order）。 |
| Options | 启用 Options 指令（如表 21-5 中所述）。 |
| None | 无法覆盖上述任何访问功能。 |
| All | 可以覆盖上述所有访问功能。 |

## 在根目录中禁用索引

以下指令禁用了根目录（可能是 /var/www/html）的索引，以便在请求该目录时显示你的 index.html 或 Fedora 项目放在那里的默认文件。（在 Apache Web 服务器上列出目录内容的默认方式在本章后面的“定义索引”一节中定义。）

```
# # 禁用根目录的自动索引，如果没有其他索引页面，
# 则显示默认的欢迎页面。
#
<LocationMatch "\*/$">
    Options -Indexes
    ErrorDocument 403 /error/noindex.html
</LocationMatch>
```

## 标识用户目录

如果你的服务器上有多个用户，并且希望每个用户都能发布自己的 Web 内容，常见的做法是标识一个目录名称，用户可以在自己的主目录中创建该目录以存储这些内容。当你标识附加到用户主目录的名称时，该目录将用于响应针对用户名称（~user）对服务器的请求。此目录名称以前默认为 public_html；然而，现在默认是关闭的。

要允许访问用户的个人 Web 页面，请在 UserDir disable 行前添加注释字符（#）。然后，去除 UserDir public_html 行前的 #，使用户的个人 public_html 目录可以通过 Web 服务器访问。删除多余的注释行后，以下文本显示了启用部分的样子：

```
# UserDir: 收到 ~user 请求时，附加到用户
# 主目录的目录名称。

<IfModule mod_userdir.c>
#  UserDir disable
    UserDir public_html
</IfModule>
```

除了取消注释上一个示例中显示的 UserDir public_html 行之外，你还必须使用户的主目录和 public_html 目录对每个人可执行，以便 UserDir 指令允许访问特定用户的 public_html 目录。例如，用户 cjb 可以键入以下内容来使这些目录可访问。

```
$ chmod 711 /home/cjb
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```
