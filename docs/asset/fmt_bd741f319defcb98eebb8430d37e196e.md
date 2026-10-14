
值通常包含在引号中；许多命令允许单个属性-值对。允许的元素如下：

- `config`（此命令控制解析的各个方面；有效属性为 `errmsg` 用于错误消息，`sizefmt` 用于设置文件大小，以及 `timefmt`，它是 `strftime` 库在打印日期时使用的字符串。）
- `echo`（此命令打印包含的变量之一；`var` 是要打印的名称。）
- `exec`（此命令执行指定的 shell 命令或 CGI 脚本。`option` 选项将完全禁用此命令，有效属性为 `cgi` 用于 CGI 脚本，`cmd` 用于服务器命令。）
- `fsize`（此命令打印指定文件的大小，取决于 `sizefmt` 规范。它具有以下潜在属性：`file` 用于相对路径，`virtual` 用于 URL。）
- `fastmod`（此命令打印指定文件的最后修改日期，取决于 `timefmt` 规范，具有与 `fsize` 命令相同的属性。）
- `include`（此命令将另一个文档或文件的文本插入到解析后的文件中。任何被包含的文件都遵循通常的访问控制，如果包含解析文件的目录设置了 `IncludesEXEC` 且包含该文档会导致程序执行，则将不会被包含，以防止 cgi 脚本的执行。）

属性定义文档的位置；包含操作针对每个 `include` 命令执行。有效属性是 `file`（其值为相对于正在解析的当前文档所在目录的路径）和 `virtual`（相对于当前文档的 URL）。

## 第 4 章：设置 Web 服务器 287

对于 `echo` 命令以及文档调用的任何程序，有很多变量：

- `DATE_GMT`（格林尼治时间的当前日期）
- `DATE_LOCAL`（当前时区的当前日期）
- `DOCUMENT_NAME`（用户请求文档的文件名，不包含目录）
- `DOCUMENT_URL`（用户请求文档的解码 URL 路径；对于嵌套文件，这是当前文档的 URL）
- `LAST_MODIFIED`（用户请求文档的最后修改日期）

该模块提供了一个指令：`XBitHack`

### XBitHack

| 语法 | XBitHack 状态 |
| :--- | :--- |
| 默认 | XBitHack off |
| 上下文 | 服务器配置, 虚拟主机, 目录, .htaccess |
| 覆盖 | options |
| Status | base |

`XBitHack` 指令控制普通 HTML 文档的解析。Status 有以下值：

- off（对可执行文件没有特殊处理。）
- on（任何设置了用户执行位的文件将被视为服务器解析的 HTML 文档。）
- full（与 on 类似，但还会测试组执行位。如果设置了，则返回的文件的最后修改日期将为文件的最后修改时间；如果没有设置，则不发送最后修改日期。设置此允许客户端和代理缓存请求的结果。）

### Mod_log_common 模块

该模块包含在 `mod_log_common.c` 文件中并默认编译。它提供了使用常用日志格式（Common Log Format）对发送服务器的请求进行记录。

日志文件每个请求单独占一行。一行由多个用空格分隔的标记组成：

```
host ident autuser date status bytes
```

如果某个标记没有值，则用连字符 (`-`) 表示。这些标记的含义和值如下：

- host: 客户端的完全限定域名，如果名称不可用则为其 IP 地址。
- ident: 如果启用了 IdentityCheck 且客户端机器运行 ident，则这是客户端报告的身份信息。
- autuser: 如果请求的是受密码保护的文档，则请求中使用的用户。
- date: 请求的日期和时间，格式如下：

```
date = [day/month/year:hour:minute:second zone]

day = 2*digit

month = 3*letter

year = 4*digit

hour = 2*digit

minute = 2*digit

second = 2*digit

zone = ('+' | '~') 4*digit
```

该模块提供了一个指令：`TransferLog`。

## 第 4 章：设置 Web 服务器 289

### TransferLog

语法: `TransferLog file-pipe`
默认: `TransferLog logs/transfer_log`
上下文: 服务器配置, 虚拟主机
状态: base

`TransferLog` 指令设置服务器记录传入请求的文件名。`file-pipe` 可以是一个文件名（相对于 `ServerRoot`），或后跟着命令（以便在标准输入接收日志信息）。如果使用了程序，它将在 VirtualHost 下启动。

### Mod_mime 模块

该模块包含在 `mod_mime.c` 中并默认编译。它提供了根据文件名确定 MIME 类型的功能。

该模块用于确定文档的 MIME 类型。某些 MIME 类型表示服务器需要执行的特殊处理；否则将类型返回给客户端。

文档的文件名被视为由基准和后续某些扩展名组成，顺序如下：

```
base.type.language.enc
```

`type` 扩展设置文档的类型；类型由 `TypesConfig` 和 `AddType` 定义。`language` 扩展设置文档的语言，由 `AddLanguage` 定义。最后，`enc` 指令设置文档的编码，由 `AddEncoding` 定义。

支持的指令有 `AddEncoding`, `AddHandler`, `AddLanguage`, `AddType`, `ForceType`, `SetHandler` 和 `TypesConfig`。

## 第 4 章：设置 Web 服务器

### AddEncoding

语法: `AddEncoding mime-enc extension...`
上下文: 服务器配置, 虚拟主机, 目录, .htaccess
覆盖: FileInfo
状态: base

`AddEncoding` 指令向文件名扩展名列表添加内容。`MIME-enc` 是以 `extension` 结尾的文档使用的 MIME 编码。例如，

```
AddEncoding x-gzip gz

AddEncoding x-compress Z
```

这将导致 `.gz` 结尾的文件标记为使用 `x-gzip` 编码，`.Z` 文件标记为使用 `x-compress` 编码。

### AddHandler

语法: `<AddHandler handler-name extension>`
上下文: 服务器配置, 虚拟主机, 目录, .htaccess
状态: base

`AddHandler` 将扩展名 `extension` 映射到处理器 `handler-name`。例如，为了激活扩展名为 `.cgi` 的 CGI 脚本，可以使用

```
AddHandler cgi-script cgi
```

一旦将其放入 `srm.conf` 或 `httpd.conf` 文件，任何以 `.cgi` 结尾的文件都将被视为 CGI 程序。

# 第 4 章：设置 Web 服务器 291

`AddLanguage` 指令将指定的内容语言添加到文件名扩展名列表中，这些扩展名以该语言结尾。`Mime-lang` 是在移除任何内容编码扩展名后，以扩展名结尾的文件的 MIME 语言。例如：

```
AddEncoding x-compress Z

AddLanguage en .en

AddLanguage fr .fr
```

文档 `xxxx.en.Z` 将被视为一个压缩的英文文档。尽管向客户端报告了内容语言，但浏览器不太可能使用此信息。`AddLanguage` 指令在内容协商中更有用，此时服务器会根据客户端的语言偏好从多个文档中返回一个。

- `AddType`
  语法：`AddType mime-type extension...`
  上下文：服务器配置、虚拟主机、目录、.htaccess
  覆盖：FileInfo
  状态：base

`AddType` 指令将指定的内容类型添加到文件名扩展名列表中，这些扩展名以该内容类型结尾。`Mime-type` 是在移除内容编码和语言扩展名后，对于以扩展名结尾的文件，应使用的 MIME 类型。例如：

```
AddType image/gif GIF
```

建议使用 `AddType` 指令添加新的 MIME 类型，而不是更改 `TypesConfig` 文件。
与 NCSA httpd 不同，此指令无法设置特定文件的类型。

- `ForceType`
  语法：`<ForceType media type>`
  上下文：目录、.htaccess
  状态：base

## 第 4 章：设置 Web 服务器

当放置在 `.htaccess` 文件或 `<Directory>` 或 `<Location>` 节中时，此指令强制所有匹配的文件作为由 `media type` 给出的内容类型提供服务。例如，如果你有一个 GIF 文件的目录，但不想将它们都标记为 `.gif`，你可能想使用：

```
ForceType image/gif
```
