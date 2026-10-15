
- `MaxClients`: 设置同时连接服务器的客户端数量。默认值为 150。`MaxClients` 的值不能超过 256。
- `LoadModule` `modules/module.so`: 加载作为动态共享对象 (DSO) 构建的模块。您必须指定模块名称和模块的对象文件。由于加载模块的顺序很重要，您应该保持这些指令在默认配置文件中的顺序不变。注意，`mod_ssl` 模块提供了使用安全套接层 (SSL) 协议进行加密的支持。

## 第 14 章：Web 服务器

## 资源配置指令

资源配置指令指定了 Web 页面的位置，以及如何指定各种文件的数据类型。要开始使用，你可以让这些指令保持默认设置。以下是 Apache 服务器的一些资源配置指令：

- `DocumentRoot` `pathname`: 指定 HTTP 服务器提供 Web 页面的目录。在 Fedora Linux 中，默认的 `DocumentRoot` 是 `/var/www/html`。如果你将 HTML 文档放在另一个目录中，请将 `DocumentRoot` 设置为该目录。
- `UserDir` `dirname`: 指定用户主目录下的一个目录，当 URL 中出现用户名时，HTTP 服务器会在该目录下查找 Web 页面（例如在 URL 如 `http://www.psn/~naval/` 中，其中包含一个带有 t 前缀的用户名）。默认的 `UserDir` 是 `public_html`，这意味着你的 Web 页面位于主目录下的 `public_html` 子目录中。如果你不想允许用户拥有 Web 页面，`UserDir` 默认是禁用的，因为 Apache 建议在 `httpd.conf` 中添加以下内容：
- `DirectoryIndex` `filename2 ...`: 指定当客户端未指定文档时，服务器返回的默认文件或文件。默认的 `DirectoryIndex` 是 `index.html`。如果 `httpd` 找不到此文件，它将返回目录的索引（通常是一个美观的文件列表）。
- `AccessFileName`: 指定可能出现在包含文档的每个目录中的文件名，并指示该文件具有访问该目录内容的权限。默认的 `AccessFileName` 是 `.htaccess`。该文件的语法与 Apache 访问控制指令相似，接下来的章节将详细介绍。
- `AddType` `subtype` `extension`: 将文件扩展名与 `type/subtype` 格式的 MIME（多用途互联网邮件扩展）数据类型关联起来，例如 `text/plain` 或 `image/gif`。要让服务器将 `.lst` 结尾的文件视为纯文本文件，请指定以下：
  `AddType text/plain .lst`
- `AddEncoding` `extension`: 将编码类型与文件扩展名关联。要让服务器将以 `.gz` 或 `.tgz` 结尾的文件标记为 `x-gzip` 编码方法，请指定以下：
  `AddEncoding x-gzip .gz .tgz`
- `DefaultType` `type/subtype`: 指定当服务器无法从文件扩展名确定类型时应该使用的 MIME 类型。如果你没有指定 `DefaultType`，`http` 假设 MIME 类型为 `text/html`。在从随附 DVD-光盘获取的默认 `httpd.conf` 文件中，`DefaultType` 指定为 `text/plain`。
- `Redirect` `requested-file-actual-URL`: 指定任何对 `requested-file` 的请求都重定向到实际 URL。

## 第三部分：网络化 Linux

- `Alias` `requested-dir` `actual-dir`: 指定服务器使用 `actual-dir` 来定位 `requested-dir` 目录中的文件。换句话说，`requested-dir` 是 `actual-dir` 的别名。要让对 `/icons` 目录的请求指向 `/var/www/icons/:var/www/icons/`，请指定以下：
- `ScriptAlias` `requested-dir` `actual-dir`: 指定用于通用网关接口 (CGI) 脚本目录的真实名称。例如，以下指令指定了 `/cgi-bin/` 目录的位置：
  `ScriptAlias /cgi-bin/ /var/www/cgi-bin/`
  该指令意味着当 Web 浏览器请求脚本（如 `/cgi/test-cgi`）时，HTTP 服务器运行脚本 `/var/www/cgi-bin/test-cgi`。
- `DefaultIcon`: 指定服务器为无信息文件使用的默认图标的位置。默认情况下，`DefaultIcon` 是 `/icons/unknown.gif`。
- `ReadMeName`: 指定 README 文件的名称，其内容会被添加到自动生成的目录列表索引中。默认的 `ReadMeName` 是 `README`。
- `HeaderName`: 指定头文件的名称，其内容会被插入到自动生成的目录列表的顶部。默认的 `HeaderName` 是 `HEADER`。
- `Description` `"file description"`: 指定在目录列表中指定的文件名旁边显示文件描述字符串。你可以使用通配符（如 `*.html`）作为文件名。例如，以下指令将带有 `.tgz` 扩展的文件描述为 GZIP 压缩归包：
  `AddDescription "GZIP compressed archive" .tgz`
- `AddIcon` `iconfile1` `extension2...`: 将一个图标与一个或多个文件扩展名关联。以下指令将图标文件 `/icons/text.gif` 与文件扩展名 `.txt` 关联：
  `AddIcon /icons/text.gif .txt`
- `AddIconType` `iconfile` `MIME-types`: 将图标与由 MIME 类型通配符指定的组类型组（如 `/*` 或 `image/*`）关联。要将 `/icons/text.gif` 图标与所有类型关联，请指定以下：
  `AddIconType (TXT,/icons/text.gif) */*`
  该指令还允许服务器为无法接受图片的客户端使用 TXT 代替图标。浏览器会告诉服务器它们接受什么类型的数据。
- `AddByEncoding` `filename` `encoding1` `encoding2...`: 为一个或多个编码类型（如 `x-compress` 或 `x-gzip`）指定显示的图标。
- `Indexignore` `filename1filename2...`: 指示服务器忽略指定的文件（包含通配符）。要排除 `README`、`HEADER` 以及所有以点（`.`）、末尾波浪（`~`）或末尾井号（`#`）开头的文件，请指定以下：
  `Indexignore ??* ~ *# README RCS CVS *,t`
- `IndexOptions` `option1option2...`: 指定你希望在服务器准备的目录列表中使用的选项。
- `FancyIndexing`: 启用目录列表。
- `IconHeight-N`: 指定高度。
- `IconWidth-N`: 指定宽度。
- `NameAre`: 指定文件名。
- `ScanHTML`: 指定类型。
- `SuppressHeader`: 不添加头（指令）。
- `SuppressModified`: 不显示日期。
- `SuppressSize`: 不显示大小。
- `SuppressDescription`: 不显示描述。
- `ErrorDocument` `filename`: 指定发生错误时服务器发送的文件。你也可以提供文本消息。有一些：
- 400: Bad Request
- 401: Unauthorized
- 402: Payment Required
- 403: Forbidden
- 404: Not Found
- 405: Method Not Allowed
- 406: Not Acceptable
- 407: Proxy Authentication
- 408: Request Timeout
- 409: Conflict
- 410: Gone
- 411: Length Required
- 412: Precondition Failed
- 413: Entity Too Large
- 414: Request-URI Long
- 415: Unsupported Media Type
- 416: Range Not Satisfiable
- 417: Expectation Failed
- 500: Internal Server Error
- 501: Implemented
- 502: Bad Gateway
- 503: Service Unavailable
- 504: Gateway Timeout
- 505: HTTP Version Not Supported

`TypesConfig` `filename`: 指定包含文件扩展名到 MIME 类型映射的文件（MIME 代表多用途互联网邮件扩展，定义了在单个消息封装附件的方法）。服务器向客户端报告这些 MIME 类型。如果你没有指定 `TypesConfig` 指令，`http` 的 `TypesConfig` 文件为 `/etc/mime.types`。每行列出 MIME 类型及其扩展名。以下是默认类型中的部分：

application/mail      doc
application/pdf        pdf
application/postscript ai eps ps
application/x-tl       tcl
audio/mpeg               mpga mp2 mp3
audio/x-pn-realaudio    ram rm
audio/wav               wav
image/gif               gif
image/jpeg              jpeg jpg Jpe
image/png               png
text/html              html txt
text/plain              asc txt
video/mpeg              mpeg mpe
