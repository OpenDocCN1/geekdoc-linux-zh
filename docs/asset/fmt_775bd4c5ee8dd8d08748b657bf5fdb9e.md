
```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

此段落为 `Options` 和 `AllowOverride` 指令设置了一个默认权限块。`<Directory>...</Directory>` 标签包含了要应用于该目录的指令（默认由 `DocumentRoot` 定义，为 `/var/www/html`）。

`Options FollowSymLinks` 指令告诉服务器，可以跟踪目录内的符号链接，以允许访问位于计算机上其他位置的内容。除非稍后显式指定，否则 `/directory` 或其任何子目录下的其他特殊服务器功能将不会被激活。接下来，为你的 Web 服务器的根目录（`/var/www/html`）专门设置了以下访问选项。（为了清晰起见，我删除了注释。）

```
<Directory "/var/www/html*>
Options Indexes FollowSymLinks
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

## 第 21 章：设置 Web 服务器 847

如果你在此值之前之前更改了 `DocumentRoot` 的值，你需要将 `/var/www/html` 更改为匹配该值。`Options` 设置适用于 `Indexes` 和 `FollowSymLinks` 目录。这些和其他服务器功能在表 21-2 中描述。`AllowOverride` 指令告诉服务器，`.htaccess` 文件（或 `AccessFileName` 的值）不能覆盖任何特殊功能。你可以将 `None` 替换为表 21-3 中描述的任何特殊功能。

### 表 21-2：Options 指令的特殊服务器功能

| 特性 | 描述 |
|---|---|
| `ExecCGI` | 允许执行 CGI 脚本。 |
| `FollowSymLinks` | 服务器允许符号链接。 |
| `Includes` | 允许服务器端包含（SSI）。 |
| `IncludesNOEXEC` | 除 #exec 元素外。 |
| `Indexes` | 如果 `DirectoryIndex` 中指定的任何文件都不存在，则将由 `mod_autoindex` 生成目录索引。 |
| `MultiViews` | 服务器允许根据用户浏览器的偏好（如首选语言、字符集和媒体类型）进行内容协商。 |
| `SymLinksOwnerMatch` | 仅当目标的所有者与链接的所有者相同时，服务器才允许符号链接。 |
| `None` | 未启用上述任何功能。 |
| `All` | 启用上述所有功能，但 `MultiViews` 除外。这必须显式启用。 |

### 表 21-3：AllowOverride 指令的特殊访问功能

| 特性 | 描述 |
|---|---|
| `AuthConfig` | 启用与认证相关的指令（`AuthName`、`AuthType`、`AuthUserFile`、`AuthGroupFile`、`Require` 等）。 |
| `FileInfo` | 启用与 MIME 相关的指令（`AdType`、`AddEncoding`、`AddLanguage`、`LanguagePriority` 等）。 |
| `Indexes` | 启用与目录索引相关的指令（`FancyIndexing`、`DirectoryIndex`、`IndexOptions`、`IndexIgnore`、`HeaderName`、`ReadReadme`、`AddIcon`、`AddDescription` 等）。 |
| `Limit` | 启用控制主机访问的指令（`Allow`、`Deny` 和 `Order`）。 |
| `Options` | 启用 `Options` 指令（如表 21-2 所示）。 |

## 第四部分：Fedora 和 RHEL 网络和服务器设置

| 特性 | 描述 |
| --- | --- |
| `None` | 上述访问功能均不可被覆盖。 |
| `All` | 上述访问功能均可以被覆盖。 |

> **注意：** 请记住，除非你专门启用表 21-2 和 21-3 中描述的功能，否则该功能在你的服务器上不会启用（`Indexes` 和 `FollowSymLinks` 除外）。

## 识别用户目录

如果你的服务器上有多个用户，并且你希望他们能够发布自己的 Web 内容，通常做法是识别一个用户可以在其主目录中创建的目录名称以存储内容。当你确定附加到用户主目录的名称时，`directory` 被用于响应对服务器名称的请求（`~user`）。该目录名以前是 `public_html`，但现在默认是关闭的。

要允许禁用用户的个人 Web 页面，请在 `UserDir` 行添加注释字符 (`#`)。然后删除 `UserDir public_html` 行中的 `#`，以便使用户通过 Web 服务器访问用户的个人 `public_html` 目录。在删除多余的注释行后，下文显示了启用部分的内容：

- # `UserDir`: 附加到用户目录后的目录名称。

```
<IfModule userdir>
# UserDir disable
UserDir public_html
</IfModule>
```

在删除额外的注释行后，下文显示了启用部分的内容：

- # `UserDir`: 附加到用户目录的目录名称，当接收到 `~user` 请求时。

为了允许通过 Web 服务器访问用户的个人 `public_html` 目录。例如，为了让 `UserDir` 工作，你还需要执行以下命令设置 `cjb` 的主目录和 `public_html` 目录的权限：

```
$ chmod 711 /home/cjb
$ chmod 755 /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```

为了让 `UserDir` 工作，必须加载 `mod_userdir` 模块。

### 设置目录的默认索引

`DirectoryIndex` 建立了一个当传入的请求指定目录而不是文件时使用的文件列表。例如，客户端请求 URL `http://www.mybox.com/~jsmith`。因为这是一个目录，它会被自动翻译为 `http://www.mybox.com/~jsmith/`。现在该目录将搜索 `DirectoryIndex` 指令列出的任何文件。第一个匹配项（来自默认列表 `index.html` 和 `index.html.var`）将用作该目录的默认文档。如果这些文件都不存在，并且选择了 `Options` 选项（如 `httpd.conf` 文件所示），则服务器将自动生成目录文件的索引。

## 第四部分：Fedora 和 RHEL 网络与服务器设置

```
# DirectoryIndex: 设置当请求目录时 Apache 将提供的文件。
#
# index.html.var 文件（一种类型映射）用于交付经过内容-
# 协商的文档。MultiViews 选项也可以用于相同目的，
# 但它的运行速度要慢得多。
# DirectoryIndex index.html index.var
```

## 设置目录访问控制

你和用户可以在每个目录中添加一个访问文件来控制对该目录的访问。默认情况下，`AccessFileName` 指令将 `.htaccess` 设置为包含此类信息的文件。以下行设置了防止 Web 访问者查看该文件的内容。如果您将文件更改为 `.htaccess` 以外的名称，请务必修改下方拒绝访问该文件的行（"^\.ht"）。

```
# AccessFileName: 在每个目录中查找的用于访问控制
# 的信息的文件名。
#
AccessFileName .htaccess
```

```apache
<Files ~"^\.ht">
  Order allow,deny
  Deny from all
</Files>
```

你可以像在 `httpd.conf` 文件中那样在 `.htaccess` 文件中添加相同的访问指令。通常情况下，在 `httpd.conf` 文件中使用 `<Directory>` 指令比创建 `.htaccess` 文件更有效率。通过 `<Directory>` 指令，你可以专门识别与该目录单独关联的访问控制。由于指令适用于当前目录下的所有子目录，如果你在某个目录中添加了 `.htaccess` 文件，Apache 必须搜索该点以上的所有目录（例如，/、var/www/www/ 等），以包含这些目录中可能的 `.htaccess` 文件的设置。

## 设置 MIME 类型 默认值

MIME 类型定义文件的位置由 `TypesConfig` 指令定义。`DefaultType` 指令设置 MIME 类型：

```
# TypesConfig 描述了 mime.types 文件（或等效文件）
# 所在。
TypesConfig /etc/mime.types
```
