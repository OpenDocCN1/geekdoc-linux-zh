
如果目录中既没有 `index.html` 也没有 `index.txt`，则会导致执行 CGI 脚本 `/cgi-bin/index.pl`。

# 第 4 章：设置 Web 服务器

## FancyIndexing

- **语法：** `FancyIndexing` `boolean`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`
- **状态：** 基础

`FancyIndexing` 指令为目录设置 FancyIndexing 选项。布尔值可以是 `on` 或 `off`。应优先使用 `IndexOptions` 指令。

## HeaderName

- **语法：** `HeaderName` `filename`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`
- **状态：** 基础

`HeaderName` 指令设置将插入在索引列表顶部的文件名。`filename` 是要包含的文件名，被认为是相对于被索引目录的。服务器首先尝试将 `filename.html` 作为 HTML 文档包含；否则，它将 `filename` 作为纯文本包含。例如：

```
HeaderName HEADER
```

在对目录 `/web` 建立索引时，服务器将首先查找 HTML 文件 `/web/HEADER.html` 如果找到则包含；否则，如果存在，将包含纯文本文件 `/web/HEADER`。

## IndexIgnore

- **语法：** `IndexIgnore` `file` ...
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`
- **状态：** 基础

`IndexIgnore` 指令将文件添加到列出目录时要隐藏的文件列表中。`file` 是要忽略的文件扩展名、部分文件名、通配符表达式或完整文件名。多个 `IndexIgnore` 指令会添加到列表中，而不是替换已忽略的文件列表。默认情况下，列表包含 `'.'`。例如：

```
IndexIgnore README .htaccess ~
```

## IndexOptions

- **语法：** `IndexOptions` `option` `option`...
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`
- **状态：** 基础

`IndexOptions` 指令指定目录索引的行为。`Option` 可以是以下内容之一：

- `FancyIndexing`（这开启了目录的花式索引。）
- `IconsAreLinks`（这使图标成为文件名锚点的一部分，用于花式索引。）
- `ScanHTMLTitles`（这开启了从 HTML 文档中提取标题以用于花式索引；如果文件没有通过 `AddDescription` 提供的描述，那么 `httpd` 将读取文档以获取 `TITLE` 标签的值，但请注意，这非常消耗 CPU 且是密集型操作。）
- `SuppressLastModified`（这在花式索引列表中抑制最后修改日期显示。）
- `SuppressSize`（这在花式索引列表中抑制文件大小。）
- `SuppressDescription`（这在花式索引列表中抑制文件描述。）

默认情况下没有选项。如果多个 `IndexOptions` 应用于目录，则采用最具体的一个；选项不会合并。例如：

```
<Directory /web/docs>
<IndexOptions FancyIndexing
</Directory>
<Directory /web/spec>
<IndexOptions ScanHTMLTitles
</Directory>
```

对于 `/web/spec` 目录仅设置了 `ScanHTMLTitles`。

## ReadmeName

- **语法：** `ReadmeName` `filename`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`
- **状态：** 基础

`ReadmeName` 指令设置附加到索引列表末尾的文件名。`filename` 是要包含的文件，被认为是相对于被索引目录的。服务器首先尝试将 `filename.html` 作为 HTML 文档包含；否则，它将 `filename` 作为纯文本包含。在此示例中：

`ReadmeName README`

对目录 `/web` 建立索引时，服务器将首先查找 HTML 文件 `/web/README.html` 如果找到则包含；否则，如果存在，将包含纯文本文件 `/web/README`。

## Mod_imap 模块

该模块包含在 `mod_imap.c` 文件中，并默认编译。它为 `.map` 文件提供功能，取代了 `imageap` 程序。任何配置使用 `handler` `imap-file`（使用 `AddHandler` 或 `SetHandler`）的目录或类型将由此模块处理。

以下指令激活以 `.map` 结尾的文件作为 `imageap` 文件：

```
AddHandler imap-file map
```

注意，仍然支持：

```
AddType application/x-httpd-imap map
```

`imap` 模块增加以前发布的 `imageap` 程序无法实现的新功能：

- 相对于 `Referer` 信息的 URL 引用。
- 通过新的 `map` `base` 设置默认 `<BASE>`。
- 不需要 `imageap.conf` 文件。
- 点引用。
- 可 `ap` `imageap` 生成。

此模块使得三个指令成为可能：`ImapMenu`、`ImapDefault` 和 `ImapBase`。

## ImapMenu

- **语法：** `ImapMenu` `{none, formatted, semiformatted, unformatted}`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`

`ImapMenu` 指令决定如果没有有效坐标调用 `imageap` 文件时采取的操作。它有以下选项：

- `none`（如果 `ImapMenu` 为 `none`，则不生成菜单，并执行默认操作。）
- `formatted`（格式化菜单是最简单的菜单，因为 `imageap` 文件中的注释被忽略；打印一个一级标题、一条规则，然后单独行打印链接——菜单具有一致的、朴的外观，类似于目录列表。）
- `semiformatted`（注释在 `imageap` 文件中出现的地方打印。空行转换为 HTML 换行符；不打印标题或规则；否则，菜单与格式化菜单相同。）

## ImapDefault

- **语法：** `ImapDefault` `{error, nocontent, map, referer, URL}`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`

`ImapDefault` 指令设置 `imagemap` 文件中使用的默认值。其值会被 `imagemap` 文件内部的默认指令覆盖。如果不存在，默认操作为 `nocontent`，这意味着将向客户端发送 `204 NoContent` 消息。在这种情况下，客户端应该继续显示原始页面。

## ImapBase

- **语法：** `ImapBase` `{map, referer, URL}`
- **上下文：** 服务器配置、虚拟主机、目录、`.htaccess`
- **覆盖：** `indexes`

`ImapBase` 指令设置 `imagemap` 文件中使用的默认基础路径。其值会被 `imagemap` 文件内部的 `base` 指令覆盖。如果不存在，`base` 默认为 `http://servername/`。

## Mod_include 模块

该模块包含在 `mod_include.c` 中，并默认编译。它为服务器解析的 HTML 文档（称为 SGML 文档）提供了支持。任何 MIME 类型为 `text/x-server-parsed-html` 或 `text/x-server-parsed-html` 的文档都将被此模块解析，并将输出结果作为 HTML 文档提供。

文档被作为 HTML 文档解析，其中嵌入了注释形式的命令。命令的语法如下：

```
<![element attribute=value attribute=value ...>
```
