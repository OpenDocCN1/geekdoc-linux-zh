
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

### 选择字符集

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

你可以在 `www.iana.org/assignments/character-sets` 获取官方字符集列表以及分配给它们的文件扩展名。

### 添加 MIME 类型和处理程序

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

### 定义操作和头

某些类型的媒体可以设置为在打开时执行脚本。同样，某些处理程序名称在打开时可以设置为执行指定的脚本。可以使用 `Action` 指令来配置这些脚本：

```apache
# Action 允许你定义在调用匹配文件时执行脚本的媒体类型。
# 这消除了对常用 CGI 文件处理程序重复 URL 路径名的需求。
# 格式：Action media/type /cgi-script/location
# 格式：Action handler-name /cgi-script/location
```

`Action` 指令将 CGI 脚本映射到处理程序或 MIME 类型，而 `Script` 指令将 CGI 脚本映射到特定的 HTTP 请求方法（GET、POST、PUT 或 DELETE）。这些选项允许在请求适当 MIME 类型的文件、调用处理程序或调用请求方法时执行脚本。

### 自定义错误响应

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

正如注释所示，`ErrorDocument` 指令可以自定义任何服务器响应代码，将其重定向到外部页面、本地文件或 CGI 脚本，或者简单的文本句子。表 21-6 列出了最常见的服务器响应代码及其含义。

### 表 21-6：HTTP 响应代码

| 响应代码 | 含义 |
|---|---|
| 200 OK | 请求已成功处理。 |
| 201 Created | 使用 POST 请求方法，新文件已成功存储在服务器上。 |
| 202 Accepted | 请求已接收，目前正在处理中。 |
| 204 No Content | 请求成功，但显示给客户端的当前页面没有变化。 |
| 301 Moved Permanently | 请求的页面已永久移动，后续对该页面的引用应使用显示出的新 URL。 |
| 302 Moved Temporarily | 请求的页面已临时迁移。后续引用应继续使用相同的 URL，但当前连接正在被重定向。 |
| 304 Not Modified | 页面的缓存版本与请求的页面相同。 |
| 400 Bad Request | 客户端的请求包含无效语法。 |
| 401 Unauthorized | 客户端指定了无效的用户名/密码组合。 |
| 402 Payment Required | 客户端必须提供完成货币交易的手段。 |
| 403 Forbidden | 访问控制机制拒绝了客户端的请求。 |
| 404 Not Found | 请求的页面在服务器上不存在。 |
| 500 Internal Server Error | 通常在运行 CGI 程序时遇到，此响应代码表示程序或脚本包含无效代码，或者接收了无法处理的输入。 |
| 501 Not Implemented | 请求方法（例如，GET、POST、PUT、DELETE、HEAD）不被服务器理解。 |
| 502 Bad Gateway | 当 Web 服务器充当代理服务器时，在尝试满足对外部主机的请求时遇到了错误。 |
| 503 Service Unavailable | 服务器当前正在处理过多的请求。 |
| 505 HTTP Version Not Supported | 请求版本（例如，HTTP/1.0、HTTP/1.1）不被服务器理解。 |

为了使错误消息更容易国际化并标准化这些消息的呈现方式，最新版本的 Apache 包含了所谓的变体页面（以 `.var` 后缀结尾）。这些提供基于语言的变量输出的变体页面存储在 `/var/www/error` 目录中。
