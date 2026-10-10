
本章后面关于“配置模块和相关服务（`/etc/httpd/conf.d\*.conf`）”的部分，描述了 `conf.d` 目录中一些您可能会感兴趣的配置文件。

## 选择服务器的用户和组

`httpd` 守护进程不必以 root 用户身份运行；默认情况下它**不**以 root 身份运行这一事实使您的系统更加安全。通过设置 `User` 和 `Group` 条目，您可以让 `httpd` 守护进程以与另一个用户和组关联的权限运行：

```
User apache
Group apache
```

默认情况下，`apache` 被定义为服务器的用户和组。如果您更改 `User` 和 `Group` 指令，则应指定一个非特权实体。这样做可以最大限度地降低如果您的站点被入侵时造成损害的风险。启动的第一个守护进程以 root 身份运行。这是为了将服务器绑定到低端口号并切换到由 `User` 和 `Group` 指令指定的用户和组所必需的。所有其他进程都在由这些指令定义的用户 ID `UID` 和组 ID `GID` 下运行。

## 设置主服务器配置

`httpd.conf` 文件的第二部分与由主服务器（由 `ServerName` 指令定义的那个服务器）处理的指令有关。换句话说，除非为虚拟主机明确更改，否则这些值被默认服务器和所有虚拟主机使用。要更改特定虚拟主机的相同指令，请将它们添加在虚拟主机容器内。

## 设置电子邮件地址

您可以指定一个地址，以便用户在遇到服务器问题时发送电子邮件。这是通过 `ServerAdmin` 指令完成的：

```
ServerAdmin you@your.address
```

`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值是 `root@localhost`。

## 设置服务器名称

如果您的服务器名称不是您确切注册的托管名或域名，您应该在此处标识您的服务器名称。正如注释所指出的，`ServerName` 指令可以设置为不同于机器实际主机名的值。然而，如果服务器要作为公共互联网服务器，这个其他名称仍然应在 DNS 中指向您的机器。通常，`www` 只是机器真实名称的别名（例如，一台机器可能响应 `www.linuxtoys.net`，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName jukebox.linuxtoys.net
```

如果您没有输入有效的服务器名称，Apache 会尝试使用您的主机名作为 `ServerName`。我建议在此处显式输入 `ServerName`。

## 设置标准名称

您可能需要配置服务器如何确定其自身的名称和端口。为此，您可以修改 `UseCanonicalName` 指令以创建自引用 URL。这使得 Apache 能够使用指定的主机名和端口来构建服务器的标准名称。由 `UseCanonicalName` 产生的值用于所有自引用 URL 以及 CGI 中 `SERVER_NAME` 和 `SERVER_PORT` 的值。您可以将 `UseCanonicalName` 指令设置为 `On`、`Off` 或 `DNS`。

为了允许 Apache 使用主机名和端口形成自引用 URL，请按以下方式设置 `UseCanonicalName` 指令：

```
UseCanonicalName Off
```

使用 `UseCanonicalName` 指令可以使标识服务器的名称更加一致。当指令设置为 `On` 时，Apache 使用 `ServerName` 和 `Port` 指令创建引用同一机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 设置为 `Off` 时，URL 由客户端指定的内容组成（例如，如果客户端在同一域内，URL 可以是 `http://abc.linuxtoys.net/docs/` 或 `http://abc/docs/`）。

这可能存在问题，特别是当访问控制规则需要用户名和密码认证时：如果客户端针对主机 `abc.linuxtoys.net` 进行了认证，但链接将其发送到 `www.linuxtoys.net`（物理上是同一台机器），客户端将再次被提示输入用户名和密码。我建议将 `UseCanonicalName` 设置为 `On`，以便在上述情况下，由于对同一服务器的任何引用始终被解释为 `www.linuxtoys.net`，因此无需重复认证。

最后一个选项，`UseCanonicalName DNS`，在您想要部署虚拟托管环境以支持不提供 `Host:` 头部的旧客户端时可以配置。使用此选项时，Apache 会对客户端连接到的服务器 IP 地址执行反向 DNS 查找，以确定自引用 URL。

## 标识 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。您的 Web 内容的主要位置由 `DocumentRoot` 指令设置为 `/var/www/html`。请注意路径名称末尾不使用斜杠。

```
DocumentRoot "/var/www/html"
```

（请注意，此位置与 Red Hat Linux 早期版本有所变化。以前的位置是 `/home/http`。将 Web 内容移出 `/home` 有助于将 `/home` 中的用户目录与系统文件分开。）

## 设置访问选项和覆盖

您可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认值（如下所示）相当严格。

```
<Directory />
   Options FollowSymLinks
   AllowOverride None
</Directory>
```

此段为 `Options` 和 `AllowOverride` 指令设置默认的权限块。`<Directory />...</Directory>` 标签包围了应用于 `/` 目录（默认情况下由 `DocumentRoot` 定义为 `/var/www/html`）的指令。

`Options FollowSymLinks` 指令指示服务器可以跟踪目录中的符号链接，以允许位于计算机其他位置的内容。如果没有稍后明确指定，`/` 目录或其下任何目录中的其他特殊服务器功能都不会激活。接下来，以下访问选项专门用于您的 Web 服务器根目录（`/var/www/html`）。(此处为清晰起见删除了注释。)

```
<Directory "/var/www/html">
   Options Indexes FollowSymLinks
   AllowOverride None
   Order allow,deny
   Allow from all
</Directory>
```

如果您之前在此文件中更改了 `DocumentRoot` 的值，您需要将 `/var/www/html` 更改为匹配该值。为该目录设置的 `Options` 是 `Indexes` 和 `FollowSymLinks`。这些和其他特殊服务器功能在表 20-2 中描述。`AllowOverride None` 指令指示服务器 `.htaccess` 文件（或 `AccessFileName` 的值）不能覆盖任何特殊访问功能。您可以将 `None` 替换为表 20-3 中描述的任何特殊访问功能。

### 表 20-2：Options 指令的特殊服务器功能

| 功能 | 描述 |
| --- | --- |
| ExecCGI | 允许执行 CGI 脚本。 |
| FollowSymLinks | 服务器将遍历符号链接。 |
| Includes | 允许服务器端包含。 |
| IncludesNOEXEC | 允许服务器端包含，但排除 #exec 元素。 |
| Indexes | 如果 DirectoryIndex 指令指定的文件均不存在，将由 mod_autoindex 生成目录索引。 |
| MultiViews | 服务器允许基于用户浏览器的偏好（如首选语言、字符集和媒体类型）进行内容协商。 |
| SymLinksIfOwnerMatch | 仅当目标的所有者与链接的所有者相同时，服务器才遍历符号链接。 |
| None | 未启用上述任何功能。 |
| All | 启用上述所有功能，但 MultiViews 除外。这需要明确启用。 |

### 表 20-3：AllowOverride 指令的特殊访问功能

| 功能 | 描述 |
|---|---|
| AuthConfig | 启用认证相关指令（AuthName, AuthType, AuthUserFile, AuthGroupFile, Require 等）。 |
| FileInfo | 启用 MIME 相关指令（AddType, AddEncoding, AddLanguage, LanguagePriority 等）。 |
