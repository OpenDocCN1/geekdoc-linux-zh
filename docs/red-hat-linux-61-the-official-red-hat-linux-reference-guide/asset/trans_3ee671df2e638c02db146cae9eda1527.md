

## 10.52. AccessFileName

AccessFileName 指定了服务器在每个目录下应用于访问控制信息的文件名。默认值为 `.htaccess`。

在 `AccessFileName` 指令之后，有一组 `Files` 标签将对任何以 `.ht` 开头的文件应用访问控制。出于安全考虑，这些指令会拒绝 Web 访问任何 `.htaccess` 文件（或其他以 `.ht` 开头的文件）。

## 10.533. CacheNegotiatedDocs

默认情况下，Web 服务器会请求代理服务器不要缓存任何基于内容协商的文档（即可能随时间变化，或由于请求者的输入而改变的文档）。如果将 `CacheNegotiatedDocs` 设置为 `on`，将禁用此功能并允许代理服务器缓存文档。

## 10.534. TypesConfig

TypesConfig 指定了设置默认 MIME 类型映射列表（文件扩展名到内容类型）的文件。默认的 TypesConfig 文件为 `/etc/mime.types`。相对于 `/etc/mime.types`，添加 MIME 类型映射推荐的方法是使用 `AddType` 指令。

有关 `AddType` 的信息，请参阅第 10.5.58 节 `AddType`。

## 10.535. DefaultType

DefaultType 为 Web 服务器无法确定 MIME 类型的文档设置一个默认类型。默认值为 `text/plain`。

## 10.536. IfModule

`<IfModule>` 和 `</IfModule>` 标签创建一个条件容器，只有在指定的模块加载时它才被激活。包含在 `IfModule` 标签内的指令将在两种条件之一被处理：如果起始 `<IfModule>` 标签中包含的模块已加载，则处理指令；或者，如果在模块名称之前出现感叹号 `[!`，则只有在 `<IfModule>` 标签指定的模块未加载时，才处理指令。

有关 Apache HTTP Server 模块的信息，请参阅第 10.7 节“添加模块”。

## 10.537. HostnameLookups

`HostnameLookups` 可以设置为 `on`、`off` 或 `double`。如果将 `HostnameLookups` 设置为 `on`，服务器会自动为每个连接解析 IP 地址。解析 IP 地址意味着服务器与 DNS 服务器建立一个或多个连接，这增加了处理开销。如果将 `HostnameLookups` 设置为 `double`，服务器将执行双反向 DNS 解析，产生更多的处理开销。

为了节省服务器资源，`HostnameLookups` 默认设置为 `off`。

如果服务器日志文件中需要主机名，请考虑在滚动 Web 服务器日志文件时更高效、批量地进行 DNS 查找。

## 第 10 章 Apache HTTP Server

## 10.5.38. ErrorLog

`ErrorLog` 指定记录服务器错误的文件。默认情况下，此指令设置为 `/var/log/httpd/error_log`。

## 10.5.39. LogLevel

`LogLevel` 设置错误日志中错误信息的详细程度。`LogLevel` 可以设置为（从最不详细到最详细）`emerg`、`alert`、`crit`、`error`、`warn`、`notice`、`info` 或 `debug`。默认 `LogLevel` 为 `warn`。

## 10.5.40. LogFormat

`LogFormat` 指令配置虚拟 Web 服务器日志文件的格式。实际的 `LogFormat` 取决于 `CustomLog` 指令中给出的设置（参见第 10.5.41 节 `CustomLog`）。

当 `CustomLog` 指令设置为 `combined` 时，可用选项如下：

- %h（远程主机的 IP 地址或主机名）
列出请求客户端的 IP 地址。如果 `HostnameLookups` 设置为 `on`，除非无法从 DNS 获取主机名，否则将记录客户端主机名。

- %l (rfc931)
不使用。日志文件中的该字段显示连字符 `[-]`。

- %u（身份验证用户）
如果需要身份验证，则列出记录的用户名。通常不使用此，因此日志文件中的该字段显示连字符 `[-]`。

- %t（日期）
列出请求的日期和时间。

- %r（请求字符串）
列出完全来自浏览器或客户端传来的请求字符串。

- %s（状态）
列出返回给客户端主机的 HTTP 状态码。

- %b（字节）
列出文档的大小。

- %(Referer)i（引用者）
列出将客户端主机引用到 Web 服务器的网页 URL。

- %(User-Agent)i（用户代理）
列出发出请求的 Web 浏览器类型。

## 10.5.41. CustomLog

`CustomLog` 识别日志文件和日志格式。默认情况下，日志记录在 `/var/log/httpd/access_log` 文件。

默认的 `CustomLog` 格式为 `combined`。以下展示了组合日志文件格式：

| remote | rfc931 | user | date | "request" | status | bytes | referrer | user-agent |
|---|---|---|---|---|---|---|---|---|

## 10.5.42. ServerSignature

`ServerSignature` 指令向任何服务器生成的文档添加包含 Apache HTTP 服务器版本和 `ServerName` 的行，例如发送给客户端的错误消息。`ServerSignature` 默认设置为 `on`。

也可以将其设置为 `off` 或 `EMail`。`EMail` 在自动生成的响应的签名行中添加一个 `mailto:ServerAdmin` HTML 标签。

## 10.5.43. Alias

`Alias` 指令允许访问 `DocumentRoot` 目录之外的目录。任何以别名结尾的 URL 都会自动解析为别名路径。默认情况下，`icons` 目录的别名已被 Web 服务器访问，但该目录不在 `DocumentRoot` 中。

## 10.5.44. ScriptAlias

`ScriptAlias` 指令允许 `DocumentRoot` 目录之外的目录被访问。任何以别名结尾的 URL 都会自动解析为别名路径。默认情况下，`icons` 目录的别名已被 Web 服务器访问，但该目录不在 `DocumentRoot` 中。 (注：此处原文似乎存在重复或错误，已按逻辑翻译)

## 10.5.45. Redirect

当使用 `Redirect` 时，它可以将文件映射到新的 URL。格式如下：

```
Redirect /old-path http://<current-domain>/<file-name>
```

在此示例中，<old-path> <current-domain>/<file-name>

在此示例中，<old-path> <current-domain>/<file-name>

在此示例中，<old-path> <current-domain>/<file-name>

有关更多重定向技术，请使用 `mod_rewrite` 模块。有关配置 `mod_rewrite` 的更多信息，请参阅 http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html。

## 第 10 章 Apache HTTP Server

## 10.5.46. IndexOptions

`IndexOptions` 通过添加图标、文件描述等控制列表的外观。如果设置了 `Options`（参见第 10.5.25 节），当 Web 服务器接收到目录请求时会生成列表。

首先，服务器会在请求目录中查找匹配的文件。如果没有找到 `index.html` 文件，Apache 服务器将生成目录的 HTML 列表。此列表的外观由 `IndexOptions` 指令控制。

默认配置使用 `FancyIndexing`。这意味着用户可以通过表头进行排序。再次点击同一个表头将升序切换为降序。Fancy 还会根据文件扩展显示不同的图标。

`AddDescription` 选项与 `FancyIndexing` 配合使用时，可以在生成的目录列表中显示文件的简短描述。

`IndexOptions` 还有许多其他可以控制生成目录外观的参数。包括 `IconHeight` 和 `IconWidth`，允许服务器在生成的网页中为图标添加 HTML 的 `HEIGHT` 和 `WIDTH` 标签；`IconsLinks` 则让图标与文件名一起作为 HTML 链接的一部分。

## 10.5.47. IndexByEncoding

该指令在生成的目录列表中，根据具有 MIME 编码的文件显示其对应的图标。例如，默认情况下，Web 服务器会在生成的目录列表中为 MIME 编码的 x-gzip 和 x-zip 文件显示 `compressed.gif` 图标。

## 10.5.48. IndexByType

该指令在生成的目录列表中，根据具有 MIME 类型的文件显示图标。例如，服务器会在生成的目录列表中为 MIME 类型为 text 的文件显示 `text.gif` 图。

## 10.5.49. AddIcon

`AddIcon` 指定在生成的目录列表中为特定扩展名显示图标。例如，Web 服务器设置为为 .bin 或 .exe 扩展的文件显示 `binary.gif` 图标。

## 10.5.50. DefaultIcon

`DefaultIcon` 指定未指定其他图标的文件在生成的目录列表中显示的图标。默认是 `unknown.gif` 图像。

## 10.5.51. AddDescription

当将 `FancyIndexing` 作为 `IndexOptions` 参数使用时，可以使用 `AddDescription` 指令在生成的目录列表中为特定文件或文件类型显示自定义描述。`AddDescription` 指令支持列出特定文件、通配符表达式和文件扩展名。

