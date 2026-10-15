
那么每当表单提交时，将按常规调用 `/cgi-bin/form_processor.pl` 脚本。在默认操作脚本中执行什么操作取决于你。在 Internet 服务提供商的配置中，我建议让默认脚本打印有意义的消息，以便 HTML 表单开发人员能够意识到自己哪里做错了。

对于 GET 请求，只有当请求附带查询数据时才会使用默认操作。例如，`www.your_site.com/somefile.html` 将按常规处理，但如果收到类似 `http://www.your_site.com/somefile.html?some=data` 的请求，则 GET 的默认操作将被执行。

## `mod_ext_filter`

`mod_ext_filter` 模块使 Apache 能够使用外部程序作为输入和输出过滤器。任何能从 `STDIN` 读取输入并写入 `STDOUT` 输出的程序都可以使用。当然，为每个请求运行外部程序来处理输入或输出是一个耗时任务，在生产环境中应避免这样做。过滤器最好使用 Apache API（应用程序编程接口）开发，并在 Apache 服务器进程内运行。

### `ExtFilterDefine`

`ExtFilterDefine` 指令允许你定义一个过滤器，该过滤器随后可以通过此指令中指定的过滤器名称来使用。

**语法：** `ExtFilterDefine filter_name [mode=input | output] [intype=MIME-type] [outtype=MIME-type] [PreservesContentLength]`

**上下文：** `服务器配置`

在下面的示例中，定义了一个名为 `gzfilter` 的过滤器，它是一个输出过滤器（`mode=output`），当被调用时运行 `/usr/bin/gzip` 程序：

```apache
ExtFilterDefine gzfilter mode=output cmd=/usr/bin/gzip
```

这里，`mode` 只能设置为 `output`。`intype` 和 `outtype` 设置用于定义输入和输出使用的 MIME 类型。例如，如果一个过滤器接收 `intype=text/plain` 和 `outtype=text/html`，则该过滤器负责将数据从纯文本格式转换为 HTML 格式。当过滤器不改变数据的字节大小时，应使用 `PreservesContentLength` 参数。

假设你有一个名为 `/usr/local/bin/program` 的自定义过滤器程序，并希望将其用作名为 `/www/mysite/htdocs/mytxts` 的 Web 目录中所有纯文本文件的输出过滤器。以下是一个示例配置，允许你实现这一点：

```apache
ExtFilterDefine my_test_filter \
mode=output cmd=/usr/local/bin/program \
intype=text/plain \
outtype=text/html

<Directory "/www/mysite/htdocs/mytxts">
    SetOutputFilter my_test_filter
    AddType text/html
</Directory>
```

这里 `ExtFilterDefine` 定义了一个名为 `my_test_filter` 的过滤器，当被调用时运行 `/usr/local/bin/program`，它从 `STDIN` 接收 `text/plain` 数据，并将 `text/html` 数据写入 `STDOUT`。现在 `<Directory>` 容器将此过滤器设置为该目录的输出过滤器，并使用 `AddType` 指令告知 Apache 输出 MIME 类型是 `text/html`。如果你在此目录中存储文本文件，并且 Web 客户端请求它们，这些文件将通过 `/usr/local/bin/program` 转换为 HTML。

### `ExtFilterOptions`

`ExtFilterOptions` 指令为模块设置调试选项。当需要设置调试时，使用 `DebugLevel` 选项。将此选项设置为 `0` 会禁用调试，这是默认行为。将其设置为 `1` 会启用显示选项的调试日志条目。将其设置为 `9` 会启用过滤器处理的所有详细细节。

**语法：** `ExtFilterOptions DebugLevel=n LogDebugr | NoLogStderr`

**上下文：** `服务器`

## `Content-Type` 配置模块

本节中介绍的模块（见表 5-5）使你能够配置、检测和协商适合服务请求的内容类型。

| 模块 | 用途 |
| :--- | :--- |
| `mod_mime` | 允许 Apache 通过文件扩展名确定 MIME 类型。 |
| `mod_mime_magic` | 允许 Apache 通过魔数（字节模式）确定 MIME 类型。 |
| `mod_negotiation` | 允许 Apache 执行内容协商，以发送客户端可接受的最佳类型内容。 |

## `mod_mime`

`mod_mime` 模块在 Apache 中默认编译。它为客户端提供关于文档的元信息。它还允许你为文档定义一个处理器，以确定 Apache 如何处理该文档。

### `AddCharset`

`AddCharset` 指令将一个或多个文件扩展名映射到 MIME 字符集。这允许你将一个字符集关联到一个或多个文件扩展名。

**语法：** `AddCharset charset file_extension [file_extension ...]`

**上下文：** `服务器配置`、`虚拟主机`、`目录`、`逐目录配置 (.htaccess)`

**覆盖：** `FileInfo`

以下示例将使名为 `filename.utf8` 的文件映射为名为 `UTF-8` 的字符集。

```apache
AddCharset UTF-8 .utf8
```

### `AddEncoding`

`AddEncoding` 指令将一个或多个文件扩展名映射到 MIME `编码` 方案。换句话说，此指令将一个编码方案关联到一个或多个文件扩展名。

- **语法：** `AddEncoding MIME file_extension [file_extension...]`
- **上下文：** `服务器配置`、`虚拟主机`、`目录`、`逐目录配置 (.htaccess)`
- **覆盖：** `FileInfo`

例如，以下指令将使名为 `backup.gz` 的文件映射为 `x-gzip` 编码文件，而名为 `tarball.tar` 的文件映射为 `x-tar` 编码文件。

```apache
AddEncoding x-gzip gz

AddEncoding x-tar tar
```

### `AddHandler`

`AddHandler` 指令为一个或多个文件扩展名定义处理器。每当 Apache 遇到具有已定义处理器的文件时，它允许该处理器处理文件。

- **语法：** `AddHandler handler-name file-extension [file-extension ...]`
- **上下文：** `服务器配置`、`虚拟主机`、`目录`、`逐目录访问控制文件 (.htaccess)`

在以下示例中：该指令指定所有 `.cgi` 文件由名为 `cgi-script` 的处理器处理。

```apache
AddHandler cgi-script .cgi
```

### `AddLanguage`

`AddLanguage` 指令将文件扩展名列表映射到 MIME 语言。当 Apache 遇到具有此类扩展名的文件时，它知道该文件支持什么语言。

- **语法：** `AddLanguage MIME_language file_extension [file_extension] [...]`
- **上下文：** `服务器配置`、`虚拟主机`、`目录`、`单目录访问控制文件 (.htaccess)`
- **可覆盖级别：** `FileInfo`

以下示例将扩展名为 `.en` 或 `.english` 的所有文件映射为英语语言文件。这在内容协商中非常有用，服务器可以根据客户端的语言偏好返回文档。

```apache
AddLanguage en .en .english
```

或者，在下面的示例中，如果客户端偏好英语文档，并且 `document.fr.html` 和 `document.en.html` 都可用，服务器应返回 `document.en.html`。

```apache
AddLanguage en .en

AddLanguage fr .fr
```
