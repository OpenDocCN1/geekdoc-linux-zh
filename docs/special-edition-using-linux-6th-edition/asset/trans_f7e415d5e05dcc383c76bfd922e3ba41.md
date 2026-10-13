
- **AddIconByType**—按 MIME 文件类型指定图标。类型由 `mime.types` 配置文件中的设置决定。
- **AddIconByEncoding**—按 MIME 编码指定图标。文件编码类型由 `AddEncoding` 指令定义。
- **AddAlt**—按文件扩展名分配 alt 字符串。
- **AddAltByType**—按 MIME 文件类型分配 alt 字符串。
- **AddAltByEncoding**—按 MIME 编码分配 alt 字符串。
- **DefaultIcon**—当无法为此条目找到其他图标时，指定要使用的图标。

Add... 指令的语法如下：

```
<directive> <icon> <match> [<match2> ...]
```

对于任意 AddIcon... 指令，你可以在图标字段中仅指定图标文件名，或指定 alt 字符串与图标文件名的组合。这样，如果你愿意，可以绕过 AddAlt... 指令。图标文件名是相对于 Web 服务器文档树的路径，而不是相对于本地文件系统的路径。此外，AddIcon 指令可以使用字符串 `^DIRECTORY^` 来匹配目录条目。以下示例展示了若干不同的图标分配行。其中一些在功能上有所重叠，但此处仅为说明目的而展示：

```
AddIcon /icons/binary.gif .bin .exe
AddIcon /icons/text.gif .txt
AddIconByType /icons/apache/text.gif text/*
AddAltByType "TXT" # text/*
AddIconByType (TXT,/icons/text.gif) text/*
AddIconByType (HTM,/icons/about.gif) text/html
AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip
AddIcon (DIR,/icons/folder.gif) ^DIRECTORY^
DefaultIcon /icons/unknown.gif
```

图标指令按照它们在 httpd.conf 文件中出现的顺序进行处理。Web 服务器使用它找到的第一个匹配项作为文件的图标。因此，为了让匹配生效，应将更具体的指令放在文件更靠前的位置。

当然，如果你想完全自定义目录列表页面的外观，也可以添加自己的图标文件。图标必须是 .gif 或 .jpg 格式，并位于文档树中的某个目录下。Apache 提供的默认图标位于 `/usr/local/apache/icons` 目录中，是 20×22 的 8 位彩色 GIF 文件。这些图标使用的颜色很少（这是一个好做法），并且具有透明背景。

## 使用描述

在增强型目录列表中，“描述”列包含每个条目的简短描述。Web 服务器根据服务器配置文件中使用的 `AddDescription` 指令，或根据文档的标题（如果是 HTML 文件）来确定此字段的值。

使用 `AddDescription` 指令为条目添加描述。例如，以下行在文档树的根目录为文件 foo.txt 添加描述：

```
AddDescription "foo text file" /foo.txt
```

服务器可以根据目录中 HTML 文档的标题，自动为目录列表添加描述。在 httpd.conf 中的 `IndexOptions` 指令中添加 `ScanHTMLTitles` 选项，即可让服务器执行此操作。请注意，这会导致服务器在每次读取目录时，都读取该目录中的每个 HTML 文件并解析出 HTML 标题。这会花费相对较长的时间，因此不应在繁忙的网站上使用。

## 控制列和目录格式

`IndexOptions` 指令使您能够控制增强型目录列表的其他几个方面。表 33.4 显示了您可以使用的选项及其对列表页面的影响。

**表 33.4 — 使用 IndexOptions 控制增强型目录列表的选项**

| 选项 | 含义 |
| --- | --- |
| `IconHeight=pixels` | Web 服务器在用于目录索引页面的 IMG 标记中包括图标的高度。这可以加快客户端浏览器对页面的处理。 |
| `IconWidth=pixels` | Web 服务器在用于目录索引的 IMG 标记中包括图标的宽度。 |
| `IconsAreLinks` | 这使得图标成为条目链接的一部分，因此用户可以单击条目名称或图标来访问它。 |
| `NameWidth=n\|*` | 指示文件名列的宽度。如果使用 *，则列会自动调整大小。 |
| `ScanHTMLTitles` | 服务器扫描 HTML 文件以获取其标题，用于“描述”列。 |
| `SuppressDescription` | 隐藏“描述”列。 |
| `SuppressLastModified` | 隐藏“最后修改”列。 |
| `SuppressSize` | 隐藏“大小”列。 |
| `SuppressColumnSorting` | 不要将列标题设置为可用于按该列对列表进行排序的链接。 |
| `SuppressHTMLPreamble` | 不要用标准 HTML 前言（HTML、HEAD 等）作为由 `HeaderName` 指定的文件的前缀。这使您可以更灵活地使用头文件控制页面输出。 |

## 自定义错误消息

Web 服务器会自动为某些错误情况生成错误消息响应。但是，您可以为您的网站自定义错误响应，以便在出错时向远程客户端提供您自己的消息（以及外观和感觉）。

使用 `ErrorDocument` 指令为特定错误情况自定义错误响应。该指令可以多次使用，为服务器生成的每个不同错误代码指定响应。Web 服务器使用的常见错误代码如表 33.5 所示。

**表 33.5 — 常见 HTTP 错误代码**

| 错误代码 | 摘要 | 含义 |
| --- | --- | --- |
| 400 | 错误请求 | 来自客户端的请求格式错误。 |
| 401 | 未授权 | 客户端必须提供用户名和密码才能访问该项。请注意，此代码的错误响应无法自定义，因为当客户端收到来自服务器的此错误时，会自动显示登录提示（而不是返回的页面）。 |
| 402 | 需要付款 | 访问请求的项要求客户端以某种方式付款。 |
| 403 | 禁止 | 不允许客户端访问该项。提供用户名和密码也无济于事。 |
| 404 | 未找到 | 服务器未找到与客户端提交的 URL 匹配的文档或目录。 |
| 500 | 致命错误 | 服务器遇到了无法解决的情况，无法满足请求。 |
| 501 | 未实现 | 服务器不支持请求的功能。 |
| 502 | 临时过载 | 由于负载过高，服务器无法处理请求。它可能稍后能够处理该请求。 |

错误文档可以通过多种方式指定。首先，您可以仅指定一个字符串作为 `ErrorDocument` 的值返回给用户。您也可以引用本地文件来返回静态错误页面，或者引用 CGI 脚本在请求时生成错误页面。使用 CGI 脚本可以让您自定义响应以完全匹配您的情况，因为脚本可以在发出请求时检查有关客户端、其请求以及本地文件系统的信息。最后，您还可以指定外部文档作为错误响应。

对于每条 `ErrorDocument` 指令，请指定错误代码，然后指定您希望服务器针对该错误响应的项目。以下是 `ErrorDocument` 行的一些示例：

```
ErrorDocument 400 "Hey, you sent invalid request."
ErrorDocument 402 http://www.example.com/pay_me.html
ErrorDocument 500 /fatal.html
ErrorDocument 404 /cgi-bin/missing.pl
```

## 按目录配置设置

当您在 httpd.conf 中使用控制文件信息、目录索引、错误响应和授权（稍后讨论）的配置指令时，它们适用于 Web 服务器提供的整个文档树。但是，您也可以将这些指令应用于系统中的特定目录和文件。

服务器以这种方式支持按目录自定义有几个不同的原因。首先，您可能希望网站上的某些目录对公众开放，而其他文件和目录则仅限于特定用户组。除了特定于安全的指令外，许多其他指令也具有重要的安全影响。例如，您通常不希望公众看到文档树中目录的内容。因此，习惯上对文档树中任何远程用户都可访问的部分禁用目录索引。但是，您可能仍然希望允许组织内的用户进行索引。

有时，网站的内容由公司中的不同组织维护。在这种情况下，他们可能有不同的策略和约定来控制其站点部分。例如，某个部门可能会对其部分内容使用服务器解析的 HTML 文件，而另一个部门则不会。由于服务器解析的 HTML 文件需要服务器进行额外处理，因此明智的做法是仅在文档树中需要它的部分使用它。

使用按目录设置可以精细控制服务器文档树的呈现、处理和访问控制。

### 按目录选项

可以按目录配置的一些主要选项由 `Options` 指令控制。该指令使您能够设置许多与目录相关的策略：

- **All**—除 `MultiViews` 之外的所有选项
- **ExecCGI**—允许执行 CGI 脚本。
- **FollowSymLinks**—服务器遵循此目录中的符号链接。这可能存在潜在的安全风险。
- **Includes**—允许服务器端包含（服务器解析的 HTML）。
- **IncludesNOEXEC**—允许服务器端包含，但不处理某些指令（`#exec` 和 `#include`）。
- **MultiViews**—当请求的文件不存在时，允许服务器选择与客户端请求最匹配的文档。这称为内容协商，在线手册 http://www.apache.org/docs/content-negotiation.html 中有介绍。
- **SymLinksIfOwnerMatch**—如果链接的目标与链接具有相同的所有者 ID，则允许服务器遵循符号链接。

> **警告**
> 
> 此列表中的大多数选项都具有重要的安全后果。例如，允许 Web 服务器执行任何类型的操作（例如，使用 `ExecCGI` 和 `Includes`）可能会导致未经授权的用户让更多客户端运行危险程序或脚本。在多用户系统上使用这些选项之前，请查阅每个选项的在线文档，了解有关安全影响的信息。
