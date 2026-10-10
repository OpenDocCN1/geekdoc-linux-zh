
# `<Directory>` 容器

## 示例配置

```apache
<Directory /www/mycompany/public/htdocs/download>
    Options +Indexes
</Directory>
```

你也可以在指定路径时使用通配符。在以下示例中，`?`将匹配任何单个字符：

```apache
<Directory /www/mycompany/public/htdocs/downloa?>
    Options +Indexes
</Directory>
```

因此，诸如 `/www/mycompany/public/htdocs/download`和 `/www/mycompany/public/htdocs/downloa`这样的目录将被匹配。你还可以使用 `*`（星号）来匹配 `/`（斜杠）字符以外的任何字符序列。还可以通过添加 `~`（波浪号）字符来使用扩展正则表达式。例如：

```apache
<Directory ~ "^/www/.*/">
```

这将匹配 `/www/`下的任何子目录。请注意，基于正则表达式的 `<Directory>` 容器可能必须等到所有常规（即不使用正则表达式的）`<Directory>` 容器和 `.htaccess` 文件应用后才生效。

然后，所有正则表达式将按照其在配置文件中出现的顺序进行测试。

> **提示**
>
> 有关正则表达式的详细解释，请参见附录 C。

如果您为同一目录空间指定了多个 `<Directory>` 容器，则应用范围最窄的 `<Directory>` 容器将优先生效。例如：

```apache
<Directory /www>
    AllowOverride None
</Directory>

<Directory - "/www/mycompany/public/htdocs/*">
    AllowOverride FileInfo
</Directory>
```

根据此配置，当一个针对 `/www/mycompany/public/htdocs/somefile.cvs` 的请求到达时，`Apache`会禁用 `/www` 的每目录访问控制文件（`*.htaccess`），然后启用 `/www/mycompany/public/htdocs` 的控制文件。它还会接受来自 `/www/mycompany/public/htdocs/.htaccess` 文件内的任何 `FileInfo` 指令，例如 `DefaultType`。

## `<DirectoryMatch>`

`DirectoryMatch` 容器与 `<Directory>` 容器几乎相同，只不过它接受正则表达式作为参数，并且不需要 `-`（连字符）：使用 `<DirectoryMatch>` 和 `</DirectoryMatch>` 包围一组仅应用于指定目录及其子目录的指令。

- **语法：** `<DirectoryMatch regex> ... </DirectoryMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机

以下示例将匹配 `/www/mycompany/public/htdocs` 下名称恰好由八个大写字母组成的所有子目录；因此，`/www/mycompany/public/htdocs/AAAABBBB/`将匹配上述正则表达式。

```apache
<DirectoryMatch "^/www/mycompany/public/htdocs/[A-Z]{8}|/*">
```

> **交叉参考**
>
> 有关正则表达式的更多细节，请参见附录 B。

## `<Files>`

为了通过文件名控制访问，您需要使用 `Files` 容器。`<Files>` 部分将按照其在配置文件中出现的顺序进行处理，这在读取 `<Directory>` 部分和 `.htaccess` 文件之后，但在读取 `<Location>` 部分之前发生。

- **语法：** `<Files filename> ... </Files>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机，每目录

`filename`（文件名）参数应包含一个文件名或通配符字符串，其中 `?` 匹配任意单个字符，`*` 匹配除 `/` 字符外的任意字符序列。通过使用 `~`（波浪线）字符，您可以启用对参数的扩展正则表达式检查。例如：

```apache
<Files "\.(zip|tar|tgz|arj|zoo)$">
```

这将匹配任何扩展名为 `.zip`、`.tar`、`.tgz`、`.arj`或 `.zoo` 的文件。与 `<Directory>` 和 `<Location>` 部分不同，`<Files>` 部分可以用于 `.htaccess` 文件中。当在 `.htaccess` 文件内使用这些配置时，您无需添加路径名，因为 `.htaccess` 文件仅适用于其所在的目录。

## `<FilesMatch>`

`FilesMatch` 容器与 `<Files>` 容器完全相同，只不过它接受正则表达式作为参数。

- **语法：** `<FilesMatch regex> ... </FilesMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机，每目录

例如，以下示例将匹配任何扩展名为 `.zip`、`.tar`、`.tgz`、`.arj`和 `.zoo` 的文件。请注意，在这个容器中使用正则表达式时，不需要使用 `~`（波浪线）字符：

```apache
<FilesMatch "\.(zip|tar|tgz|arj|zoo)$">
```

## `<Location>`

`<Location>` 容器提供基于 `URL` 的访问控制。`<Location>` 容器将按照其在配置文件中出现的顺序进行处理，这在读取 `<Directory>` 容器和 `.htaccess` 文件之后发生。

- **语法：** `<Location URL> ... </Location>`
- **默认设置：** 无
- **上下文：** 服务器，虚拟主机

`URL` 参数不需要 `http://servername`。它可以使用通配符字符，例如 `?`（匹配任意单个字符）或 `*`（匹配除 `/` 字符外的任意字符序列）。您也可以在表达式前使用 `~`（波浪线）字符来使用扩展正则表达式。例如，`<Location ~ "/(my|your)/file">`将匹配诸如 `/my/file` 或 `/your/file`等 `URL`。

## `<LocationMatch>`

`LocationMatch` 容器与 `<Location>` 容器相同，只不过其参数（`URL`）是一个正则表达式，并且不需要在表达式前加 `~`（波浪线）。例如，`<LocationMatch "/(my|your)/file">`将匹配诸如 `/my/file` 或 `/your/file`等 `URL`。

- **语法：** `<LocationMatch regex> ... </LocationMatch>`
- **默认设置：** 无
- **上下文：** 服务器配置，虚拟主机

## 虚拟主机特定指令

这些指令用于创建虚拟主机。默认情况下，`Apache` 仅由 `ServerName` 指令指定的 `Web` 站点主机提供服务。然而，可以使用虚拟主机容器指令使 `Apache` 为其他 `Web` 站点提供服务。请注意，我之前在“通用配置指令”部分讨论的许多指令也适用于虚拟主机。

### `NameVirtualHost`

如果您计划使用基于名称的虚拟主机，则需要使用 `NameVirtualHost` 指令。虽然 `addr` 可以是主机名，但我建议您始终使用 `IP` 地址。

- **语法：** `NameVirtualHost addr[:port]`
- **默认设置：** 无
- **上下文：** 服务器配置

例如，对于名为 `www.mycompany.com`且使用 `IP` 地址 `192.168.1.200` 的虚拟主机，该指令和虚拟主机定义如下：

```apache
NameVirtualHost 192.168.1.200

<VirtualHost 192.168.1.200>
    ServerName www.mycompany.com
    # Other directives go here
</VirtualHost>
```

如果您在多个地址上拥有多个基于名称的主机，请为每个地址重复该指令。在清单 4-1 中，第一个 `NameVirtualHost` 指令用于 `www.mycompany.com` 和 `www.friendscompany.com` 虚拟主机。第二个容器用于 `www.myclient.com` 和 `www.herclient.com` 虚拟主机。

**清单 4-1：`NameVirtualHost` 指令**

```apache
NameVirtualHost 192.168.1.200

#
# First virtual host that corresponds to the above directive
#
```
