
上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<Location>`

将指令应用于指定的 `URI`。

```
<Location URI> ... </Location>
```

其中 `URI` 指向内容，并指定容器中指令应用的文件或目录层级的根。虽然 `<Directory>` 容器指向本地文件系统内部，但 `<Location>` 指向本地文件系统外部。`URI` 可以包含通配符；`a*` 不匹配 `a`。

以下 `<Location>` 容器限制来自 `example.net` 域的客户端对 `http://server/pop` 的访问，其中 `server` 是服务器的 `FQDN`：

```
<Location /pop>
Order deny,allow
deny from all
</Location>
```

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<Files>`

将指令应用于指定的目录。

```
<Files directory> ... </Files>
```

其中 `directory` 是一个绝对路径，用于指定容器中要应用的普通文件指令的目录层级名称。该目录可以包含通配符；`a*` 不匹配 `a`。此容器与 `<Directory>` 类似，但它适用于普通文件而不是目录。

以下来自 `Red Hat` `http.conf` 的指令拒绝对所有以 `ht` 开头的文件名的访问。波浪号 (`~`) 会改变 `Apache` 解释字符串的方式。如果没有波浪号，它将是简单匹配，并解释特殊字符（第 22 页）。如果有波浪号，`Apache` 将字符串解释为正则表达式（第 67 页）。

```
<Files ~ "ht">
Order allow,deny
Deny from all
</Files>
```

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<IfModule>`

如果加载了指定的模块，则应用指令。

```
<IfModule [module-name]> ... </IfModule>
```

其中 `module-name` 是为 `Apache` 测试的模块名称（第 820 页）。如果 `module-name` 已加载或未加载，`Apache` 都会匹配此容器中的指令。

如果你指定了针对未加载模块的配置指令，`Apache` 将不会启动。

以下来自 `Red Hat` `http.conf` 的 `<IfModule>` 容器取决于 `mod_mime_magic.c` 模块是否加载。如果加载了此模块，`Apache` 执行 `MIMEMagicFile`，它告诉 `mod_mime_magic.c` 模块其提示文件的位置。

```
<IfModule mod_mime_magic.c>
MIMEMagicFile conf/magic
</IfModule>
```

查看第 815 页 `<IfModule>` 容器的另一个示例。

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<Limit>`

将访问控制指令限制为指定的 `HTTP` 方法。

```
<Limit method [method]> ... </Limit>
```

其中 `method` 是一个 `HTTP` 方法。`HTTP` 方法指定了在 `URI` 上执行的操作。最常用的方法是 `GET`、`PUT`、`POST` 和 `OPTIONS`；方法名区分大小写。`GET` 是默认方法，发送 `URI` 指示的任何数据。`PUT` 将通信主体存储在指定的 `URI` 上。`POST` 创建包含指定 `URI` 主体的新文档。`OPTIONS` 请求有关服务器能力的信息。

此容器将一组访问控制指令绑定到指定的 `HTTP` 方法：只有受 `<Limit>` 容器限制的方法受此组指令的影响。

以下是来自非 `example.com` 子域的系统的 `HTTP` 上传 (`PUT`) 示例：

```
<Limit PUT>
order deny.allow
deny from all
allow from .example.com
</Limit>
```

## 注意：使用 `<LimitExcept>` 代替 `<Limit>`

使用 `<LimitExcept>` 容器代替 `<Limit>` 容器更安全，因为前者可以防止任意方法。当你使用 `<Limit>` 时，必须小心地显式命名该组指令可能影响的所有可能方法。

仍然不要将访问控制指令放在任何容器中。

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<LimitExcept>`

将访问控制指令限制为除指定 `HTTP` 方法之外的所有方法。

```
<LimitExcept method [method]> ... </LimitExcept>
```

其中 `method` 是一个 `HTTP` 方法。关于方法的讨论请参阅 `<Limit>`。

此容器导致一组访问控制指令不绑定到指定的 `HTTP` 方法：不在 `<LimitExcept>` 中的方法受此组指令的影响。

以下 `<LimitExcept>` 内部的访问控制指令影响 `GET` 和 `POST` 以外的 `HTTP` 方法。你可以将其放在 `<Directory>` 容器中以限制其范围：

```
<LimitExcept GET POST OPTIONS>
order deny.allow
deny from all
</LimitExcept>
```

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<Location>`

将指令应用于指定的 `URI`。

```
<Location URI> ... </Location>
```

其中 `URI` 指向内容，并指定容器中指令应用的文件或目录层级的根。虽然 `<Directory>` 容器指向本地文件系统内部，但 `<Location>` 指向本地文件系统外部。`URI` 可以包含通配符；`a*` 不匹配 `a`。

以下 `<Location>` 容器限制来自 `example.net` 域的客户端对 `http://server/pop` 的访问，其中 `server` 是服务器的 `FQDN`：

```
<Location /pop>
Order deny,allow
deny from all
</Location>
```

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## 注意：使用 `<LimitExcept>` 代替 `<Limit>`

使用 `<LimitExcept>` 容器代替 `<Limit>` 容器更安全，因为前者可以防止任意方法。当你使用 `<Limit>` 时，必须小心地显式命名该组指令可能影响的所有可能方法。

上下文：`server config`、`virtual host`、`directory`、`.htaccess`

## `<Location>`

将指令应用于指定的 `URI`。

```
<Location URI> ... </Location>
```

其中 `URI` 指向内容，并指定容器中指令应用的文件或目录层级的根。虽然 `<Directory>` 容器指向本地文件系统内部，但 `<Location>` 指向本地文件系统外部。`URI` 可以包含通配符；`a*` 不匹配 `a`。

以下 `<Location>` 容器限制来自 `example.net` 域的客户端对 `http://server/pop` 的访问，其中 `server` 是服务器的 `FQDN`：

```
<Location /pop>
Order deny,allow
deny from all
</Location>
```

# 提示：查询可能会消耗大量系统资源

请谨慎使用 `On` 和 `DNS`：它们在繁忙的系统上可能会消耗大量资源。你可以使用诸如 `resolve` 的程序进行离线反向域名解析，以用于统计目的。

如果你离线执行主机名解析，可能会面临名称可能已经更改的风险；你通常希望获得请求当时的名称。为了尽量地减少这个问题，请在写入日志后尽快进行主机名解析。

# `Timeout`

指定 `Apache` 等待网络操作完成的时间。

```
Timeout num
```

其中 `num` 是 `Apache` 等待网络操作完成的秒数。你通常可以将此指令设置为较低的值；对于繁忙的服务器来说，等待五分钟是一个很长的时间了。`Apache` 文档说，默认值不更低是因为“因为代码中可能存在某些特殊情况，在发送数据包时计时器不会重置”。

上下文：`server config`

默认值: `300`

`Red Hat`: `120`

# `UseCanonicalName`

指定服务器用于识别自身身份的方法。

```
UseCanonicalName On | Off | DNS
```

`On`: `Apache` 使用 `ServerName` 指令（第 796 页）的值作为其身份。

`Off`: `Apache` 使用传入请求中的名称和端口作为其身份。

`DNS`: `Apache` 对传入请求的 `IP` 地址进行 `DNS` 反向域名解析（第 729 页），并使用结果作为其身份。很少使用。

当服务器有多个名称且需要执行重定向时，此指令非常重要。`Red Hat` 将此指令设置为 `Off`，因为 `ServerName` 指令（第 796 页）被注释掉了。一旦设置了 `ServerName`，请将 `UseCanonicalName` 改为 `On`。关于重定向和此指令的讨论请参见第 817 页。

上下文：`server config`, `virtual host`, `directory`

默认值: `RHEL On`, `FEDORA Off`

`Red Hat`: `RHEL Off`, `FEDORA On`

# 日志指令

# `ErrorLog`

指定 `Apache` 向何处发送错误消息

```
ErrorLog filename | syslog[facility of the file]
```

其中 `filename` 指定相对于 `ServerRoot`（第 609 页）的文件名，`Apache` 将错误消息发送到该文件；`syslog` 指定 `Apache` 发到 `syslog`（第 562 页），`facility` 指定使用哪种 `syslog` 设施。默认设施为 `local7`。

上下文：`logs/error_log`, `virtual host`

默认值: `logs/error_log`

`Red Hat`: `logs/error_log`

# `LogLevel`

指定 `Apache` 记录的错误消息级别

```
LogLevel level
```

其中 `level` 指定 `Apache` 记录该级别及更高（更紧急）的错误。从下列表中选择 `level`，此列表按紧急程度递减和详细程度增加的顺序排列。

- `emerg`: 系统不可用消息
- `alert`: 需要立即采取行动的消息
- `crit`: 严重状态消息
- `error`: 错误状态消息
- `warn`: 非致命警告消息
- `notice`: 正常的重要消息
- `info`: 运行状态消息和建议
- `debug`: 用于查找和解决问题的消息

上下文：`server config`, `virtual host`

默认值: `warn`

`Red Hat`: `warn`

# 控制内容的指令

# `AddHandler`

在文件名扩展名与 `Apache` 内置处理器之间建立映射。

```
AddHandler handler extension [extension] ...
```

其中 `handler` 是内置处理器的名称，`extension` 是映射到该处理器的文件名扩展名。处理器是内置在 `Apache` 中的操作，并与加载的模块直接相关。当客户端请求具有指定文件名扩展名的文件时，`Apache` 会使用处理器。

例如，以下 `AddHandler` 指令导致 `Apache` 使用 `cgi-script` 处理器处理文件名扩展名为 `.cgi` 的文件：

```
AddHandler cgi-script .cgi
```

上下文：`server config`, `virtual host`, `directory`, `.htaccess`

默认值: `none`

`Red Hat`: `type-map var`

# `Alias`

将 `URI` 映射到目录或文件。

```
Alias pathname
```

其中 `alias` 匹配客户端请求调用的 `URI` 部分，而 `pathname` 是别名的绝对路径名，通常是一个目录。

例如，以下别名会导致 `Apache` 在客户端请求 `http://www.example.com/pix/milk.jpg` 时提供 `/usr/local/pix/milk.jpg` 服务：

```
Alias /pix /usr/local/pix
```

在某些情况下，你需要使用 `<Directory>` 容器（799）来授予对别名内容的访问权限。

上下文：`server config`, `virtual host`

默认值: `None`

`Red Hat` 提供两个别名，一个用于 `/icons/`，另一个用于 `/error/`

# `ErrorDocument`

指定发生特定错误时执行的 `Apache` 操作。

```
ErrorDocument code action
```

其中 `code` 是错误代码（826），此指令为其定义了响应，而 `action` 是以下内容之一：

- `string`: 定义 `Apache` 返回给客户端的消息。
- `absolute pathname`: 指向 `Apache` 重定向到客户端的本地脚本或其他内容。
- `URI`: 指向 `Apache` 重定向到客户端的外部脚本或其他内容。

当你未为特定错误指定此指令时，当该错误发生，`Apache` 会返回硬编码的错误消息。参见 816 以解释 `ErrorDocument` 指令在系统首次安装时如何返回 `Red Hat` 测试页。

`ErrorDocument` 指令的一些示例：

- `ErrorDocument 403 "Sorry, access is forbidden."`
- `ErrorDocument 403 /cgi-bin/uh-ph.pl`
- `ErrorDocument 403 http://errors.example.com/not_allowed`

上下文：`server config`, `virtual host`, `directory`

默认值: `none`

`Red Hat`: `index.html`; 参见第 816 页的“`Red Hat` 测试页”

# `IndexOptions`

指定 `Apache` 如何显示目录列表。

```
IndexOptions [*|option] ...
```

其中 `option` 可以是这些选项的任何组合。使用 `*` 代替 `n` 以适应最宽的情况。

- `DescriptionWidth=n`: 设置描述列宽为 `n` 个字符。
- `FancyIndexing`: 在目录列表中显示链接的列头。
- `FoldersFirst`: 排序使目录位于文件之前。
- `HTMLTable`: 以表格形式目录列表。
- `IconsAreLinks`: 使图标可点击。
- `IconHeight=n`: 设置图标高度为 `n` 像素。
- `IgnoreCase`: 排序名称时忽略大小写。
- `IconClient`: 忽略客户端提供的路径。
- `NameWidth=n`: 设置文件名列宽为 `n` 个字符。
- `ScanHTMLSorting`: 从 `HTML` 文档中提取并解析字段。由于消耗 `CPU` 和磁盘而不使用。
- `SuppressColumn`: 隐藏用于排序列的列头。
- `SuppressDescription`: 隐藏文件描述。
- `SuppressHTMLreamble`: 隐藏 `HeaderName` 指令指定的文件，即使该文件存在。
- `Suppression`: 隐藏图标。
- `SuppressLastModified`: 隐藏修改日期。
- `SuppressRules`: 隐藏水平线。
- `SuppressSize`: 隐藏文件大小。
- `VersionSort`: 自然地对版本号（文件名）进行排序；字符字符串不受影响，数字子串除外。

当此指令在目录中出现多次时，`Apache` 会合并来自目录的选项。使用 `+` 合并高级目录的选项。（除非使用 `+` 或配合所有选项，否则 `Apache` 会丢弃任何合并高级目录选项的设置。）例如，以下目录将 `/custup/download` 的选项设置为 `VersionSort`；`Apache` 会丢弃下载目录中的 `FancyIndexing` 和 `IgnoreCase`。

```
<Directory /custup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custup/download>
    IndexOptions VersionSort
</Directory>
```

由于 `*` 出现在 `VersionSort` 之前，后续的指令和继续设置将 `/custup/download` 的选项配置为 `FancyIndexing`、`IgnoreCase` 和 `VersionSort`：

```
<Directory /custup>
    IndexOptions FancyIndexing
    IndexOptions IgnoreCase
</Directory>

<Directory /custup/download>
    IndexOptions +VersionSort
</Directory>
```

上下文：`server config`, `virtual host`, `directory`, `.htaccess`

默认：无；仅列出文件名
