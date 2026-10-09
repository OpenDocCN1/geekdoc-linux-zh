

## IndexOptions
表 5-7 展示了您可以与 `IndexOptions` 配合使用的选项。

| 选项 | 作用 |
|---|---|
| `FancyIndexing` | 开启目录的花式索引。注意，`FancyIndexing` 和 `IndexOptions` 指令会**相互覆盖**。 |
| `IconHeight[=pixels]` | 允许 Apache 在图标的 `IMG` 标签中包含 `HEIGHT=pixels` 属性，这使得大多数浏览器加载图标时速度更快。如果您未指定像素值，则使用标准默认值。 |
| `IconsAreLinks` | 使图标成为文件名锚点的一部分，用于花式索引。 |
| `IconWidth[=pixels]` | 允许 Apache 在图标的 `IMG` 标签中包含 `WIDTH=pixels` 属性，这使得大多数浏览器加载图标时速度更快。如果您未指定像素值，则使用标准默认值。 |
| `ScanHTMLTitles` | 如果您希望 Apache 读取 HTML 文档的标题（由 `<TITLE>` 和 `</TITLE>` 标签对标识）以进行花式索引，请使用此选项。但是，如果您已使用 `AddDescription` 指令指定了描述，则不会使用此选项。请注意，读取每个文件的内容并搜索标题信息是一个耗时任务，可能会减慢目录列表的生成速度。我不推荐此选项。 |
| `SuppressColumnSorting` | 默认情况下，Apache 会为花式目录索引创建可点击的列标题，这允许用户对该列中的信息进行排序。此选项将禁用该功能。 |
| `SuppressDescription` | 如果您不想在花式目录列表中显示文件描述，请使用此选项。 |
| `SuppressHTMLOreamble` | 如果目录确实包含由 `HeaderName` 指令指定的文件，该模块通常会在标准 HTML 前导内容（`<HTML>`、`<HEAD>` 等）之后包含该文件的内容。`SuppressHTMLOreamble` 选项会禁用此行为。 |
| `SuppressLastModified` | 抑制在花式索引列表中显示最后修改日期。 |
| `SuppressSize` | 抑制在花式索引列表中显示文件大小。 |

## IndexOrderDefault

IndexOrderDefault 指令允许您通过排序名称、日期、大小和描述等各个字段来更改目录列表视图，这些目录是使用 FancyIndexing 功能显示的。

- **语法：** IndexOrderDefault Ascending | Descending Name | Date | Size | Description
- **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
- **覆盖：** Indexes

## ReadmeName

如果您希望在花式目录列表的末尾插入一个文件，请使用 ReadmeName 指令。

- **语法：** ReadmeName filename
- **上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)
- **覆盖：** Indexes

例如，以下设置使 Apache 查找名为 readme.html（默认扩展名）或 readme 的文件并将其插入到列表末尾：

```
ReadmeName readme
```

## Response Header Modules

Apache 允许您在发送数据时发送自定义 HTTP 响应头。本节中的模块如表 5-8 所示，允许您配置各种自定义响应头。

表 5-8 响应头模块

| 模块 | 用途 |
| --- | --- |
| mod_alias | 发送包含自身 HTTP 头的文件。 |
| mod_headers | 为资源添加任意 HTTP 头。 |
| mod_expires | 为资源应用 Expires 头。 |
| mod_cern_meta | 支持 HTTP 头元文件。 |

### mod_asis

*mod_asis* 模块默认已编译。此模块允许您原样发送文档——也就是说，文档在不带 HTTP 头的情况下发送给客户端。这在不需要脚本帮助的情况下重定向客户端时非常有用。要原样发送文件，您需要确保 *httpd.conf* 文件包含如下条目：

```
AddType httpd/send-as-is .asis
```

这将 *httpd/send-as-is* MIME 类型分配给文件扩展名 *.asis*。如果您创建一个名为 *foobar.asis* 的文件并且客户端请求它，该文件将在没有 HTTP 头的情况下发送给客户端。您需要在文件中包含适当的头。例如，如果您想通过 *.asis* 文件提供重定向机制，您可以创建具有如下头的文件：

```
Status: 301 Text Message
Location: new-URL
Content-type: text/html
```

清单 5-2 展示了一个名为 *redirect.asis* 的文件，它将客户端重定向到新位置。

清单 5-2: *redirect.asis*

```
Status: 301 We have moved.
Location: http://www.our-new-site/
Content-type: text/html
<H1>Notice to Visitors</H1>
Please update your bookmark to point to <A HREF="http://www.our-new-site/ "> www.our-new-site/ </A><BR>
<BR>
Thanks.
```

当客户端请求此文件时，301 状态消息告诉客户端使用位置信息来重定向请求。您不需要添加 *Date:* 和 *Server:* 头，因为服务器会自动添加它们。但是，服务器不提供 *Last-Modified* 头。

### mod_headers

此模块默认未编译。*mod_headers* 允许您操作 HTTP 响应头，它提供了一个名为 *Header* 的指令，使您能够操作 HTTP 响应头。

语法: Header action header value

上下文: 服务器配置，虚拟主机，目录，每目录访问控制文件 (.htaccess)

覆盖: FileInfo

允许的操作如下：

| 操作 | 作用 |
|---|---|
| Set | 设置一个头。如果存在同名旧头，其值将更改为新值。 |
| Add | 添加一个头。如果一个或多个同名头已存在，这可能导致出现多个同名头。 |
| Append | 将值追加到现有头的值后面。 |
| Unset | 移除一个头。 |

例如，以下指令添加了值为 "Mohammed J. Kabir" 的 Author 头：

```
Header add Author "Mohammed J. Kabir"
```

以下行移除相同的头：

```
Header unset Author
```

## mod_expires

mod_expires 模块在 Apache 中默认未编译。它让您决定 Apache 如何处理服务器对请求的响应中的 Expires HTTP 头。Expires HTTP 头提供了一种告诉客户端请求的资源何时失效的方法。当文档被客户端缓存且需要再次请求时，这很有用。大多数智能客户端通过检查由 Expires HTTP 头提供的缓存文档的过期时间来确定请求文档的有效性。此模块允许您控制 Expires HTTP 头的设置。

### ExpiresActive

ExpiresActive 指令启用或禁用 Expires 头的生成。它并不保证会生成 Expires 头。如果条件不满足，则不会发送头。

**语法：** *ExpiresActive* On | Off

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (`.htaccess`)

**覆盖：** Indexes

### ExpiresByType

*ExpiresByType* 指令指定特定 *MIME 类型* 文档的 *Expires* HTTP 头的值。过期时间以秒为单位指定。您可以以两种方式定义时间。如果您选择使用 *Mseconds* 格式指定过期时间，则使用文件的最后修改时间作为基准时间。也就是说，*M3600* 意味着您希望文件在最后修改后一小时过期。另一方面，如果您使用 *Aseconds* 格式，则使用客户端的访问时间作为基准时间。以下是一些示例。

**语法 1：** *ExpiresByType* *MIME 类型* *Mseconds* | *Aseconds*

**语法 2：** *ExpiresByType* *MIME 类型* "*base_time* [plus] *num* *Years* | *Months* | *Weeks* | *Days* | *Hours* | *Minutes* | *Seconds*"

**上下文：** 服务器配置，虚拟主机，目录，每目录访问控制文件 (`.htaccess`)

**覆盖：** Indexes

以下操作使所有纯文本文件在客户端缓存中一小时后过期：

```
ExpiresByType text/plain A3600
```

以下操作使所有 GIF 文件在最后一次修改时间一周后过期：

```
ExpiresByType image/gif M604800
```

如果您想使用第二种语法来指定过期时间，您需要使用以下选项确定 *base_time* 的适当值：

| 值 | 含义 |
| :--- | :--- |
| Access | 客户端访问文件的时间。 |
| Now | 当前时间。这与访问时间相同。 |
| Modification | 文件最后更改的时间。 |

例如，以下指令告诉 Apache 发送头以告知浏览器 HTML 文档应在访问日期七天后过期，而 GIF 图像应在文件更改后或三小时十分后过期。

