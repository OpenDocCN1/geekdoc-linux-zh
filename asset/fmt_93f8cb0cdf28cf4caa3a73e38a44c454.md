
`httpd.conf` 文件的第二部分涉及由您的主服务器（由 `ServerName` 指令定义的那个）处理的指令。换句话说，除非明确为虚拟主机更改，否则这些值用于默认服务器和所有虚拟主机。要为特定的虚拟主机更改相同的指令，请将这些指令添加到虚拟主机容器中。

### 设置电子邮件地址

您可以识别一个地址，以便用户在服务器出现问题时发送电子邮件。这是通过 `ServerAdmin` 指令完成的：

```
# ServerAdmin: your address, where problems with the server should be
# e-mailed.  This address appears on some server-generated pages, such
# as error documents. e.g. admin@your-domain.com
#
ServerAdmin you@your.address
```

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值是 `root@localhost`。

### 设置服务器名称

如果您的服务器名称不是确切的已注册主机或域名，您应该在此处标识您的服务器名称。正如注释所指出的，`ServerName` 指令可以设置为机器实际主机名以外的值。但是，如果服务器要是公共互联网服务器，则此其他名称在 DNS 中仍应指向您的机器。通常，www 只是机器真实名称的别名（例如，机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName jukebox.linuxtoys.net
```

如果您没有输入有效的服务器名称，Apache 会尝试使用您的主机名作为 `ServerName`。建议在此处显式输入一个 `ServerName`。

### 设置规范名称

使用 `UseCanonicalName` 指令来创建自引用 URL，如下所示：

```
# UseCanonicalName: Determines how Apache constructs self-referencing
# URLs and the SERVER_NAME and SERVER_PORT variables.
# When set "Off", Apache will use the Hostname and Port supplied
# by the client.  When set "On", Apache will use the value of the
# ServerName directive.
#
UseCanonicalName Off
```

`UseCanonicalName` 指令提供了一致性命名形式。当设置为 On 时，Apache 使用 `ServerName` 和 `Port` 指令创建引用同一台机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 为 `Off` 时，URL 由客户端指定的任何内容组成（例如，如果客户端在同一域内，URL 可以是 `http://al.linuxtoys.net/docs/` 或 `http://al/docs/`）。

这可能有问题，特别是当访问控制规则需要用户名和密码身份验证时：如果客户端针对主机 `al.linuxtoys.net` 进行了身份验证，但链接将其引导到 `www.linuxtoys.net`（物理上是同一台机器），客户端将再次被提示输入用户名和密码。建议将 `UseCanonicalName` 设置为 `On`。在前述情况下，由于对同一服务器的任何引用始终被解释为 `www.linuxtoys.net`，因此无需重复身份验证。

### 标识 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。您的 Web 内容的主位置由 `DocumentRoot` 指令设置为 `/var/www/html`。（注意此位置已从 Red Hat Linux 的早期版本中更改。位置以前在 `/home/httpd` 中。）

```
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from the directory, but
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

### 设置访问选项和覆盖

您可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认值相当严格。以下是默认设置：

```
<Directory />
   Options FollowSymLinks
        AllowOverride None
</Directory>
```

此段设置了 `Options` 和 `AllowOverride` 指令的默认权限块。`<Directory />` … `</Directory>` 标签包裹了将应用于 `/` 目录的指令（默认情况下是 `/var/www/html`，由 `DocumentRoot` 定义）。

`Options FollowSymLinks` 指令指示服务器可以跟踪目录中的符号链接，以允许访问位于计算机其他位置的内容。如果没有明确指定，`/` 目录或该目录下的任何目录中都不会激活其他特殊服务器功能。接下来，以下访问选项专门为您的 Web 服务器根目录 (`/var/www/html`) 设置。（此处去除了注释以提高清晰度。）

```
<Directory "/var/www/html">
   Options Indexes FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
</Directory>
```

如果在此文件中之前更改了 `DocumentRoot` 的值，您需要将 `/var/www/html` 更改为与该值匹配。目录的 `Options` 设置为 `Indexes` 和 `FollowSymLinks`。这些以及其他特殊服务器功能在表 21-2 中有描述。

`AllowOverride None` 指令指示服务器，`.htaccess` 文件（或 `AccessFileName` 的值）不能覆盖任何特殊的访问功能。你可以将 `None` 替换为表 21-3 中描述的任意特殊访问功能。

### 表 21-2：Options 指令的特殊服务器功能

| 功能 | 描述 |
| :--- | :--- |
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将遍历符号链接。 |
| Includes | 允许使用服务器端包含（SSI）。 |
| IncludesNOEXEC | 允许使用服务器端包含，但排除 `#exec` 元素。 |
| Indexes | 如果 `DirectoryIndex` 指令中指定的文件均不存在，`mod_autoindex` 将生成目录索引。 |
| MultiViews | 服务器允许基于用户浏览器的偏好（如首选语言、字符集和媒体类型）进行内容协商。 |
| SymLinksIfOwnerMatch | 仅当目标的所有者与链接的所有者相同时，服务器才会遍历符号链接。 |
| None | 上述所有功能均未启用。 |
| All | 上述所有功能均被启用，但 `MultiViews` 除外。`MultiViews` 必须显式启用。 |

### 表 21-3：AllowOverride 指令的特殊访问功能

| 功能 | 描述 |
| :--- | :--- |
| AuthConfig | 启用与身份验证相关的指令（如 `AuthName`、`AuthType`、`AuthUserFile`、`AuthGroupFile`、`Require` 等）。 |
| FileInfo | 启用与 MIME 相关的指令（如 `AddType`、`AddEncoding`、`AddLanguage`、`LanguagePriority` 等）。 |
| Indexes | 启用与目录索引相关的指令（如 `FancyIndexing`、`DirectoryIndex`、`IndexOptions`、`IndexIgnore`、`HeaderName`、`ReadmeName`、`AddIcon`、`AddDescription` 等）。 |
| Limit | 启用控制主机访问的指令（如 `Allow`、`Deny` 和 `Order`）。 |
| Options | 启用 `Options` 指令（如表 21-2 所述）。 |
| None | 上述所有访问功能均不可被覆盖。 |
| All | 上述所有访问功能均可被覆盖。 |
