
`ServerAdmin` 指令可以设置为任何有效的电子邮件地址。默认值为 `root@localhost`。

## 设置服务器名称

如果你的服务器名称不是你准确注册的主机名或域名，你可以在此处标识你的服务器名称。正如注释所指，`ServerName` 指令可以设置为你机器实际主机名以外的其他值。然而，如果该服务器要作为公共 Internet 器，该其他值仍应在 DNS 中指向你的名称。通常情况下，它是机器真实名称的别名（例如，一台机器可能对 `www.linuxtoys.net` 响应，但其真实名称可能是 `al.linuxtoys.net`）。

```
ServerName jukebox.linuxtoys.net
```

如果你没有输入有效的服务器名称，Apache 会尝试使用你的主机名作为 `ServerName`。建议在此处显式地输入一个 `ServerName`。

## 设置规范名称

使用 `CanonicalName` 指令创建自引用的 URL，如下：

`UseCanonicalName` 提供了一种命名一致性。当它被设置为 `On` 时，Apache 使用 `ServerName` 和 `Port` 指令创建一个引用同一台机器上文件的 URL（例如，`http://www.linuxtoys.net/docs/`）。当 `UseCanonicalName` 设置为 `Off` 时，URL 将由客户端指定的任何内容组成（例如，URL 可能是 `http://al.linuxtoys.net/docs/` 或如果客户端在同一域名内，则是 `http://al/docs/`）。

这可能会导致问题，特别是当访问控制规则需要用户名和密码验证时：如果客户端对主机 `al.linuxtoys.net` 通过了身份验证，但一个链接将他发送到 `www.linuxtoys.net`（物理上是同一台机器），客户端将被提示再次输入用户名和密码。建议将 `UseCanonicalName` 设置为 `On`。在的情况下，不需要重复身份验证，因为对同一服务器的任何引用将始终被解释为 `www.linuxtoys.net`。

## 识别 HTTP 内容目录

有几个指令用于确定服务器 Web 内容的位置。`DocumentRoot` 指令将你的 Web 内容的主要位置设置为 `/var/www/html/`。（注意，此位置在 Red Hat Linux 7 之前的版本中已更改。该位置位于 `/home/http`）。

```
# DocumentRoot: 你从中提供文档的目录。
# 默认情况下，所有请求都来自该目录，
# 可以使用符号链接和别名指向其他位置。
DocumentRoot="/var/www/html"
```

## 设置访问选项和覆盖

你可以为 Web 服务器目录结构中的每个目录设置单独的访问权限。默认设置是相当严格的。以下是默认设置：

```
<Directory />
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

此段为 `Options` 和 `AllowOverride` 指令设置了一个默认权限块。`<Directory>...</Directory>` 标签包围了要应用于该目录的指令（默认是 `/var/www/html`，由 `DocumentRoot` 定义）。

`Options FollowSymLinks` 指令告诉服务器，目录内的符号链接可以被跟踪，以允许访问计算机上其他位置的内容。在稍后显式指定之前，该目录或其下方的任何目录中的其他其他特殊服务器功能将不会激活。接下来，专门为你的 Web 服务器根目录 (`/var/www/html`) 设置了以下访问选项。（我在此处删除了注释以便清晰）。

```
<Directory "/var/www/html">
  Options Indexes FollowSymLinks
  AllowOverride None
  Order allow, deny
  Allow from all
</Directory>
```

如果你在此文件的较早部分更改了 Document Root 的值，你需要更改 `/var/www/html` 以匹配该值。为目录设置的 `Options` 是 `Indexes` 和 `FollowSymLinks`。这些和其他特殊服务器功能在表 21 中描述。除非你在表 21 中显式启用它，否则 `AllowOverride` 指令无法覆盖任何 `.htaccess` 文件（或文件名）。注意：21：设置 Web 服务器 813

## 第 21 章：设置 Web 服务器 817

`public_html` 目录。例如，用户 `cjb` 可以输入以下命令使这些目录变为可访问。

```
$ chmod 711 /home/cjb
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```

要使 `UserDir` 起作用，必须加载 `mod_userdir` 模块（默认已加载）。

`UserDir` 指令可以通过两种方式处理包含用户名（例如 `~cjb`）的传入请求。其中一种可能的格式是识别个人公共访问目录的物理路径名。另一种可以指定请求将被重定向到的 URL。表 21-4 展示了几个示例，使用 URL `http://www.mybox.com/~cjb/proj/c004.html` 作为示例请求。

### 表 21-4：UserDir 路径名和 URL 示例

| UserDir | 被引用的路径或 URL |
|---|---|
| UserDir/public_html | ~cjb/public_html/proj/c004.html |
| UserDir/public/*WWW | /public/cjb/WWW/proj/c004.html |
| UserDir/usr/local/web | /usr/local/web/cjb/proj/c004.html |
| UserDir http://www.mybox.com/users | http://www.mybox.com/cjb/proj/c004.html |
| UserDir http://www.mybox.com/~* | http://www.mybox.com/~cjb/proj/c004.html |
| UserDir http://www.mybox.com/*/html | http://www.mybox.com/cjb/html/proj/c004.html |

`UserDir` 指令也可用于显式地允许或拒绝特定用户的用户名到路径名的翻译。例如，包含以下行可以避免发布不应公开的数据：

```
UserDir disable root
```

或者，使用以下行禁用除极少数用户以外的所有翻译：

```
UserDir disable
UserDir enable wilhelm cjb smith
```

`DirectoryIndex` 指令建立了一个文件列表，当传入请求指定目录而非文件时，将使用该列表。由于它是目录，它会被翻译为 `http://www.mybox.com/~jsmith/`。现在将在该目录下搜索 `DirectoryIndex` 指令中列出的任何文件。第一个匹配项（来自默认列表 `index.html` 和 `index.html.var`）将用作该目录的默认文档。如果没有找到任何这些文件，且没有选择 `Indexes` 选项（如 `httpd.conf` 文件所示），服务器将自动生成目录中文件的索引。

```
# DirectoryIndex: 设置当请求目录时 Apache 
# 将提供的文件。
# index.html.var 文件（一种类型映射）用于交付通过内容
# 协商的文档。MultiViews 选项可用于相同的
# 目的，但它的速度慢得多。
# DirectoryIndex index.html index.html.var
```

## 设置目录访问控制

你和你的用户可以为每个目录添加一个访问文件，以控制对该目录的访问。默认情况下，`AccessFileName` 指令将 `.htaccess` 作为包含该信息的文件。以下行设置了文件名，并防止网站访问者查看该文件的内容。如果你将文件更改为 `.htaccess` 以外的任何名称，请确保更改下方拒绝访问该文件的行（`^\\.htac`）。

```
# AccessFileName: 在每个目录中查找的用于访问
# 控制信息的文件名。
AccessFileName .htaccess

<Files "^\\.ht">
  Order allow, deny
```

# AccessFileName: 在每个目录中查找的用于访问
# 控制信息的文件名。
AccessFileName .htaccess

<Files "^\\.ht">
  Order allow, deny
```

如果你将文件更改为 `.htaccess` 以外的任何名称，请确保更改下方拒绝访问该文件的行（`^\\.htac`）。
