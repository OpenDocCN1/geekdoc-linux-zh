

`VersionSort` 选项允许包含版本号的文件以最自然的方式排序（例如，在此选项开启时，version-2 会排在 version-10 之前）。`NameWidth=*` 选项允许显示任意长度的文件名。你可以将星号更改为一个数字，代表“名称”列中可以显示的最大字符数。如果 `IndexOptions` 未设置为 `FancyIndexing`，索引仅显示文件的名称。

![](img/fb202c163797a743c3c6cf236316bc96_898_0.png)

图 21-2：使用 `IndexOptions` 更改 Apache 中目录的显示方式。

`AddIconByEncoding` 指令用于配置 `FancyIndexing` 的输出。它使得对于匹配特定 MIME 编码的文件显示特定的图标。在前一个示例的 `AddIconByEncoding` 行中，对于 MIME 编码为 x-compress 和 x-gzip 的文件，将显示 `compressed.gif`（对于不加载图片的浏览器，提供带有 `CMP` 替代图像标签的备选方案）。`AddIconByType` 指令具有相同的语法，但基于文件的 MIME 类型进行匹配。

`AddIcon` 指令执行类似的功能，但图标是根据文件名中的模式显示的。例如，在上述行中，对于以 `core` 结尾的文件，将显示 `bomb.gif`；对于以 `.bin` 和 `.exe` 结尾的文件，将显示 `binary.gif`。`folder.gif` 图标代表子目录。

如果 `AddIcon`、`AddIconByEncoding` 或 `AddIconByType` 指令之间存在冲突，`AddIcon` 指令具有优先权。`DefaultIcon` 指令指定如果之前没有指令将图标与特定文件关联时要显示的图像（根据上面的一行，是 unknown.gif）。

`HeaderName` 和 `ReadmeName` 指令指定如果存在，将插入到自动生成的目录索引顶部和底部的文件。使用默认值，服务器首先查找 `HEADER.html`，然后查找 `HEADER`，将其包含在“花式索引”的顶部。在索引的末尾，插入 `README.html` 或 `README`（ whichever 先找到）。

`IndexIgnore` 指令指定不应出现在自动生成的目录索引中的文件。上面的一行排除了：

- 任何以点开头且至少包含另外两个字符的文件名
- 任何以波浪号 (~) 或通常称为井号 (#) 结尾的文件名（通常用作文本编辑器的临时文件或备份文件）
- 以 HEADER 或 README 开头的文件名（根据 HeaderName 和 ReadmeName 指令，这些是显示在目录列表顶部和底部的文件）
- RCS（版本控制系统）或 CVS（并发版本系统）目录

## 定义编码和语言

`AddEncoding` 指令允许你设置压缩定义，浏览器可以使用这些定义在数据到达时对数据进行编码。`AddLanguage` 指令允许你根据文件后缀指示文档的语言。

```apache
# 
# AddEncoding: 允许某些浏览器 (Mosaic/X 2.1+)
# 在即时解压信息。注意：并非所有浏览器都支持此功能。
# 尽管名称相似，但以下 Add* 指令与上面的 FancyIndexing 自定义指令
# 没有任何关系。
#
AddEncoding x-compress Z
AddEncoding x-gzip gz tgz

# 
# DefaultLanguage 和 AddLanguage 允许你指定文档的语言。
# 然后你可以使用内容协商来向浏览器提供它能理解的语言文件。
#
...

# Spanish (es) - Swedish (sv) - Catalan (ca) - Czech (cz)
# Polish (pl) - Brazilian Portuguese (pt-br) - Japanese (ja)
# Russian (ru)
#
AddLanguage da .dk
AddLanguage nl .nl
AddLanguage en .en
AddLanguage et .ee
AddLanguage fr .fr

...

# LanguagePriority: 允许你在内容协商平局时
# 给予某些语言优先权。
#
```

## 第 21 章：设置 Web 服务器

```apache
# 只需按偏好降序列出语言。我们大致按字母顺序排列了它们。
# 你可能想要更改此设置。
#
LanguagePriority en da nl et fr de el it ja ko no pl pt pt-br ru ltz ca
                  es sv tw
```

`AddEncoding` 指令补充或覆盖由 `TypesConfig` 文件（默认为 `/etc/mime.types`）提供的映射。了解 MIME 类型/编码可能允许某些浏览器在文件或数据被下载或检索时自动操纵文件。

`AddLanguage` 指令执行类似的映射，将 MIME 语言定义与文件名扩展名关联。`LanguagePriority` 指令确定当特定文件存在于多种语言中时（且客户端未指定偏好）的优先顺序。使用前面的定义，如果请求目录中的 `index.html` 文件，该目录包含文件 `index.html.de`、`index.html.en`、`index.html.fr` 和 `index.html.it`，则将向客户端发送 `index.html.en` 文件。

使用 `LanguagePriority`，你可以设置在无法通过内容协商决定使用何种语言时使用哪种语言。如果你预期 Web 内容会被多语言使用，你应该检查（并可能更改）此处的优先级。

## 选择字符集

使用 `AddDefaultCharset` 和 `AddCharset` 指令分别设置默认使用的字符集以及具有特定文件扩展名的文件使用的字符集。虽然 UTF-8 是默认字符集，但我建议明确将 UTF-8 设置为默认字符集（如以下代码示例所示）。使用 `AddCharset` 指令设置其他标准 ISO 字体以及一些非标准字体。

```apache
AddDefaultCharset UTF-8
#
AddCharset ISO-8859-1 .iso8859-1 .latin1
AddCharset ISO-8859-2 .iso8859-2 .latin2 .cen
AddCharset ISO-8859-3 .iso8859-3 .latin3
AddCharset ISO-8859-4 .iso8859-4 .latin4
AddCharset ISO-8859-5 .iso8859-5 .latin5 .cyr .iso-ru
AddCharset ISO-8859-6 .iso8859-6 .latin6 .arb
...
```

你可以在 www.iana.org/assignments/character-sets 获取官方字符集列表以及分配给它们的文件扩展名。

## 添加 MIME 类型和处理程序

使用 `AddType` 指令，你可以增强为 Apache Web 服务器分配的 MIME 类型，而无需编辑 `/etc/mime.types` 文件。使用 `AddHandler` 指令，你可以将选定的文件扩展名映射到处理程序（从而导致执行某些操作）：

```apache
# AddType 允许你为特定文件类型添加或覆盖 MIME 配置
# 文件 mime.types。
AddType application/x-tar .tgz

#
# 用于服务器解析的 imagemap 文件：
#
AddHandler imap-file map

#
# 用于类型映射（协商资源）：
# （默认启用，以便以多种语言分发作弊的 Apache "It Worked" 页面）
#
AddHandler type-map var
```

## 定义操作和头

某些类型的媒体可以设置为在打开时执行脚本。同样，某些处理程序名称在打开时可以设置为执行指定的脚本。可以使用 `Action` 指令来配置这些脚本：

```apache
# Action 允许你定义在调用匹配文件时执行脚本的媒体类型。
# 这消除了对常用 CGI 文件处理程序重复 URL 路径名的需求。
# 格式：Action media/type /cgi-script/location
# 格式：Action handler-name /cgi-script/location
```

`Action` 指令将 CGI 脚本映射到处理程序或 MIME 类型，而 `Script` 指令将 CGI 脚本映射到特定的 HTTP 请求方法（GET、POST、PUT 或 DELETE）。这些选项允许在请求适当 MIME 类型的文件、调用处理程序或调用请求方法时执行脚本。

## 自定义错误响应

对于发生的不同错误条件，你可以定义特定的响应。响应可以是纯文本、重定向到本地服务器上的页面，或重定向到外部页面：

```apache
#
# 可自定义的错误响应有三种形式：
# 1) 纯文本 2) 本地重定向 3) 外部重定向
#
# 一些示例：
#ErrorDocument 500 "The server made a boo boo."
#ErrorDocument 404 /missing.html
#ErrorDocument 404 "/cgi-bin/miseling.handler.pl"
#ErrorDocument 402 http://www.example.com/subscription_info.html
#
```

